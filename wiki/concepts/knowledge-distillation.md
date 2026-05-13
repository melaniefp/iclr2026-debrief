---
title: "Knowledge Distillation"
type: concept
tags:
  - knowledge-distillation
  - model-compression
  - language-models
related:
  - "wiki/concepts/on-policy-distillation.md"
sources:
  - "raw/multi-teacher-on-policy-distillation-new-post-training.md"
  - "raw/flow-maps-learning-integral-diffusion-model.md"
  - "wiki/papers/discrete-mmd-distilling-discrete-diffusion.md"
---

# Knowledge Distillation

Knowledge distillation is a technique for transferring knowledge from one or more teacher models to a (typically smaller or more general) student model, by training the student to match the teacher's output distribution rather than just ground-truth labels.

## Key ideas

- **Soft targets**: The student is trained to match the teacher's softened output distribution (logits / probabilities), which carries richer information than hard labels alone.
- **Forward vs. reverse KL**: Standard (off-policy) distillation minimizes forward KL, which is mean-seeking and forces the student to cover all teacher modes. On-policy distillation uses reverse KL, which is mode-seeking and focuses the student on the teacher's major modes.
- **Multi-teacher distillation**: Using multiple domain-expert teachers allows the student to absorb diverse capabilities. Teacher selection can be static (fixed weights), dynamic (RL-guided), or domain-routed (each prompt mapped to one teacher).
- **On-policy vs. off-policy**: Off-policy distillation trains the student on teacher-generated data. [On-policy distillation](on-policy-distillation.md) trains on student-generated rollouts with teacher feedback, avoiding exposure bias and distribution mismatch.
- **Full-vocabulary vs. sampled-token**: Full-vocabulary logit distillation (as in DeepSeek-V4) computes KL across the entire vocabulary, giving lower-variance gradients but higher memory cost. Sampled-token estimation is cheaper but noisier.

## Sources

- [Multi-Teacher On-Policy Distillation](../../raw/multi-teacher-on-policy-distillation-new-post-training.md) — Survey of MOPD as a post-training primitive in frontier LLMs
- [Flow Maps](../../raw/flow-maps-learning-integral-diffusion-model.md) — Flow maps as distillation of diffusion models into few-step generators
- [Discrete MMD: Distilling Discrete Diffusion](../papers/discrete-mmd-distilling-discrete-diffusion.md) — Distillation applied to discrete diffusion models

## Related concepts

- [On-Policy Distillation](on-policy-distillation.md)
- [Flow Maps](flow-maps.md) — Distillation of diffusion models into few-step generators
