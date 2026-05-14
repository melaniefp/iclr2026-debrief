---
title: "Sharpness-Aware Pretraining Mitigates Catastrophic Forgetting"
url: "https://openreview.net/forum?id=B2qTJi5s0M"
source: "openreview"
author: "Ishaan Watts, Catherine Li, Sachin Goyal, Jacob Mitchell Springer, Aditi Raghunathan"
date: "2026-04-23"
captured: "2026-05-13"
tags:
  - iclr-2026
  - openreview
  - pretraining
  - optimizers
  - llms
  - catastrophic-forgetting
related:
  - "wiki/papers/sharpness-pretraining.md"
---

# Sharpness-Aware Pretraining Mitigates Catastrophic Forgetting

**OpenReview:** [B2qTJi5s0M](https://openreview.net/forum?id=B2qTJi5s0M)
**Venue:** ICLR 2026 Workshop GRaM Poster

## Abstract

Standard optimizer choices for pre-training are designed to minimize pre-training loss. Yet pre-trained models are routinely subjected to further transformations—such as fine-tuning to acquire new capabilities or quantization for efficiency. In this work, we evaluate optimizer choices across model scales, token budgets, and datasets, and find that strategies that explicitly (Sharpness-Aware Minimization) or implicitly (large learning rates and Warmup–Stable–Decay schedules) reduce sharpness yield better downstream performance, even when they achieve comparable or worse pre-training loss. Combining these strategies yields a new pre-training recipe that substantially outperforms standard baselines with minimal compute overhead, delivering a better learning–forgetting frontier during fine-tuning and higher accuracy after quantization.

**TL;DR:** Downstream stability in language models depends on both pre-training loss and loss-landscape sharpness, with increased sharpness leading to greater catastrophic forgetting.

## Decision

**Decision:** Accept (Poster)

## Decision

**Decision:** Accept

## Review 1 (Reviewer_pZVs)

**Rating:** 6
**Confidence:** 3

## Review 2 (Reviewer_27gH)

**Rating:** 5
**Confidence:** 3

## Review 3 (Reviewer_XD9o)

**Rating:** 4
**Confidence:** 4