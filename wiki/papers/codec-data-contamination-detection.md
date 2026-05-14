---
title: "CoDeC: Detecting Data Contamination in LLMs via In-Context Learning"
authors: "Michał Zawalski, Meriem Boubdir, Klaudia Bałazy, Besmira Nushi, Pablo Ribalta"
affiliations: "NVIDIA"
url: "https://openreview.net/forum?id=YlpaaYxx4t"
date: "2026-04-23"
category: "LLM Evaluation"
raw_source: "raw/codec-openreview.md"
keywords:
  - data-contamination
  - benchmark-integrity
  - in-context-learning
  - LLM-evaluation
---

# CoDeC: Detecting Data Contamination in LLMs via In-Context Learning

## Summary

TL;DR: We propose Contamination Detection via Context (CoDeC), a simple, efficient, and model-agnostic method that detects training data contamination in LLMs by measuring how in‑context examples affect predictions.

- **Problem**: We present Contamination Detection via Context (CoDeC), a practical and accurate method to detect and quantify training data contamination in large language models.
- **Approach**: We find that in‑context examples typically boost confidence for unseen datasets but may reduce it when the dataset was part of training, due to disrupted memorization patterns.
- **Results**: Experiments show that CoDeC produces interpretable contamination scores that clearly separate seen and unseen datasets, and reveals strong evidence of memorization in open-weight models with undisclosed training corpora.
- **Impact**: The method is simple, automated, and both model- and dataset-agnostic, making it easy to integrate with benchmark evaluations.

**TL;DR:** We propose Contamination Detection via Context (CoDeC), a simple, efficient, and model-agnostic method that detects training data contamination in LLMs by measuring how in‑context examples affect predictions..

## Abstract

We present Contamination Detection via Context (CoDeC), a practical and accurate method to detect and quantify training data contamination in large language models. CoDeC distinguishes between data memorized during training and data outside the training distribution by measuring how in-context learning affects model performance. We find that in‑context examples typically boost confidence for unseen datasets but may reduce it when the dataset was part of training, due to disrupted memorization patterns. Experiments show that CoDeC produces interpretable contamination scores that clearly separate seen and unseen datasets, and reveals strong evidence of memorization in open-weight models with undisclosed training corpora. The method is simple, automated, and both model- and dataset-agnostic, making it easy to integrate with benchmark evaluations.

**TL;DR:** We propose Contamination Detection via Context (CoDeC), a simple, efficient, and model-agnostic method that detects training data contamination in LLMs by measuring how in‑context examples affect predictions.

## Review Summary

**Decision:** Accept (Poster)

**Reviewer ratings:**
- Rating: 6
- Rating: 4
- Rating: 6

See [OpenReview discussion](https://openreview.net/forum?id=YlpaaYxx4t) for full reviews.

## Implementation Notes

- **OpenReview:** [YlpaaYxx4t](https://openreview.net/forum?id=YlpaaYxx4t)
- **Venue:** ICLR 2026 Poster
