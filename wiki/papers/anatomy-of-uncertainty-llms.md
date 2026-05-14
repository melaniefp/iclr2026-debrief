---
title: "The Anatomy of Uncertainty in LLMs"
authors: "Aditya Taparia, Ransalu Senanayake, Kowshik Thopalli, Vivek Narayanaswamy"
affiliations: "Arizona State University, Lawrence Livermore National Laboratory"
url: "https://openreview.net/forum?id=0GYclsjLUb"
date: "2026-04-23"
category: "LLM Evaluation"
raw_source: "raw/anatomy-uncertainty-openreview.md"
keywords:
  - uncertainty-quantification
  - LLMs
  - epistemic-uncertainty
  - aleatoric-uncertainty
---

# The Anatomy of Uncertainty in LLMs

## Summary

TL;DR: A framework for decomposing uncertainty in LLMs.

- **Problem**: Understanding why a large language model (LLM) is uncertain about the response is important for their reliable deployment.
- **Approach**: In this work, we advocate for an uncertainty decomposition framework that dissects LLM uncertainty into three distinct semantic components: (i) input ambiguity, arising from ambiguous prompts; (ii) knowledge gaps, caused by insufficient parametric  evidence; and (iii) decoding randomness, stemming from stochastic sampling.
- **Results**: Through a series of experiments we demonstrate that the dominance of these components can shift across model size and task.
- **Impact**: Our framework provides a better understanding to audit LLM reliability and detect hallucinations, paving the way for targeted interventions and more trustworthy systems.

**TL;DR:** A framework for decomposing uncertainty in LLMs..

## Abstract

Understanding why a large language model (LLM) is uncertain about the response is important for their reliable deployment. Current approaches, which either provide a single uncertainty score or rely on the classical aleatoric-epistemic dichotomy, fail to offer actionable insights for improving the generative model. Recent studies have also shown that such methods are not enough for understanding uncertainty in LLMs. In this work, we advocate for an uncertainty decomposition framework that dissects LLM uncertainty into three distinct semantic components: (i) input ambiguity, arising from ambiguous prompts; (ii) knowledge gaps, caused by insufficient parametric  evidence; and (iii) decoding randomness, stemming from stochastic sampling. Through a series of experiments we demonstrate that the dominance of these components can shift across model size and task. Our framework provides a better understanding to audit LLM reliability and detect hallucinations, paving the way for targeted interventions and more trustworthy systems.

**TL;DR:** A framework for decomposing uncertainty in LLMs.


## Implementation Notes

- **OpenReview:** [0GYclsjLUb](https://openreview.net/forum?id=0GYclsjLUb)
- **Venue:** ICLR 2026 Workshop ICBINB
