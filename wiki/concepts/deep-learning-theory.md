---
title: "Deep Learning Theory"
type: concept
tags:
  - deep-learning-theory
  - optimization
  - generalization
  - scientific-method
related:
  - "wiki/concepts/neural-scaling-laws.md"
  - "wiki/concepts/edge-of-stability.md"
  - "wiki/concepts/mechanistic-interpretability.md"
  - "wiki/concepts/spontaneous-symmetry-breaking.md"
  - "wiki/concepts/equivariant-networks.md"
  - "wiki/concepts/stochastic-thermodynamics.md"
  - "wiki/concepts/hyperball-optimizer.md"
  - "wiki/articles/edge-of-stability-cohen-talk.md"
  - "wiki/articles/kempe-llm-reasoning-insights.md"
sources:
  - "raw/iclr-2026-workshop-sci4dl/README.md"
  - "raw/learningmechanics-pub.md"
  - "raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/"
  - "raw/fantastic-pretraining-optimizers-weight-norm-theory.md"
---

# Deep Learning Theory

Deep learning theory seeks to explain why deep neural networks generalize well and how optimization landscapes enable training. The Sci4DL workshop at ICLR 2026 advocated for a scientific-method approach—forming hypotheses and testing them with controlled experiments—as a complement to mathematical proofs, which have so far been limited to oversimplified settings. Key topics include optimization dynamics (edge of stability, gradient descent behavior), generalization bounds, loss landscape geometry, and the role of data structure in learning.

## Key ideas

- The scientific method (hypothesis → experiment → revision) complements formal proofs for understanding deep learning
- Optimization dynamics such as the edge of stability reveal implicit regularization in gradient descent
- Generalization in overparameterized networks remains poorly explained by classical theory
- Data structure and representation learning are central to why deep networks outperform shallow ones

## Sources

- [Sci4DL Workshop (ICLR 2026)](../../raw/iclr-2026-workshop-sci4dl/README.md)
- [Learning Mechanics blog](../../raw/learningmechanics-pub.md) — research blog on deep learning theory

## Related concepts

- [Neural Scaling Laws](neural-scaling-laws.md)
- [Edge of Stability](edge-of-stability.md)
- [Mechanistic Interpretability](mechanistic-interpretability.md)
