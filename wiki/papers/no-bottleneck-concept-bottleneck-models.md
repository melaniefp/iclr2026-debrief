---
title: "There Was Never a Bottleneck in Concept Bottleneck Models"
authors: "Antonio Almudévar, José Miguel Hernández-Lobato, Alfonso Ortega"
affiliations: "University of Zaragoza, University of Cambridge"
url: "https://openreview.net/forum?id=Fy7V5dalvX"
date: "2026-04-23"
category: "Interpretability"
raw_source: "raw/no-bottleneck-openreview.md"
keywords:
  - concept-bottleneck-models
  - interpretability
  - information-leakage
  - explainability
---

# There Was Never a Bottleneck in Concept Bottleneck Models

## Summary

TL;DR: Deep learning representations are often difficult to interpret, which can hinder their deployment in sensitive applications. Concept Bottleneck Models (CBMs) have emerged as a promising approach to mitigate this issue by learning representations that support target task performance while ensuring that each component predicts a concrete concept from a predefined set.

- **Problem**: Deep learning representations are often difficult to interpret, which can hinder their deployment in sensitive applications.
- **Approach**: This shortcoming raises concerns regarding interpretability and the validity of intervention procedures.
- **Results**: This IB is implemented via a variational regularization term added to the training loss.
- **Impact**: As a result, MCBMs yield more interpretable representations, support principled concept-level interventions, and remain consistent with probability-theoretic foundations..

## Abstract

Deep learning representations are often difficult to interpret, which can hinder their deployment in sensitive applications. Concept Bottleneck Models (CBMs) have emerged as a promising approach to mitigate this issue by learning representations that support target task performance while ensuring that each component predicts a concrete concept from a predefined set. In this work, we argue that CBMs do not impose a true bottleneck: the fact that a component can predict a concept does not guarantee that it encodes only information about that concept. This shortcoming raises concerns regarding interpretability and the validity of intervention procedures. To overcome this limitation, we propose Minimal Concept Bottleneck Models (MCBMs), which incorporate an Information Bottleneck (IB) objective to constrain each representation component to retain only the information relevant to its corresponding concept. This IB is implemented via a variational regularization term added to the training loss. As a result, MCBMs yield more interpretable representations, support principled concept-level interventions, and remain consistent with probability-theoretic foundations.

## Review Summary

**Decision:** Accept (Poster)

**Reviewer ratings:**
- Rating: 6
- Rating: 4
- Rating: 6
- Rating: 4

See [OpenReview discussion](https://openreview.net/forum?id=Fy7V5dalvX) for full reviews.

## Implementation Notes

- **OpenReview:** [Fy7V5dalvX](https://openreview.net/forum?id=Fy7V5dalvX)
- **Venue:** ICLR 2026 Poster
