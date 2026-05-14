---
title: "WRING Out the Bias: A Rotation-Based Alternative to Projection Debiasing"
authors: "Walter Gerych, Cassandra Parent, Quinn Perian, Rafiya Javed, Justin Solomon, Marzyeh Ghassemi"
affiliations: "WPI, MIT EECS, Google"
url: "https://openreview.net/forum?id=tkE29O0jzF"
date: "2026-04-23"
category: "Fairness & Bias"
raw_source: "raw/wring-bias-openreview.md"
keywords:
  - debiasing
  - word-embeddings
  - rotation-matrix
  - fairness
---

# WRING Out the Bias: A Rotation-Based Alternative to Projection Debiasing

## Summary

TL;DR: Vision-Language models (VLMs), including CLIP, are known to encode biases such as learning spurious correlations that falsely associate background attributes with particular labels. Debiasing approaches typically aim to isolate and remove subspaces corresponding to a target concept via projecting the embedding away from the concept.

- **Problem**: Vision-Language models (VLMs), including CLIP, are known to encode biases such as learning spurious correlations that falsely associate background attributes with particular labels.
- **Approach**: In practice, it is impossible to enumerate all possible biases, meaning that an increase in bias can go unobserved during evaluation.
- **Results**: We propose a debiasing approach for a set of known concepts such that the relation to the remaining, unconsidered, concepts is minimally changed.
- **Impact**: We achieve this by rotating the VLM's embeddings within only a relevant subspace, rather than removing these subspaces, which mitigates unintended bias amplification..

## Abstract

Vision-Language models (VLMs), including CLIP, are known to encode biases such as learning spurious correlations that falsely associate background attributes with particular labels. Debiasing approaches typically aim to isolate and remove subspaces corresponding to a target concept via projecting the embedding away from the concept. This strategy succeeds in debiasing VLM embeddings with respect to the concepts considered but can amplify biased shortcuts in unconsidered concepts. In practice, it is impossible to enumerate all possible biases, meaning that an increase in bias can go unobserved during evaluation. We propose a debiasing approach for a set of known concepts such that the relation to the remaining, unconsidered, concepts is minimally changed. We achieve this by rotating the VLM's embeddings within only a relevant subspace, rather than removing these subspaces, which mitigates unintended bias amplification.

## Review Summary

**Decision:** Accept (Poster)

**Reviewer ratings:**
- Rating: 6
- Rating: 4
- Rating: 6

See [OpenReview discussion](https://openreview.net/forum?id=tkE29O0jzF) for full reviews.

## Implementation Notes

- **OpenReview:** [tkE29O0jzF](https://openreview.net/forum?id=tkE29O0jzF)
- **Venue:** ICLR 2026 Poster
