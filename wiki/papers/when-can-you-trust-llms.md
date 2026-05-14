---
title: "When Can You TRUST Large Language Models?"
authors: "Radu Paradovschi, Darvin Yi, Andrew Rabinovich, Zhao Chen"
affiliations: "Upwork"
url: "https://openreview.net/forum?id=Q6OIA4KIGT"
date: "2026-04-23"
category: "LLM Evaluation"
raw_source: "raw/trust-llms-openreview.md"
keywords:
  - trust
  - LLM-reliability
  - uncertainty-estimation
  - calibration
---

# When Can You TRUST Large Language Models?

## Summary

TL;DR: Quantifying neural network model uncertainty is a difficult problem that has far-reaching implications on our ability to improve model reliability. Uncertainty quantification is especially difficult in the context of LLMs and autoregressive models, as standard methods for uncertainty measurement that apply to single outputs often fail to capture the semantic complexity of the entire autoregressive output.

- **Problem**: Quantifying neural network model uncertainty is a difficult problem that has far-reaching implications on our ability to improve model reliability.
- **Approach**: TRUST scores take advantage of the natural semantic branching of LLM outputs for nonzero temperatures, and calculate uncertainty based on semantic similarity of multiple output rollouts for an LLM model.
- **Results**: We show that TRUST outperforms industry standard uncertainty methods within complex multi-token language tasks like predicting math problem difficulty, and also can be distilled into efficient forward-pass models for easy inference.
- **Impact**: Crucially, TRUST scores can be calculated with nothing more than standard LLM calls and require zero white-box access to model internals..

## Abstract

Quantifying neural network model uncertainty is a difficult problem that has far-reaching implications on our ability to improve model reliability. Uncertainty quantification is especially difficult in the context of LLMs and autoregressive models, as standard methods for uncertainty measurement that apply to single outputs often fail to capture the semantic complexity of the entire autoregressive output. To remedy this gap, we introduce TRUST (Temperature-Related Unambiguity via Similarity Tracking) scores, a novel approach for quantifying LLM uncertainty which reasons about uncertainty $\textit{across the entire model output}$ rather than being limited to a small number of subsequent tokens. TRUST scores take advantage of the natural semantic branching of LLM outputs for nonzero temperatures, and calculate uncertainty based on semantic similarity of multiple output rollouts for an LLM model. We show that TRUST outperforms industry standard uncertainty methods within complex multi-token language tasks like predicting math problem difficulty, and also can be distilled into efficient forward-pass models for easy inference. Crucially, TRUST scores can be calculated with nothing more than standard LLM calls and require zero white-box access to model internals.

## Review Summary

**Decision:** Reject

**Reviewer ratings:**
- Rating: 2
- Rating: 2
- Rating: 4
- Rating: 2

See [OpenReview discussion](https://openreview.net/forum?id=Q6OIA4KIGT) for full reviews.

## Implementation Notes

- **OpenReview:** [Q6OIA4KIGT](https://openreview.net/forum?id=Q6OIA4KIGT)
- **Venue:** Submitted to ICLR 2026
