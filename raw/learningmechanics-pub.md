---
title: "Learning Mechanics"
url: "https://learningmechanics.pub/"
source: "blog"
author: "Jeremy Cohen, Jamie Simon, and collaborators"
date: "2026-04-23"
captured: "2026-04-28"
tags:
  - deep-learning-theory
  - optimization
  - neural-scaling-laws
  - edge-of-stability
  - science-of-deep-learning
aliases:
  - "learningmechanics.pub"
related:
  - "wiki/concepts/deep-learning-theory.md"
  - "wiki/concepts/edge-of-stability.md"
  - "wiki/concepts/neural-scaling-laws.md"
  - "wiki/articles/edge-of-stability-cohen-talk.md"
  - "wiki/papers/there-will-be-a-scientific-theory-of-deep-learning.md"
  - "raw/iclr-2026-workshop-sci4dl/README.md"
---

# Learning Mechanics

[learningmechanics.pub](https://learningmechanics.pub/) is a blog publishing long-form posts on the theory and science of deep learning. It was announced by Jeremy Cohen at the end of his invited talk at the [Sci4DL workshop (ICLR 2026)](iclr-2026-workshop-sci4dl/README.md), alongside the paper "There Will Be a Scientific Theory of Deep Learning" (Simon, Kunin et al., 2025).

The site publishes in-depth, research-level blog posts aimed at building foundational understanding of how neural networks learn—emphasizing scientific methodology, toy models, and theoretical frameworks over algorithmic contributions.

## Posts (as of April 2026)

### Deep linear networks are a surprisingly useful toy model of weight-space dynamics

**URL**: [learningmechanics.pub/deep-linear-nets/](https://learningmechanics.pub/deep-linear-nets/)

A tutorial-style post on deep linear networks as toy models of training dynamics. Demonstrates that despite their functional linearity, deep linear networks exhibit four key phenomena of real neural network training:

1. **Preferential learning of certain directions first** — simplicity/spectral bias
2. **Convergence to good minima despite nonconvex landscapes** — all local minima are global
3. **Low-rank gradient updates** — instantaneous learning is low-rank
4. **Stepwise/staged learning** — plateaus punctuated by loss drops

The post walks through the mathematical setup (gradient flow on matrix factorization problems), derives exact solutions following Saxe et al. (2013), and connects the results to practical systems including `word2vec` and LoRA. Includes interactive visualizations of word embedding learning dynamics.

Key references: Saxe et al. (2013), Baldi & Hornik (1989), Karkada et al. (2025a), Dominé et al. (2025).

### On neural scaling and the quanta hypothesis

**Author**: Eric J. Michaud
**URL**: [learningmechanics.pub/quanta/](https://learningmechanics.pub/quanta/)

A deep exploration of neural scaling laws and what they tell us about the internal structure of neural networks. Revisits and refines the "quantization model of neural scaling" (Michaud, Liu, Girit, Tegmark, NeurIPS 2023), which proposes that:

- Networks learn discrete "quanta" — individual skills or mechanisms — that each emerge at characteristic scales
- Smooth power-law scaling emerges from the superposition of many such discrete transitions
- This reconciles the apparent tension between smooth aggregate scaling laws and sharp emergent abilities

Discusses connections to mechanistic interpretability, the structure of data distributions, approximation theory (Sharma & Kaplan, 2020), and the limits of interpretability. Includes discussions of emergent abilities (Wei et al., 2022), induction heads (Olsson et al., 2022), and grokking.

### Perspectives on the science of deep learning

**URL**: [learningmechanics.pub/perspectives/](https://learningmechanics.pub/perspectives/)

Three essays on building theory that matters:

1. **The scientific method in two steps** — Jamie Simon
2. **Towards an atlas of deep learning** — Dhruva Karkada
3. **Science plays the long game** — Florentin Guth

### Coming soon

- **A visual guide to progressive sharpening and the edge of stability**

## Context

The site represents a community effort to publish accessible, rigorous expositions of deep learning theory — bridging the gap between technical papers and broader understanding. It aligns with the philosophy Cohen articulated in his Sci4DL talk: that the field should invest in understanding foundations, with faith that true understanding will eventually yield practical gains.
