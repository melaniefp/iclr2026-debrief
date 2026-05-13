---
title: "Fantastic Pretraining Optimizers and Where to Find Them 2.1: Hyperball Optimization"
authors: "Kaiyue Wen, Xingyu Dang, Kaifeng Lyu, Tengyu Ma, Percy Liang"
affiliations: "Stanford University, Princeton University, Tsinghua University"
url: "https://tinyurl.com/muonh"
date: "2025-01-02"
category: "Optimization"
keywords:
  - scaling-laws
  - optimization
  - hyperparameter-transfer
  - language-models
  - weight-decay
related:
  - "wiki/concepts/hyperball-optimizer.md"
  - "wiki/concepts/neural-scaling-laws.md"
  - "wiki/concepts/marin-project.md"
  - "raw/fantastic-pretraining-optimizers-weight-norm-theory.md"
  - "raw/fantastic-pretraining-optimizers-hyperball.md"
  - "wiki/papers/hyperp-hypersphere-parameterization.md"
  - "wiki/papers/spectral-sphere-optimizer.md"
---

# Fantastic Pretraining Optimizers and Where to Find Them 2.1: Hyperball Optimization

## Summary

This paper introduces the **hyperball optimizer**, a meta-optimizer that keeps each weight matrix and its optimizer update at constant Frobenius norm through normalization/projection. By making weight-norm control explicit rather than relying on the implicit effect of weight decay, it eliminates the need for weight-decay tuning and enables substantially better hyperparameter transfer across model scales.

This is a follow-up to the original benchmarking study [arXiv:2509.02046](https://arxiv.org/abs/2509.02046) ("Fantastic Pretraining Optimizers and Where to Find Them"), which established that matrix-based optimizers (Muon, SOAP, Kron) outperform scalar ones but their advantages diminish at scale.

## Key contributions

1. **Hyperball meta-optimizer**: A principled approach that constrains each weight matrix to a fixed Frobenius norm. After each optimizer step, weights are projected back onto the hypersphere. This decouples update *direction* (controlled by the optimizer) from weight *scale* (controlled by the radius).

2. **Weight decay is redundant**: On the Frobenius sphere, standard decoupled weight decay has no first-order effect — the projection already controls the norm. This eliminates an entire hyperparameter from the search space.

3. **Improved hyperparameter transfer**: Unlike Adam/AdamW where optimal learning rates shift at each model scale, the hyperball optimizer produces consistent optima across model widths and depths. This enables simple functional scaling recipes.

4. **Persistent speedups**: 20–30% speedups over the Muon optimizer that do *not* diminish at larger scales — addressing the key finding from the original benchmarking study that optimizer gains shrink with scale.

5. **Weight norm theory**: A theoretical framework explaining why weight decay sets the effective step size in standard optimizers, and why explicit norm control via projection is more principled and transferable.

## Method

The approach constrains each weight matrix $W$ such that $\|W\|_F = r$ for a fixed radius $r$. After each optimizer step, weights are projected back onto the sphere:

$$W \leftarrow r \cdot \frac{W}{\|W\|_F}$$

This is combined with the Muon optimizer, which orthogonalizes gradients via matrix operations. The key insight is that on the sphere, the effective step size is determined purely by the angular displacement, making it independent of weight norm — hence transferable across scales.

## Relation to the original study

The original "Fantastic Pretraining Optimizers" paper (Wen, Hall, Ma, Liang, 2025) established that:
- Prior claims of 1.4–2× speedup over AdamW were inflated due to unfair tuning
- With rigorous hyperparameter sweeps, matrix-based optimizers give 1.4× at 0.1B but only 1.1× at 1.2B
- Comparing intermediate checkpoints can be misleading due to learning rate decay

The hyperball extension addresses the diminishing-gains problem by removing weight norm from the optimization landscape entirely, yielding speedups that persist at scale.

## Significance

This work connects to the [Marin project](../concepts/marin-project.md)'s scaling recipes — the [hyperball optimizer](../concepts/hyperball-optimizer.md) is a key enabler of 300× extrapolation of scaling laws from small experiments. It demonstrates that the right optimizer parameterization can make scaling predictable without expensive large-scale hyperparameter sweeps.

## Related blog posts

- [Part 2.1: Hyperball Optimization (raw capture)](../../raw/fantastic-pretraining-optimizers-hyperball.md) — Full blog post with experiments, mechanism, and related methods
- [Part 2.2: The Hitchhiker's Guide to the Weight Norm Theory](https://whenwen.github.io/wd_blog/public/weight-decay-part-2.html) ([raw capture](../../raw/fantastic-pretraining-optimizers-weight-norm-theory.md)) — Theoretical motivation for why weight decay controls effective step size
