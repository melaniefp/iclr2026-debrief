---
title: "Retain and Adapt: Auto-Balanced Model Editing for Open-Vocabulary Object Detection under Domain Shifts"
authors: "Zixuan Duan, Fengyuan Lu, Xunzhi Xiang, Wenbin Li, Yang Gao, Qi Fan"
affiliations: "Unknown"
url: "https://openreview.net/forum?id=4fOGZWupMM"
date: "2026-04-23"
category: "Computer Vision"
raw_source: "raw/retain-adapt-openreview.md"
keywords:
  - model-editing
  - object-detection
  - domain-adaptation
  - open-vocabulary
---

# Retain and Adapt: Auto-Balanced Model Editing for Open-Vocabulary Object Detection under Domain Shifts

## Summary

TL;DR: We propose a hyperparameter-free auto-balanced model editing method that flexibly injects and learns new task knowledge into open-vocabulary detectors while preserving original capabilities, achieving strong adaptation without retraining.

- **Problem**: Recent advances in Open Vocabulary Object Detection (OVOD) have shown strong performance on standard benchmarks, but performance drops sharply under out-of-distribution (OOD) shifts.
- **Approach**: Building on this insight, we introduce $\textbf{A}$utomatically $\textbf{B}$alanced $\textbf{M}$odel $\textbf{E}$diting ($\textbf{ABME}$), which injects new task knowledge into the powerful OVOD models while preserving the model’s original abilities.
- **Results**: Then we leverage the stored KV matrices to automatically balance the new and old knowledge for varying learning scenarios, 
supporting order-agnostic task insertion or removal without additional retraining.
- **Impact**: Experiments show that ABME consistently achieves a better trade-off between maintaining pre-trained performance and adapting to diverse OOD tasks compared to existing continual learning approaches for open-vocabulary object detection, and generalizes seamlessly across different models and task scales.

**TL;DR:** We propose a hyperparameter-free auto-balanced model editing method that flexibly injects and learns new task knowledge into open-vocabulary detectors while preserving original capabilities, achieving strong adaptation without retraining..

## Abstract

Recent advances in Open Vocabulary Object Detection (OVOD) have shown strong performance on standard benchmarks, but performance drops sharply under out-of-distribution (OOD) shifts. Continual learning offers a potential remedy by sequentially integrating new tasks, yet existing methods often struggle to balance retaining the pre-trained model capabilities with adapting to new tasks, and usually require retraining under specific task orders. To address these limitations, we observe that model editing naturally lends itself to this setting, as it enables efficient knowledge injection while retaining prior capabilities. Building on this insight, we introduce $\textbf{A}$utomatically $\textbf{B}$alanced $\textbf{M}$odel $\textbf{E}$diting ($\textbf{ABME}$), which injects new task knowledge into the powerful OVOD models while preserving the model’s original abilities. We first stores compact key–value representations with storage cost independent of task volume. Then we leverage the stored KV matrices to automatically balance the new and old knowledge for varying learning scenarios, 
supporting order-agnostic task insertion or removal without additional retraining. Experiments show that ABME consistently achieves a better trade-off between maintaining pre-trained performance and adapting to diverse OOD tasks compared to existing continual learning approaches for open-vocabulary object detection, and generalizes seamlessly across different models and task scales.

**TL;DR:** We propose a hyperparameter-free auto-balanced model editing method that flexibly injects and learns new task knowledge into open-vocabulary detectors while preserving original capabilities, achieving strong adaptation without retraining.

## Review Summary

**Decision:** Accept (Poster)

**Reviewer ratings:**
- Rating: 6
- Rating: 8
- Rating: 6
- Rating: 4

See [OpenReview discussion](https://openreview.net/forum?id=4fOGZWupMM) for full reviews.

## Implementation Notes

- **OpenReview:** [4fOGZWupMM](https://openreview.net/forum?id=4fOGZWupMM)
- **Venue:** ICLR 2026 Poster
