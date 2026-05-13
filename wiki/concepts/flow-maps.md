---
title: "Flow Maps"
type: concept
tags:
  - diffusion-models
  - flow-maps
  - consistency-models
  - distillation
  - generative-models
related:
  - "wiki/concepts/knowledge-distillation.md"
  - "wiki/concepts/consistency-models.md"
sources:
  - "raw/flow-maps-learning-integral-diffusion-model.md"
  - "wiki/papers/discrete-mmd-distilling-discrete-diffusion.md"
---

# Flow Maps

A flow map $F(\mathbf{x}_s, s, t)$ is a neural network that predicts the position of any point on a diffusion sampling path from any other point on that same path, by directly learning the integral of the velocity field. Flow maps generalize consistency models and enable sampling in 1–8 steps instead of the 20–100 typical for diffusion models.

## Key ideas

- **Definition**: $F(\mathbf{x}_s, s, t) = \mathbf{x}_s + \int_s^t v(\mathbf{x}_\tau, \tau) \mathrm{d}\tau$, where $v$ is the velocity field from a diffusion model
- **Parameterizations**: Can predict the target position ($F$) or the average velocity ($V$) over the interval; the two are related by $F(\mathbf{x}_s, s, t) = \mathbf{x}_s + (t-s) V(\mathbf{x}_s, s, t)$
- **Three consistency rules**: Compositionality (two jumps = one jump), Lagrangian (output follows velocity when target moves), Eulerian (output stays fixed when source moves) — any one suffices for training
- **Training approaches**: Distillation from a teacher model, self-distillation (dual loss combining consistency + diffusion), or marginal-from-conditional learning (MeanFlow)
- **Stop-gradient and EMA**: Self-referential losses require careful gradient management via stop-gradient operations and exponential moving average parameters
- **Applications**: Fast sampling, reward-based steering (trajectory tilting), efficient likelihood evaluation, discrete/categorical data generation

## Notable methods

| Method | Rule | Setting | Key innovation |
|--------|------|---------|----------------|
| Consistency Models (CM) | Eulerian | Self-distill | First flow map; anchored to $t=0$ |
| MeanFlow / iMF | Eulerian | From scratch | Marginal-from-conditional learning |
| Terminal Velocity Matching (TVM) | Lagrangian | Self-distill | Full higher-order differentiation, 10B+ scale |
| Shortcut Models | Compositional | Self-distill | Step-doubling bootstrap |
| Align Your Flow (AYF) | Eulerian | Distillation | Scaled to FLUX.1-dev, 4-step sampling |
| FreeFlow | Lagrangian | Data-free | Distillation without training data |

## Relation to diffusion distillation

Flow maps are the **trajectory-based** approach to accelerating diffusion sampling. Alternative **distributional** approaches (DMD, IMM, ADD) instead minimize distance between output distributions directly, trading the bijective noise-data mapping for potentially higher sample quality in very few steps.

## Sources

- [Learning the integral of a diffusion model](../../raw/flow-maps-learning-integral-diffusion-model.md) — Comprehensive tutorial by Sander Dieleman covering theory, training, and 20+ methods
- [Discrete MMD](../papers/discrete-mmd-distilling-discrete-diffusion.md) — Distillation of discrete diffusion models (related: flow maps for categorical data)

## Related concepts

- [Knowledge Distillation](knowledge-distillation.md) — Flow map training from a teacher is a form of distillation
- [Consistency Models](consistency-models.md) — Special case of flow maps with target anchored to $t=0$
