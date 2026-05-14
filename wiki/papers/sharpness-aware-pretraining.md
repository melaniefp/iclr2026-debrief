---
title: "Sharpness-Aware Pretraining Mitigates Catastrophic Forgetting"
authors: "Ishaan Watts, Catherine Li, Sachin Goyal, Jacob Mitchell Springer, Aditi Raghunathan"
affiliations: "Carnegie Mellon University"
url: "https://openreview.net/forum?id=B2qTJi5s0M"
date: "2026-04-23"
category: "Optimization"
raw_source: "raw/sharpness-pretraining-openreview.md"
keywords:
  - sharpness-aware-minimization
  - catastrophic-forgetting
  - pretraining
  - continual-learning
---

# Sharpness-Aware Pretraining Mitigates Catastrophic Forgetting

## Summary

TL;DR: Downstream stability in language models depends on both pre-training loss and loss-landscape sharpness, with increased sharpness leading to greater catastrophic forgetting.

- **Problem**: Standard optimizer choices for pre-training are designed to minimize pre-training loss.
- **Approach**: In this work, we evaluate optimizer choices across model scales, token budgets, and datasets, and find that strategies that explicitly (Sharpness-Aware Minimization) or implicitly (large learning rates and Warmup–Stable–Decay schedules) reduce sharpness yield better downstream performance, even when they achieve comparable or worse pre-training loss.
- **Results**: In this work, we evaluate optimizer choices across model scales, token budgets, and datasets, and find that strategies that explicitly (Sharpness-Aware Minimization) or implicitly (large learning rates and Warmup–Stable–Decay schedules) reduce sharpness yield better downstream performance, even when they achieve comparable or worse pre-training loss.
- **Impact**: Combining these strategies yields a new pre-training recipe that substantially outperforms standard baselines with minimal compute overhead, delivering a better learning–forgetting frontier during fine-tuning and higher accuracy after quantization.

**TL;DR:** Downstream stability in language models depends on both pre-training loss and loss-landscape sharpness, with increased sharpness leading to greater catastrophic forgetting..

## Abstract

Standard optimizer choices for pre-training are designed to minimize pre-training loss. Yet pre-trained models are routinely subjected to further transformations—such as fine-tuning to acquire new capabilities or quantization for efficiency. In this work, we evaluate optimizer choices across model scales, token budgets, and datasets, and find that strategies that explicitly (Sharpness-Aware Minimization) or implicitly (large learning rates and Warmup–Stable–Decay schedules) reduce sharpness yield better downstream performance, even when they achieve comparable or worse pre-training loss. Combining these strategies yields a new pre-training recipe that substantially outperforms standard baselines with minimal compute overhead, delivering a better learning–forgetting frontier during fine-tuning and higher accuracy after quantization.

**TL;DR:** Downstream stability in language models depends on both pre-training loss and loss-landscape sharpness, with increased sharpness leading to greater catastrophic forgetting.

## Review Summary

**Decision:** Accept (Poster)

**Reviewer ratings:**
- Rating: 6
- Rating: 5
- Rating: 4

See [OpenReview discussion](https://openreview.net/forum?id=B2qTJi5s0M) for full reviews.

## Implementation Notes

- **OpenReview:** [B2qTJi5s0M](https://openreview.net/forum?id=B2qTJi5s0M)
- **Venue:** ICLR 2026 Workshop GRaM Poster
