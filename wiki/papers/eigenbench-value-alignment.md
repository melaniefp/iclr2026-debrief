---
title: "EigenBench: A Comparative Behavioral Measure of Value Alignment"
authors: "Various"
affiliations: "Various"
url: "https://openreview.net/forum?id=fm79KXJIUQ"
date: "2026-04-23"
category: "LLM Evaluation"
raw_source: "raw/eigenbench-openreview.md"
keywords:
  - value-alignment
  - eigentrust
  - benchmark
  - behavioral-evaluation
---

# EigenBench: A Comparative Behavioral Measure of Value Alignment

## Summary

TL;DR: Aligning AI with human values is a pressing unsolved problem. To address the lack of quantitative metrics for value alignment, we propose EigenBench: a black-box method for comparatively benchmarking language models’ values.

- **Problem**: Aligning AI with human values is a pressing unsolved problem.
- **Approach**: EigenBench uses no ground truth labels, as it is designed to quantify subjective traits for which reasonable judges may disagree on the correct label.
- **Results**: We further demonstrate that EigenBench can recover model rankings on the GPQA benchmark without access to objective labels, supporting its viability as a framework for evaluating subjective values for which no ground truths exist.
- **Impact**: The code is available at https://github.com/jchang153/EigenBench..

## Abstract

Aligning AI with human values is a pressing unsolved problem. To address the lack of quantitative metrics for value alignment, we propose EigenBench: a black-box method for comparatively benchmarking language models’ values. Given an ensemble of models, a constitution describing a value system, and a dataset of scenarios, our method returns a vector of scores quantifying each model’s alignment to the given constitution. To produce these scores, each model judges the outputs of other models across many scenarios, and these judgments are aggregated with EigenTrust (Kamvar et al., 2003), yielding scores that reflect a weighted consensus judgment of the whole ensemble. EigenBench uses no ground truth labels, as it is designed to quantify subjective traits for which reasonable judges may disagree on the correct label. Hence, to validate our method, we collect human judgments on the same ensemble of models and show that EigenBench’s judgments align closely with those of human evaluators. We further demonstrate that EigenBench can recover model rankings on the GPQA benchmark without access to objective labels, supporting its viability as a framework for evaluating subjective values for which no ground truths exist. The code is available at https://github.com/jchang153/EigenBench.

## Review Summary

**Decision:** Accept (Oral)

**Reviewer ratings:**
- Rating: 6
- Rating: 10
- Rating: 4
- Rating: 4

See [OpenReview discussion](https://openreview.net/forum?id=fm79KXJIUQ) for full reviews.

## Implementation Notes

- **OpenReview:** [fm79KXJIUQ](https://openreview.net/forum?id=fm79KXJIUQ)
- **Venue:** ICLR 2026 Oral
