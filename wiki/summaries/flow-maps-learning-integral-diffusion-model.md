---
title: "Summary: Learning the integral of a diffusion model"
type: summary
tags:
  - diffusion-models
  - flow-maps
  - consistency-models
  - distillation
  - generative-models
  - flow-matching
related:
  - "wiki/concepts/flow-maps.md"
  - "wiki/concepts/knowledge-distillation.md"
sources:
  - "raw/flow-maps-learning-integral-diffusion-model.md"
---

# Summary: Learning the integral of a diffusion model

Sander Dieleman's comprehensive tutorial on **flow maps** — neural networks that directly predict the integral of a diffusion model's velocity field, enabling sampling in far fewer steps than standard diffusion.

## Key ideas

Flow maps generalize consistency models by predicting any point on a sampling path from any other point: $F(\mathbf{x}_s, s, t) = \mathbf{x}_t$. Unlike diffusion models that predict only the local tangent direction (velocity), flow maps provide a global characterization of entire trajectories. This enables single-step sampling by jumping directly from noise to data.

The post identifies **three consistency rules** that any valid flow map must satisfy, and shows how each can be turned into a training loss:

| Rule | Intuition | Emoji |
|------|-----------|-------|
| Compositionality | Two small jumps = one big jump | 🐶 |
| Lagrangian consistency | Moving the target: output changes as velocity | 🐱 |
| Eulerian consistency | Moving the source: output stays fixed | 🐔 |

Training flow maps involves practical challenges around **stop-gradient operations**, **higher-order derivatives**, and **EMA stabilization**. The post introduces two key parameterizations: the flow map $F$ (predicts target position) and the average velocity $V$ (predicts mean flow between source and target).

## Training approaches

1. **Distillation** (🧑‍🏫): Bootstrap from a pre-trained diffusion model's velocity predictions
2. **Self-distillation** (🪃): Combine consistency loss with a standard diffusion loss in a single model
3. **Marginal-from-conditional learning** (🌊): Train from scratch using the same marginalisation trick as standard diffusion (MeanFlow, improved MeanFlow)

## Landscape of methods

The post surveys 20+ methods with a detailed comparison table including: Consistency Models (CT/CD), Consistency Trajectory Models (CTM), MeanFlow/iMF, Terminal Velocity Matching (TVM), Shortcut Models, Align Your Flow (AYF), SoFlow, FreeFlow, Flow Map Matching (FMM), and more.

## Applications and extensions

- **Faster sampling at scale**: TVM applied to 10B+ parameter models; FACM used to distill Wan 2.2 video model
- **Reward-based steering**: Flow map trajectory tilting (FMTT) enables efficient differentiable look-ahead for reward optimization
- **Discrete data**: Categorical Flow Maps, Flow Map Language Models, and Discrete Flow Maps bring flow maps to language modeling via continuous embeddings
- **Alternative strategies**: Distributional distillation (DMD, IMM, ADD) relaxes trajectory preservation; Reflow straightens paths; FD-loss fine-tunes with Fréchet distance

## Connections to knowledge base

- Extends [knowledge distillation](../concepts/knowledge-distillation.md) to the generative modeling domain (distilling diffusion models into few-step generators)
- The [Discrete MMD paper](../papers/discrete-mmd-distilling-discrete-diffusion.md) is directly related — it distills discrete diffusion models, an approach the blog discusses as limited compared to continuous flow maps
- Flow maps relate to [on-policy distillation](../concepts/on-policy-distillation.md) conceptually: both are about transferring complex iterative behaviors into simpler models

## Source

- [raw/flow-maps-learning-integral-diffusion-model.md](../../raw/flow-maps-learning-integral-diffusion-model.md)
