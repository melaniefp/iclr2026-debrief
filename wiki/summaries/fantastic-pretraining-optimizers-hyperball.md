---
title: "Summary: Fantastic Pretraining Optimizers 2.1 — Hyperball Optimization"
type: summary
tags:
  - optimization
  - weight-decay
  - hyperparameter-transfer
  - scaling-laws
  - language-models
related:
  - "wiki/concepts/hyperball-optimizer.md"
  - "wiki/concepts/neural-scaling-laws.md"
  - "wiki/concepts/marin-project.md"
  - "wiki/summaries/fantastic-pretraining-optimizers-weight-norm-theory.md"
sources:
  - "raw/fantastic-pretraining-optimizers-hyperball.md"
---

# Summary: Fantastic Pretraining Optimizers 2.1 — Hyperball Optimization

**Source:** [Fantastic Pretraining Optimizers 2.1: Hyperball Optimization](../../raw/fantastic-pretraining-optimizers-hyperball.md)

**TL;DR:** Hyperball is an optimizer wrapper that normalizes the Frobenius norm of both weights and updates for all matrices, replacing weight decay entirely and yielding 20–30% speedups with stable hyperparameter transfer across model scales.

## Key claims

The blog introduces the **Hyperball update rule**: $W_{t+1} = R \cdot \text{Normalize}(W_t - \eta R \cdot \text{Normalize}(u_t))$, where $R$ is the initial Frobenius norm and $u_t$ is the base optimizer's update. This constrains optimization to a hypersphere, decoupling weight scale from directional learning speed. Any base optimizer can be wrapped (Adam → AdamH, Muon → MuonH).

## Experimental results

| Setting | Result |
|---------|--------|
| 1.2B Qwen3, 1–8× Chinchilla | 20–30% speedup over AdamW (scaling-law fit) |
| Marin speedrun (FineWeb-Edu) | Persistent speedup at increasing scales; matches models with 10% more parameters |
| 8B scale (Marin Ferries) | 0.04 loss improvement over AdamW baseline |
| Depth transfer (L=4→512) | Optimal LR window drifts only 1.4× |
| Width transfer (d=128→2048) | Optimal LR window drifts only 1.4× |
| Overtraining stress test (130M) | Speedup maintained far beyond Chinchilla budget |

## Mechanism

The blog explains why Hyperball works through two insights: (1) RMSNorm's rescaling parameter $\gamma$ preserves representation power when weight norms are fixed, since $f(h; cW, \gamma/c) = f(h; W, \gamma)$; (2) weight decay implicitly couples weight scale with directional learning speed via an equilibrium norm, while Hyperball decouples these by giving direct control over directional update speed.

## Related methods survey

The blog provides a comprehensive survey of 15+ related methods across four categories: reparameterization/standardization (Weight Normalization, Weight Standardization, BiT), constraints in generative models (EDM2, Spectral Normalization), update constraints (AdamP, Rotation Equilibrium, LionAR), and fixed norms in LLM pretraining ([nGPT](https://arxiv.org/abs/2410.01131), [Nemotron-Flash](https://arxiv.org/abs/2511.18890), [anGPT](https://arxiv.org/abs/2505.22014), Target Variance Rescaling).

## Knowledge base connections

- Companion theory post: [Weight Norm Theory (Part 2.2)](fantastic-pretraining-optimizers-weight-norm-theory.md)
- Concept: [Hyperball Optimizer](../concepts/hyperball-optimizer.md)
- Paper summary: [Hyperball Optimization paper](../papers/hyperp-hypersphere-scaling.md)
- Related concept: [Neural Scaling Laws](../concepts/neural-scaling-laws.md) — hyperball enables reliable isoflop scaling
- Related concept: [Marin Project](../concepts/marin-project.md) — hyperball validated in Marin speedruns
