---
title: "Summary: Weight Norm Theory (Fantastic Optimizers 2.2)"
type: summary
tags:
  - optimization
  - weight-decay
  - hyperparameter-transfer
  - deep-learning-theory
related:
  - "wiki/concepts/hyperball-optimizer.md"
  - "wiki/concepts/neural-scaling-laws.md"
  - "wiki/concepts/deep-learning-theory.md"
  - "wiki/summaries/fantastic-pretraining-optimizers-hyperball.md"
sources:
  - "raw/fantastic-pretraining-optimizers-weight-norm-theory.md"
---

# Summary: The Hitchhiker's Guide to the Weight Norm Theory

**TL;DR:** For scale-invariant models like Transformers, weight decay does not control capacity — it controls the *effective step size*, and this insight motivates the [hyperball optimizer](../concepts/hyperball-optimizer.md).

## Key claims

The blog post (Part 2.2 of the "Fantastic Pretraining Optimizers" series) provides closed-form derivations showing that in the noise-dominated training regime, three quantities reach stable equilibria determined solely by optimizer hyperparameters ($\eta$, $\lambda$, $\beta_1$) and layer geometry:

1. **Update norm is constant**: For both AdamW ($\sqrt{\frac{1-\beta_1}{1+\beta_1}}\sqrt{d_\text{in} d_\text{out}}$) and Muon ($\sqrt{d_\text{out}}$), the base optimizer update norm stabilizes quickly and remains time-independent.

2. **Weight–update correlation is stable**: Momentum creates a fixed negative correlation between the current update and the accumulated weights: $\langle W_t, u_t \rangle \approx -\frac{\eta\beta_1}{1-\alpha\beta_1} \|u_t\|_F^2$.

3. **Effective step size = $\sqrt{2\eta\lambda}$ (up to constants)**: The equilibrium weight norm and effective angular step size on the unit sphere depend on the *product* $\eta\lambda$, not on $\eta$ or $\lambda$ individually.

## Empirical phenomena explained

The theory predicts five phenomena observed in real LLM training runs:

| Phenomenon | Explanation |
|-----------|-------------|
| Weight norm tracks LR warmup/decay | Equilibrium norm $\propto \sqrt{\eta/\lambda}$ |
| Gradient norm increases late in training | Scale invariance: $\|G\| \propto 1/\|W\| \propto \sqrt{\lambda/\eta}$ |
| Fixed $\eta\lambda$ → same final loss | Effective step size depends only on $\eta\lambda$ |
| Weight decay gives higher early loss but lower final loss | Larger effective step size → faster river progress in river valley landscape |
| HP transfer depends on WD scaling, not init scale | Equilibrium doesn't depend on initialization |

## Connections to the knowledge base

- **[Hyperball optimizer](../concepts/hyperball-optimizer.md)**: This theory is the direct motivation — if weight decay just controls norm, why not control norm explicitly via projection?
- **[Neural scaling laws](../concepts/neural-scaling-laws.md)**: The effective step size formula explains why scaling recipes need to jointly tune $\eta$ and $\lambda$
- **[Deep learning theory](../concepts/deep-learning-theory.md)**: Builds on the intrinsic learning rate framework (Li, Lyu, Arora, 2020) and connects to the river valley landscape conjecture (Wen et al., 2024)

## Source

- [Full blog post](../../raw/fantastic-pretraining-optimizers-weight-norm-theory.md) — includes complete derivations, interactive demos, and 32 references
