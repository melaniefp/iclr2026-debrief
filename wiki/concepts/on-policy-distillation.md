---
title: "On-Policy Distillation"
type: concept
tags:
  - knowledge-distillation
  - reinforcement-learning
  - post-training
  - on-policy-learning
related:
  - "wiki/concepts/knowledge-distillation.md"
sources:
  - "raw/multi-teacher-on-policy-distillation-new-post-training.md"
---

# On-Policy Distillation

On-policy distillation (OPD) is a training paradigm where a student model generates its own rollouts and receives dense, token-level supervision from a teacher model via reverse KL divergence, combining the benefits of knowledge distillation with on-policy reinforcement learning.

## Key ideas

- **Reverse KL as advantage**: The OPD loss replaces GRPO's group-relative advantage with the log-ratio $\log \frac{\pi_{\text{teacher}}}{\pi_{\text{student}}}$ at each token, acting as a dense per-token reward signal. When the teacher assigns higher probability than the student, the gradient pushes the student to upweight that token.
- **Mode-seeking behavior**: Reverse KL is mode-seeking — it encourages the student to concentrate on the teacher's major modes rather than spreading probability across void regions (unlike forward KL, which is mean-seeking and used in off-policy distillation).
- **Group size 1**: Because the advantage comes from the teacher distribution rather than a group baseline, OPD needs only one rollout per prompt, making it throughput-optimal.
- **Multi-Teacher OPD (MOPD)**: The natural extension uses multiple domain-expert teachers. Each prompt is routed to the appropriate teacher based on domain, and the student absorbs capabilities from all teachers simultaneously. This addresses the see-saw problem where sequential specialization stages trade off capabilities against each other.
- **IcePop masking**: To handle train-inference logit mismatches (different kernels, batch invariance, MoE routing nondeterminism), IcePop masks out tokens whose train/infer probability ratio falls outside a tolerance band.
- **Going beyond teachers**: MiMo-V2-Flash combines OPD with an outcome reward model advantage, allowing the student to exceed teacher accuracy. ExOPD extrapolates beyond the teacher using a teacher-reference delta.

## Adoption in frontier models (2026)

Four frontier models converged on MOPD in early 2026:

- **MiMo-V2-Flash** — final-stage MOPD with mixed teacher types (SFT, RL, Self) + ORM advantage
- **GLM-5** — final-stage MOPD with stage-terminal checkpoint teachers, pure reverse-KL
- **Nemotron-Cascade 2** — mid-pipeline MOPD as a stabilization step between RL stages
- **DeepSeek-V4** — scaled MOPD with 10+ teachers, full-vocabulary logit distillation, purpose-built infra

## Sources

- [Multi-Teacher On-Policy Distillation: A New Post-Training Primitive](../../raw/multi-teacher-on-policy-distillation-new-post-training.md) — Yumo Xu's survey of MOPD across four 2026 frontier models

## Related concepts

- [Knowledge Distillation](knowledge-distillation.md)
