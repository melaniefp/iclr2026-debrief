---
title: "An Information-Theoretic Approach to Benign Leakage in Static Concept Embedding Models"
authors: "Tianchao Li, Shujian Yu, Robert Jenssen"
affiliations: "UiT Arctic University of Norway, VU Amsterdam, University of Copenhagen"
url: "https://openreview.net/forum?id=hY60e1tgJf"
date: "2026-04-23"
category: "Interpretability"
raw_source: "raw/info-theoretic-leakage-openreview.md"
keywords:
  - information-theory
  - concept-embeddings
  - leakage
  - concept-models
---

# An Information-Theoretic Approach to Benign Leakage in Static Concept Embedding Models

## Summary

TL;DR: Self-explanatory Concept Bottleneck Models (CBMs) integrate human-defined concepts into their internal representations to achieve interpretability, predictability, and intervenability. However, CBMs often suffer from concept leakage, where concept embeddings encode input information beyond the concept.

- **Problem**: Self-explanatory Concept Bottleneck Models (CBMs) integrate human-defined concepts into their internal representations to achieve interpretability, predictability, and intervenability.
- **Approach**: During the training forward process and test inference, static concept embeddings remain fixed, ensuring theoretical leakage resistance, a claim that is also empirically validated by our experiments.
- **Results**: We term this injection Benign Leakage, as it largely preserves CBM's properties while boosting performance.
- **Impact**: Our experimental results demonstrate that this approach matches or surpasses state-of-the-art methods..

## Abstract

Self-explanatory Concept Bottleneck Models (CBMs) integrate human-defined concepts into their internal representations to achieve interpretability, predictability, and intervenability. However, CBMs often suffer from concept leakage, where concept embeddings encode input information beyond the concept. Concept leakage undermines the core properties of CBMs as concept representations are dynamically extracted from inputs by the neural architecture, entangling with input-specific information, like end-to-end neural networks. To address this issue, we are the first to introduce vector quantization into CBMs for learning static concept embeddings under binary concept supervision, which we term Static Concept Embedding Models (StaticCEM). During the training forward process and test inference, static concept embeddings remain fixed, ensuring theoretical leakage resistance, a claim that is also empirically validated by our experiments. Moreover, since the input contains more substantial information than the human-defined concepts, predictions based solely on concepts may underperform compared to models that utilize the full input. To bridge the performance gap, we further inject controlled and limited input information into the leakage-resistant static embeddings via a dot-product projection, governed by the trade-off of a dual Information Bottleneck mechanism. We term this injection Benign Leakage, as it largely preserves CBM's properties while boosting performance. Our experimental results demonstrate that this approach matches or surpasses state-of-the-art methods.


## Implementation Notes

- **OpenReview:** [hY60e1tgJf](https://openreview.net/forum?id=hY60e1tgJf)
- **Venue:** UCRL@ICLR2026 Poster
