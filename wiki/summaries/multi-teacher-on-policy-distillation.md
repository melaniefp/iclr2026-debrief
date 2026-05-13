---
title: "Summary: Multi-Teacher On-Policy Distillation — A New Post-Training Primitive"
type: summary
tags:
  - knowledge-distillation
  - reinforcement-learning
  - post-training
  - language-models
  - on-policy-learning
related:
  - "wiki/concepts/on-policy-distillation.md"
  - "wiki/concepts/knowledge-distillation.md"
sources:
  - "raw/multi-teacher-on-policy-distillation-new-post-training.md"
---

# Summary: Multi-Teacher On-Policy Distillation — A New Post-Training Primitive

Multi-Teacher On-Policy Distillation (MOPD) is emerging as a standard post-training primitive for frontier LLMs, allowing models to absorb capabilities from multiple domain-expert teachers without the see-saw trade-offs of sequential specialization stages.

## Overview

Yumo Xu's blog post (April 2026) surveys how four recent frontier models — [MiMo-V2-Flash](https://arxiv.org/pdf/2601.02780) (Jan 2026), [GLM-5](https://arxiv.org/pdf/2602.01657) (Feb 2026), [Nemotron-Cascade 2](https://arxiv.org/pdf/2603.05296) (Mar 2026), and [DeepSeek-V4](https://arxiv.org/abs/2604.06527) (Apr 2026) — all converge on MOPD but deploy it differently. The core idea: sample rollouts from the student model, then use reverse KL divergence against a teacher's token-level distribution as a dense per-token reward signal, dropping neatly into a GRPO-style training loop.

## Key points

- **The see-saw problem**: Each post-training specialization stage (math RLVR, RLHF, tool-use RL) improves one capability at the cost of others. MOPD addresses this by having the student learn from multiple domain-expert teachers simultaneously.
- **From GRPO to OPD**: The OPD loss is obtained by replacing GRPO's group-relative advantage with a reverse-KL log-ratio between teacher and student. This provides dense, token-level supervision and eliminates the need for multiple rollouts per prompt (group size = 1).
- **Reverse KL is mode-seeking**: Unlike forward KL (mean-seeking, used in off-policy distillation), reverse KL encourages the student to focus on the teacher's major modes rather than spreading probability across void regions.
- **IcePop**: Three of four models adopt IcePop-style masking to handle train-inference logit mismatches, dropping noisy token updates where the train/infer probability ratio falls outside a tolerance band.

## How the four models differ

| Axis | MiMo-V2-Flash | GLM-5 | Nemotron-Cascade 2 | DeepSeek-V4 |
|------|--------------|-------|-------------------|-------------|
| Pipeline position | Final stage | Final stage | Mid-pipeline stabilization | Final stage |
| Teacher types | SFT + RL + Self | Stage-terminal checkpoints | Capability-specific | 10+ RL specialists |
| OPD augmentation | + ORM advantage | Pure reverse-KL | Pure reverse-KL | Pure reverse-KL |
| Scale | Standard | Standard | Standard | Full-vocab logits, purpose-built infra |

- **MiMo-V2-Flash** uniquely combines OPD with an outcome reward model (ORM) advantage, allowing students to *exceed* teacher accuracy on 8 of 12 benchmarks.
- **Nemotron-Cascade 2** uses MOPD mid-pipeline as a periodic re-anchor between specialization stages, preventing capability drift.
- **DeepSeek-V4** pushes scale to 10+ teachers with full-vocabulary logit distillation over 1.6T parameters and 1M-token context, requiring purpose-built infrastructure including token-granular write-ahead logs for fault-tolerant rollouts.

## Open directions

- Whether marginal benefit of additional teachers saturates at scale
- Black-box distillation from API-only teachers (no logit access)
- Teacher-student co-evolution across outer-loop generations

## Sources

- [Multi-Teacher On-Policy Distillation: A New Post-Training Primitive](../../raw/multi-teacher-on-policy-distillation-new-post-training.md) — Yumo Xu's blog post surveying MOPD across four 2026 frontier models
