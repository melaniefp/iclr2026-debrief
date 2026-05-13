---
title: "Consistency Models"
type: concept
tags:
  - diffusion-models
  - consistency-models
  - distillation
  - generative-models
  - few-step-sampling
related:
  - "wiki/concepts/flow-maps.md"
  - "wiki/concepts/knowledge-distillation.md"
sources:
  - "raw/flow-maps-learning-integral-diffusion-model.md"
---

# Consistency Models

Consistency models are a special case of [flow maps](flow-maps.md) where the target time step is anchored to $t=0$ (the data side). Given any noisy input $\mathbf{x}_t$, a consistency model predicts the clean output $F(\mathbf{x}_t, t, 0) = \mathbf{x}_0$ directly, enabling single-step sampling from diffusion models.

## Key ideas

- **Self-consistency property**: All points on the same sampling trajectory must map to the same clean output — $F(\mathbf{x}_s, s, 0) = F(\mathbf{x}_t, t, 0)$ for any $s, t$ on the same path
- **Consistency Distillation (CD)**: Trains a student using a pre-trained teacher model; propagates predictions from small time steps (near data) to large time steps (near noise) via the Eulerian consistency rule
- **Consistency Training (CT)**: Enables from-scratch learning by substituting the marginal velocity with the conditional velocity $\varepsilon - \mathbf{x}_0$; introduces bias that vanishes as step size $\Delta s \to 0$
- **Multi-step sampling**: Because every step fully denoises to $\mathbf{x}_0$, multi-step sampling requires reinjecting noise between steps (unlike full flow maps which can jump between arbitrary noise levels)
- **Anchored target**: The restriction to $t=0$ means consistency models learn a partial flow map — they cannot jump between intermediate noise levels without the reinject-noise workaround

## Evolution of the method

| Method | Year | Key advance |
|--------|------|-------------|
| Consistency Models (CM) | 2023 | Original formulation (Song et al.) |
| Improved CT (iCT) | 2024 | Better training recipe, pseudo-Huber loss |
| Easy Consistency Tuning (ECT) | 2025 | Simplified tuning procedure |
| Continuous-time CM (sCM) | 2025 | Stabilized continuous-time training |
| Consistency Trajectory Models (CTM) | 2024 | Generalized to two-time flow maps ($t > 0$) |
| LCM-LoRA | 2023 | LoRA modules converting Stable Diffusion into consistency models |

## Relation to flow maps

Consistency models are the $t=0$ slice of the full flow map $F(\mathbf{x}_s, s, t)$. The Consistency Distillation loss is recovered from the Eulerian consistency rule in the limit of infinitesimal step sizes. Consistency Trajectory Models (CTM) were the first to generalize beyond the $t=0$ anchor to learn full two-time flow maps.

## Sources

- [Learning the integral of a diffusion model](../../raw/flow-maps-learning-integral-diffusion-model.md) — Positions consistency models within the flow map framework; details CT, CD, iCT, ECT, sCM, CTM

## Related concepts

- [Flow Maps](flow-maps.md) — Consistency models are a special case (partial flow map)
- [Knowledge Distillation](knowledge-distillation.md) — CD is a form of distillation from a diffusion teacher
