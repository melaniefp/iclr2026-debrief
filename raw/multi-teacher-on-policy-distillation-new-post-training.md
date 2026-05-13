---
title: "Multi-Teacher On-Policy Distillation: A New Post-Training Primitive"
url: "https://yumoxu.notion.site/multi-teacher-on-policy-distillation"
source: "other"
author: "Yumo Xu"
date: "2026-04-29"
captured: "2026-05-08"
tags:
  - knowledge-distillation
  - reinforcement-learning
  - post-training
  - language-models
  - on-policy-learning
aliases:
  - "MOPD"
  - "Multi-Teacher OPD"
  - "On-Policy Distillation"
related:
  - "wiki/papers/discrete-mmd-distilling-discrete-diffusion.md"
  - "wiki/concepts/on-policy-distillation.md"
  - "wiki/concepts/knowledge-distillation.md"
---

# Multi-Teacher On-Policy Distillation: A New Post-Training Primitive

Yumo Xu | [Website](https://yumoxu.github.io/) | [X](https://x.com/yumoxu) | [LinkedIn](https://www.linkedin.com/in/yumoxu/)

April 29, 2026

## Intro: Why OPD?

Modern post-training has a see-saw problem: Math RLVR shortens reasoning traces and hurts open-ended writing. RLHF buys preference alignment at the cost of strict instruction following. Tool-use RL drifts away from STEM benchmarks. When every specialization stage trades against the others, shipping one model that holds onto everything becomes difficult.

On-policy distillation (OPD) has emerged as a standard fix. The idea: sample trajectories from the student, then match a teacher's distribution along those rollouts via reverse KL. You get dense, token-level supervision that drops into a GRPO-style training loop almost unchanged. The natural extension is multi-teacher OPD (MOPD): make each capability's strongest checkpoint a teacher and let the student absorb them all at once. Teachers usually share a tokenizer and lineage with the student, so the engineering overhead stays small.

This post walks through four 2026 frontier reports that all converge on MOPD but deploy it differently: [MiMo-V2-Flash](https://arxiv.org/pdf/2601.02780) (Jan), [GLM-5](https://arxiv.org/pdf/2602.01657) (Feb), [Nemotron-Cascade 2](https://arxiv.org/pdf/2603.05296) (Mar), and [DeepSeek-V4](https://arxiv.org/abs/2604.06527) (Apr):

- **Final-stage consolidation** (MiMo-V2-Flash, GLM-5): MOPD as the last step of post-training.
- **Mid-pipeline stabilization** (Nemotron-Cascade 2): MOPD as a forgetting-recovery step between RL specialization stages.
- **Scaled-up training regime** (DeepSeek-V4): full-vocabulary logits, 10+ teachers, purpose-built infra for teacher scheduling and fault-tolerant rollouts.

After a quick GRPO → OPD primer, we'll go through each in turn and discuss what's converged, what diverged, and what's ahead.

## Background

### Original GRPO

The GRPO defines the following loss to minimize:

$$
\small{
\begin{align*}
-\mathbb{E}_{
\{y_i\}_{i=1}^G \sim \pi_{\textcolor{red}{\text{infer}}}(\cdot \mid x; \theta_{\rm old})} \left[
\frac{1}{G} \sum_{i=1}^G \frac{1}{|y_i|} \sum_{t=1}^{|y_i|} \Big[
\min \left( r_{i,t}
\textcolor{purple}{\widehat{A}_{i,t}}, \text{clip} \left( r_{i,t}, 1 - \varepsilon, 1 + \varepsilon \right) \textcolor{purple}{\widehat{A}_{i,t}} \right)
\Big]
\right]
\end{align*}
}
$$

where the PPO-like importance sampling ratio per token $r_{i,t} = \frac{\pi_{\textcolor{blue}{\text{train}}}(y_{i,t} \mid x, y_{i,<t}; \theta)}{\pi_{\textcolor{red}{\text{infer}}}(y_{i,t} \mid x, y_{i,<t}; \theta_{\text{old}})}$.

Group-relative advantage per token is defined as:

$$
\textcolor{purple}{\widehat A_{i,t}} =
\frac{R_i − \text{mean}(R_1, . . . , R_G)}
{\text{std}(R_1, . . . , R_G)}
$$

where $R_i$ is the outcome reward for the $i$-th rollout in a group.

### From GRPO to OPD

We can obtain the OPD training loss via simply replacing the advantage term in GRPO with the *reverse* KL divergence between the student policy and teacher policy:

$$
\textcolor{purple}{\widehat A_{i,t}} = \text{sg}\left[
\log \frac{\pi_{\textcolor{red}{\text{infer}}}(y_{i,t} | x, y_{i,<t} ; \theta_\text{teacher})}
{\pi_{\textcolor{blue}{\text{train}}}(y_{i,t} | x, y_{i,<t} ; \theta)}
\right]
$$

where $\text{sg}$ is a stop-gradient operator. Because the advantage now comes from the teacher's distribution rather than from a group baseline, there's no need to roll out multiple samples per prompt to compute relative advantage. Setting group size to 1 is therefore both valid and throughput-optimal.

Concretely, when the teacher assigns higher probability than the student to a sampled token, the advantage is positive and the gradient pushes the student to upweight that token; when the teacher assigns lower probability, the gradient pushes it down. The teacher acts as a dense, per-token reward.

### Why reverse KL?

Reverse KL naturally fits OPD, as it allows sampling from student policy:

$$
\text{KL}[
\pi_{\textcolor{blue}{\text{train}}}(\theta_\text{student}) ||
\pi_{\textcolor{red}{\text{infer}}}(\theta_\text{teacher})
]  = \mathbb{E}_{y \sim  \pi_{\textcolor{blue}{\text{train}}}(\theta_\text{student})}
[\log
\frac{\pi_{\textcolor{blue}{\text{train}}}(\theta_\text{student})}{\pi_{\textcolor{red}{\text{infer}}}(\theta_\text{teacher})}
]
$$

On the other hand, forward KL divergence $\text{KL}[\pi_{\textcolor{red}{\text{infer}}}(\theta_\text{teacher})|| \pi_{\textcolor{blue}{\text{train}}}(\theta_\text{student})]$ is a standard objective for (off-policy) sequence knowledge distillation.

This objective difference also leads to different training dynamics. Forward KL is **mean-seeking**: it forces $\pi_{\textcolor{blue}{\text{train}}}$ to cover all modes of $\pi_{\textcolor{red}{\text{infer}}}$. While it is a common choice for simple tasks where both distributions have few modes, many real-world tasks are typically much more complex, and minimizing forward KL divergence causes $\pi_{\textcolor{blue}{\text{train}}}$ to assign unreasonably high probabilities to the void regions of $\pi_{\textcolor{red}{\text{infer}}}$ and produces very unlikely samples.

On the other hand, reverse KL divergence is **mode-seeking**: it encourages $\pi_{\textcolor{blue}{\text{train}}}$ to assign high probability to the major modes of $\pi_{\textcolor{red}{\text{infer}}}$ and low probabilities to the void regions. This makes reverse KL divergence the typical choice in OPD. We refer readers to MiniLM which provides detailed discussions and comparison results.

### Train-inference gap: IcePop

Training and inference engines often produce different logits for the same input, due to different kernels, batch invariance, etc. The gap widens in MoE RL accounting for additional factors such as expert routing nondeterminism. ***IcePop*** addresses this by masking out tokens whose train/infer probability ratio falls outside a tolerance band, dropping the noisiest updates entirely.

The masked OPD/GRPO objective then becomes:

$$
\small{\begin{align*}
-\mathbb{E}_{
\{y_i\}_{i=1}^G \sim \pi_{\textcolor{red}{\text{infer}}}(\cdot \mid x; \theta_{\rm old})} \left[ \frac{1}{G} \sum_{i=1}^G \frac{1}{|y_i|} \sum_{t=1}^{|y_i|} \left[ \mathcal{M}\Bigl(\frac{\pi_{\textcolor{blue}{\text{train}}}(y_{i,t} \mid x, y_{i,<t};\theta_{\text{old}})}{\pi_{\textcolor{red}{\text{infer}}}(y_{i,t} \mid x, y_{i,<t}; \theta_{\mathrm{old}})}; \alpha, \beta\Bigr)
\cdot \min \left( r_{i,t}
\textcolor{purple}{\widehat A_{i,t}},
\text{clip} \left( r_{i,t}, 1 - \varepsilon, 1 + \varepsilon \right) \textcolor{purple}{\widehat A_{i,t}} \right) \right]
\right] &\end{align*}}
$$

where $\mathcal{M}$ is the masking function. This forgoes all noisy updates in cases where the mismatch is large. Note that three out of the four models (MiMo-V2-Flash, GLM-5 and Nemotron-Cascade 2) that we will cover in this blog explicitly mentioned the adoption of IcePop in their training objective.

### MOPD setup in recent foundation models

The table below summarizes the differences among the four recent models regarding their OPD adoption, along five axes: which checkpoint initializes the student, how the teacher pool is assembled, where the prompts are sampled, where MOPD slots into the pipeline, and the exact advantage estimator. The rest of this post walks through each along this taxonomy.

## MiMo-V2-Flash & GLM-5: Final Capability Merging and Recovery

### Overview

**MiMo-V2-Flash: Mixed-Source Teacher Pool.** MiMo-V2-Flash starts from the general SFT checkpoint and assembles teachers from across the post-training pipeline: domain-specific SFT models, RL-trained specialists, and the student model itself ("Self").

**Teacher routing:** Each prompt carries a domain label that deterministically selects a single teacher; per-token advantages are computed against that one teacher. Multi-teacher aggregation is therefore implicit: it happens through sample-level domain mixing, not through per-token ensembling. The "multi-teacher" framing reflects the *pool* of teachers the student trains against, not a per-token weighted combination.

Used as a final-stage step, MOPD here is doing two jobs at once: capability merging across heterogeneous teacher types, and stabilization against the over-specialization introduced by domain-specific SFT and RL. To further decouple the student from any individual teacher's imperfections, MiMo-V2-Flash additionally interpolates an outcome-reward advantage on top of the OPD signal, which we will discuss in the next subsection.

**GLM-5: Stage-Terminal Teachers.** GLM-5 starts from the final post-RL checkpoint produced by a sequential Reasoning → Agentic → General RL pipeline. It uses each preceding stage's terminal checkpoint as a teacher. Prompts are drawn from each teacher's own RL training set, so teacher routing is implicit: each prompt pairs with the stage that originally trained on it. Unlike MiMo's mixed-type teacher pool, GLM-5's teachers share lineage and differ only in *when* they were taken from the pipeline. The role MOPD plays here is therefore slightly different: it's mainly for capability *recovery* rather than capability *merging* across domain teachers. The advantage term stays pure reverse-KL OPD.

In summary, both models position OPD as the final post-training stage, but they differ in two concrete ways. First, **teacher composition**: MiMo-V2-Flash routes each prompt deterministically to one of several teacher *types* (SFT, RL specialist, or Self) keyed off the prompt's domain; GLM-5 uses the terminal checkpoint of each prior post-training *stage* as a teacher, with prompts drawn from that stage's RL training set. Second, **what augments the OPD loss**: MiMo adds a scaled outcome-reward advantage on top of reverse KL (which will be introduced in the next subsection) while GLM-5 uses pure reverse-KL OPD.

### Going beyond teachers

**Interpolation with outcome reward.** A limitation of pure OPD is that the student is optimized to match the teacher's token-level distribution rather than directly optimize task success. When the teacher is strong, dense token-level supervision is a feature; but pure imitation also propagates the teacher's mistakes, style biases, and suboptimal reasoning patterns.

MiMo-V2-Flash addresses this by combining dense OPD advantage with an advantage from an outcome reward model (ORM). The final advantage is given by:

$$
\begin{align*}
\textcolor{purple}{\widehat A_{i,t}} &=
{\textcolor{purple}{\widehat A_{i,t}^\text{OPD}}} + \alpha {\textcolor{purple}{\widehat A_{i,t}^\text{ORM}}}
\end{align*}
$$

Here, $\alpha$ scales the outcome-reward advantage against the OPD log-ratio. The paper does not report its value or sensitivity, so the trade-off between dense imitation and outcome supervision is left implicit.

**What's $\hat{A}^{\text{ORM}}$?** The paper writes the outcome-reward term generically as "advantages computed by the ORMs, including GRPO". GRPO is one natural instantiation but adds complexity: it requires $G$ rollouts per prompt to compute the group baseline, which raises an open question — are those same rollouts also used for the OPD log-ratio, or is OPD computed on a separate $G=1$ rollout? Other ORM instantiations (e.g., a learned scalar reward minus a value baseline in PPO) preserve G = 1 throughout. The paper does not specify which it uses.

Nevertheless, the MOPD-vs-MOPD-w/o-ORM ablation does show that the ORM term contributes non-trivially.

A useful way to view MiMo's design is that it keeps OPD as the main dense supervision, but uses outcome reward as an external, corrective signal. This decouples the student from any single teacher's ceiling. Empirically, the combined advantage lets the student *exceed* teacher accuracy on several benchmarks.

**Connection with reward extrapolation.** The "going beyond teacher imitation" problem has been studied independently in ***ExOPD***, which takes a related but distinct approach. ExOPD introduces an additional reference model, which is, in practice, a pre-RL student/teacher checkpoint. It measures the teacher-reference delta, and *extrapolates* beyond the teacher in the direction where the teacher differs from the reference.

From the perspective of learning objectives, MiMo-V2-Flash combines teacher imitation and outcome reward, while ExOPD combines the imitation with the teacher-reference delta. The signals differ, but the structural recipe is identical: keep OPD as the dense imitation core, then add a scaled corrective term. The choice of corrective signal reflects what you trust more (verifiable rewards vs. trajectory of teacher improvement).

### Who is the best teacher?

Across the 12 benchmarking tasks, RL, Self and SFT are the best teacher on 6, 5, and 1 tasks, respectively. This reveals some interesting patterns.

Firstly, RL teachers dominate verifiable-reward benchmarks (math, code, reasoning), while Self wins where the SFT/RL teachers are more likely to distort calibration on broad / open-ended tasks.

Also, MOPD's student exceeds the best teacher on 8 of 12 tasks (largest gain: +4.1 on Arena-Hard Hard Prompt) and underperforms on 4 (largest loss: −6.3 on BrowseComp, where SFT was the best teacher).

One note here is the paper did not say that the best-performing teacher per benchmark was used in the final MOPD. That is a plausible interpretation, but not confirmed.

This is important as the **best standalone teacher ≠ best distillation teacher**. Higher benchmark score can come with worse calibration, worse log-prob support on student rollouts, worse token-level guidance, or a distribution/style mismatch. OPD cares about the teacher's conditional distribution over the student's on-policy samples, not just the teacher's final task accuracy.

## Nemotron-Cascade 2: Intermediate Training Stabilization

One critical observation from Nemotron-Cascade 2 is capability drift as the number of training environments increases. This includes:

- Non-math RLVR → Math Reasoning: certain RLVR training often reduces model entropy and shortens reasoning traces, thus can negatively impact mathematical reasoning performance, and
- RLHF → IF: RLHF-oriented optimization can partially trade off against instruction-following behavior.

Where MiMo-V2-Flash and GLM-5 place MOPD at the end of the pipeline as a consolidation step, Nemotron-Cascade 2 inserts it mid-pipeline as a stabilization step. The role shifts: instead of merging or recovering at the very end, MOPD is a periodic re-anchor between specialization stages.

In Nemotron's cascade RL pipeline, each downstream stage is liable to regress capabilities established earlier — math reasoning lost during instruction-following RL, instruction following lost during RLHF. Inserting MOPD as a mid-pipeline reset re-anchors the student to the strongest checkpoint of each capability before further specialization, so subsequent stages train on top of a balanced policy.

### Multi-Domain RL before MOPD

As part of the foundation for MOPD, Nemotron-Cascade 2 performs Multi-domain RL that covers three capabilities: multiple-choice QA in the STEM domain (55%), agentic tool calling (30%), and structured output for instruction following (15%).

The authors chose to group these domains into a single multi-domain RL stage for two main reasons:

- First, no performance degradation across evaluation benchmarks is observed when training on the blended domains. Instead, the model exhibits consistent improvements on benchmarks including MMLU-Pro, τ-Bench, and IF-Bench.
- Second, the response lengths and verification times of these datasets are similar, which minimizes training inefficiencies caused by waiting for longer generations or slower environment verification.

### MOPD implementation

In the main experiments, Nemotron-Cascade 2 uses three teachers, one per capability: a math teacher (the SFT init), an RLHF teacher (helpfulness/safety alignment from the RLHF stage), and a multi-domain teacher (the IF-RL + Multi-domain RL checkpoint).

Note: Nemotron's math teacher is the *SFT initialization itself*, not a math-specialized RL checkpoint. The team relies on the curated SFT data alone for math signal. This is a deliberate choice when SFT data quality is high enough that further math RL would risk shortening reasoning traces (the regression mode the paper itself flags).

Overall, teacher checkpoints are selected directly from the Cascade RL pipeline by choosing the strongest validation checkpoint for each benchmark category, which makes it easy to assemble a capability-diverse teacher pool without introducing external model families.

Prompts are sampled from the RL training data pools (RLHF, IF-RL, and Multi-domain), as well as from AceReason-Math for math. Similar to MiMo-V2-Flash, Nemotron-Cascade 2 applies **IcePop-style** truncated importance weighting to account for train-inference mismatch.

### Benefits in training efficiency

MOPD is substantially more sample- and step-efficient in practice. Starting from the same initial checkpoint, MOPD reaches teacher-level performance substantially faster than GRPO on AIME25 and outperforms RLHF with far fewer steps on ArenaHard v2.

## DeepSeek-V4: Scaling MOPD with Better Infra

DeepSeek-V4 trains domain experts independently, using domain-specific SFT + RL (GRPO). This is slightly different from the other three reports where domain teachers are composed of a mixture of {SFT, RL, Self} models, and which can all be traced back to the initial checkpoint from general SFT.

The teacher composition is mostly an empirical choice. What distinguishes DeepSeek-V4's OPD is its *scale* along two axes that together demand purpose-built infra:

1. **Full-vocabulary logit distillation:** Prior OPD-style implementations often estimate KL only on the sampled token. That is cheaper, but it gives high-variance gradients and can cause instability. So they preserve the full logit distribution when computing reverse KL.
2. **Number of teachers in MOPD:** More than ten teacher models are used to distill one student. The 10+ teachers span at least four domains (math, coding, agent, instruction following), with some domains further split across three reasoning-effort modes (Non-think, Think High, Think Max), each trained as a separate specialist with its own RL configuration.

These scaling factors, together with the model size (1.6T parameters, 49B activated in DeepSeek-V4-Pro) and context size (1M tokens), pose a set of new challenges to the infra stack. We will introduce them next.

### Efficient teacher scheduling

**Challenge.** There are two major memory challenges when adopting full-vocab multi-teacher OPD. First, there are many teachers. DeepSeek says the framework supports an effectively *unbounded* number of teachers, each potentially very large.

Second, full logits are huge. For vocabulary size above 100K, logits are: num_tokens × vocab_size. For long sequences, naively storing full teacher logits for every token and every teacher explodes quickly.

To address these two challenges, DeepSeek made a series of improvements in their infra.

**Aside: FP4 for inference-only forwards.** Although not OPD-specific, DeepSeek-V4's FP4 (MXFP4) quantization is worth flagging here: it applies to all inference-only forward passes, including teacher and reference. Training steps stay in FP8 via a lossless FP4→FP8 dequantization, leaving the backward pipeline unchanged. The savings here are critical in OPD as each batch may fire 10+ teacher forwards.

### Correct and efficient resumption: Preemptible and fault-tolerant rollout service

DeepSeek uses a preemptive scheduler: any running task may be preempted. Hardware failures are also common at large scale.

For normal supervised training, a failed mini-batch can often be retried. For OPD/RL rollout, it is more delicate. The model is sampling stochastic trajectories. If recovery uses fresh randomness, you're sampling a new trajectory, and the on-policy training distribution drifts.

For instance, if a long generation is interrupted and you restart from scratch with fresh randomness, you are not continuing the same sample. You are drawing a new one. That creates length bias:

- Short completions are more likely to finish before interruption.
- Long completions are more likely to be interrupted.
- If interrupted completions are freshly resampled, long samples are replaced more often.

This skews the accepted-sample distribution toward shorter outputs. Due to this length bias, regenerating unfinished requests from scratch is mathematically incorrect.

**Approach.** DeepSeek implements a **token-granular Write-Ahead Log** (**WAL**): Whenever a new token is generated, it is immediately appended to the request's WAL. During preemption, the inference engine pauses and saves the KV cache of unfinished requests. On resumption, the system continues decoding from the persisted WAL and saved KV cache. If there is a fatal hardware error, it can rerun prefill on the persisted WAL tokens to reconstruct the KV cache.

Suppose the model starts generating: A B C D E F. Due to cluster failure, the task gets preempted after: A B C. WAL helps persist A B C in a log, and restore or reconstruct its KV cache. The generation can resume from C. This preserves the identity of the original sample.

- Deterministic regeneration with the same seed could fix correctness if the inference stack is batch-invariant and deterministic. But that still requires rerunning decoding from the beginning, so it is less efficient than WAL.

**Extension to Agentic OPD/RL.** For agentic tasks, the rollout includes *environment transitions* in addition to model-generated tokens. If environment transitions are not reproducible, the OPD data is corrupted: the student may be trained on trajectories that would not have happened under the original environment state.

DeepSeek handles fault tolerance in agentic tasks within a separate **DeepSeek Elastic Compute** (DSec). Specifically, DSec keeps a globally ordered trajectory log for each sandbox. It records every command invocation and result. On resumption, it can fast-forward by replaying cached results instead of rerunning commands. This avoids errors from re-executing non-idempotent operations and enables deterministic replay. This is the sandbox analogue of token WAL.

### Efficient global planning: decoupling metadata from per-token payload

OPD needs both global planning and per-token training data. Global planning asks:

1. How should we shuffle examples?
2. How should we pack variable-length sequences?
3. Which samples use which teacher?

These tasks don't need the heavy per-token payload (e.g., token ids, attention masks, teacher hidden states, etc) which becomes huge particularly in full-vocab OPD over a million-token context. If you load all heavy fields for all samples just to shuffle or pack data, memory pressure becomes enormous.

To avoid this, DeepSeek-V4 separates metadata loading (lightweight, for global planning) from per-token payload (heavy, for actual training). Specifically, metadata is loaded for the whole rollout dataset to do global shuffling and packing layout computation. Heavy per-token fields are loaded through a shared-memory data loader, avoiding duplicate intra-node copies. These heavy fields are released immediately after mini-batch consumption.

## Summary

**Convergence.** The four frontier reports span very different models: 309B–1.6T parameters, 32k–1M context, agent-first to math-first emphasis. Yet, they land on a remarkably consistent OPD core. All adopt reverse KL over student rollouts as the central loss, employ a multi-teacher framework, and three of four explicitly adopt IcePop-style train/inference mismatch mitigation.

The convergence is notable because the underlying motivations differed: capability merging across heterogeneous specialists (MiMo-V2-Flash, DeepSeek-V4) versus forgetting recovery across sequential RL stages (GLM-5, Nemotron-Cascade 2). Reverse-KL OPD turned out to be the right primitive for both.

**Divergence.** A few interesting differences sit downstream of the algorithm:

- **Teacher composition.** MiMo-V2-Flash mixes teacher *types* (SFT, RL specialist, Self); GLM-5 chains *stages* (each prior post-training stage's terminal checkpoint); Nemotron-Cascade 2 mixes *capabilities* (math-as-SFT-init, RLHF teacher, multi-domain RL teacher); DeepSeek-V4 scales *count* (10+ RL specialists, no SFT-only, no Self).
- **Position in the pipeline.** MiMo-V2-Flash, GLM-5, and DeepSeek-V4 run MOPD at the end as a final consolidation. Nemotron-Cascade 2 runs it mid-pipeline as a stabilization point *between* specialization stages. The choice reflects whether you do forgetting recovery once at the end or continuously reset drift.
- **What augments the OPD signal.** MiMo-V2-Flash adds a scaled ORM advantage. The other three keep the OPD term pure.
- **Engineering scale.** Only DeepSeek-V4 pushed scale into a regime requiring purpose-built infra: full-vocabulary teacher logits, 10+ teachers, 1.6T parameters, 1M-token context. The other three treat OPD as a comparatively lightweight overlay on existing RL infrastructure.

To close, we'd like to highlight a few directions for future research:

- *Scaling teacher count and teacher size.* DeepSeek-V4 shows 10+ trillion-parameter teachers are feasible with the right infra. Whether the marginal benefit of each additional teacher continues to scale or saturates is unknown.
- *Black-box distillation.* All four reports rely on teacher logit access. Distilling from API-only teachers, where only sampled tokens are visible, opens a different design space.
- *Teacher-student co-evolution.* Distilled students re-enter specialist training to produce stronger teachers in an outer loop. The compute cost is substantial; whether the gains compound or diminish across generations is the empirical question worth answering.
