---
title: "Model Collapse Is Not a Bug but a Feature in Machine Unlearning for LLMs"
authors: "Yan Scholten, Sophie Xhonneux, Leo Schwinn, Stephan Günnemann"
affiliations: "TU Munich, Mila, Université de Montréal"
url: "https://openreview.net/forum?id=1MCQzboBrR"
date: "2026-04-23"
category: "LLM Safety & Alignment"
raw_source: "raw/model-collapse-openreview.md"
keywords:
  - model-collapse
  - machine-unlearning
  - LLMs
  - data-poisoning
---

# Model Collapse Is Not a Bug but a Feature in Machine Unlearning for LLMs

## Summary

TL;DR: We show that model collapse can be intentionally triggered to make LLMs unlearn specific information, turning it into a practical method for machine unlearning.

- **Problem**: Current unlearning methods for LLMs optimize on the private information they seek to remove by incorporating it into their fine-tuning data.
- **Approach**: Our central insight is that model collapse can be leveraged for machine unlearning by deliberately triggering it for data we aim to remove.
- **Results**: We empirically demonstrate that PMC overcomes four key limitations of existing unlearning methods that explicitly optimize on unlearning targets, and more effectively removes private information from model outputs while preserving general model utility.
- **Impact**: Overall, our contributions represent an important step toward more comprehensive unlearning that better aligns with real-world privacy constraints.

**TL;DR:** We show that model collapse can be intentionally triggered to make LLMs unlearn specific information, turning it into a practical method for machine unlearning..

## Abstract

Current unlearning methods for LLMs optimize on the private information they seek to remove by incorporating it into their fine-tuning data. We argue this not only risks reinforcing exposure to sensitive data, but also fundamentally contradicts the principle of minimizing its use. As a remedy, we propose a novel unlearning method—Partial Model Collapse (PMC), which does not require unlearning targets in the unlearning objective. Our approach is inspired by recent observations that training generative models on their own generations leads to distribution collapse, effectively removing information from model outputs. Our central insight is that model collapse can be leveraged for machine unlearning by deliberately triggering it for data we aim to remove. We theoretically analyze that our approach converges to the desired outcome, i.e. the model unlearns the data targeted for removal. We empirically demonstrate that PMC overcomes four key limitations of existing unlearning methods that explicitly optimize on unlearning targets, and more effectively removes private information from model outputs while preserving general model utility. Overall, our contributions represent an important step toward more comprehensive unlearning that better aligns with real-world privacy constraints.

**TL;DR:** We show that model collapse can be intentionally triggered to make LLMs unlearn specific information, turning it into a practical method for machine unlearning.

## Review Summary

**Decision:** Accept (Poster)

**Reviewer ratings:**
- Rating: 6
- Rating: 6
- Rating: 4
- Rating: 4

See [OpenReview discussion](https://openreview.net/forum?id=1MCQzboBrR) for full reviews.

## Implementation Notes

- **OpenReview:** [1MCQzboBrR](https://openreview.net/forum?id=1MCQzboBrR)
- **Venue:** ICLR 2026 Poster
