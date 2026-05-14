---
title: "Edge of Stability"
type: concept
tags:
  - optimization
  - deep-learning-theory
  - gradient-descent
related:
  - "wiki/concepts/deep-learning-theory.md"
  - "wiki/articles/edge-of-stability-cohen-talk.md"
sources:
  - "raw/iclr-2026-workshop-sci4dl/README.md"
  - "raw/learningmechanics-pub.md"
---

# Edge of Stability

The edge of stability is a phenomenon in neural network training where the largest eigenvalue of the Hessian hovers near the stability threshold 2/η (where η is the learning rate). At Sci4DL (ICLR 2026), Jeremy Cohen's invited talk explored how gradient descent works, and Minhak Song presented a contributed talk on zeroth-order optimization at the edge of stability. This phenomenon suggests that gradient descent self-tunes to operate at the boundary of stability, which may explain its implicit regularization properties.

## Key ideas

- The sharpness (top Hessian eigenvalue) rises to 2/η during training, then oscillates near that threshold
- Gradient descent self-regulates to the boundary between stable and unstable optimization regimes
- This self-tuning behavior may underlie the implicit regularization that helps generalization
- Zeroth-order methods can exhibit analogous edge-of-stability dynamics

## Sources

- [Sci4DL Workshop (ICLR 2026)](../../raw/iclr-2026-workshop-sci4dl/README.md)
- [Learning Mechanics blog](../../raw/learningmechanics-pub.md) — forthcoming visual guide to progressive sharpening and the edge of stability

## Related concepts

- [Deep Learning Theory](deep-learning-theory.md)
