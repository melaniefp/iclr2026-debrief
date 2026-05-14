---
title: "The Anatomy of Uncertainty in LLMs"
url: "https://openreview.net/forum?id=0GYclsjLUb"
source: "openreview"
author: "Aditya Taparia, Ransalu Senanayake, Kowshik Thopalli, Vivek Narayanaswamy"
date: "2026-04-23"
captured: "2026-05-13"
tags:
  - iclr-2026
  - openreview
  - large-language-models
  - uncertainty
  - foundational-models
related:
  - "wiki/papers/anatomy-uncertainty.md"
---

# The Anatomy of Uncertainty in LLMs

**OpenReview:** [0GYclsjLUb](https://openreview.net/forum?id=0GYclsjLUb)
**Venue:** ICLR 2026 Workshop ICBINB

## Abstract

Understanding why a large language model (LLM) is uncertain about the response is important for their reliable deployment. Current approaches, which either provide a single uncertainty score or rely on the classical aleatoric-epistemic dichotomy, fail to offer actionable insights for improving the generative model. Recent studies have also shown that such methods are not enough for understanding uncertainty in LLMs. In this work, we advocate for an uncertainty decomposition framework that dissects LLM uncertainty into three distinct semantic components: (i) input ambiguity, arising from ambiguous prompts; (ii) knowledge gaps, caused by insufficient parametric  evidence; and (iii) decoding randomness, stemming from stochastic sampling. Through a series of experiments we demonstrate that the dominance of these components can shift across model size and task. Our framework provides a better understanding to audit LLM reliability and detect hallucinations, paving the way for targeted interventions and more trustworthy systems.

**TL;DR:** A framework for decomposing uncertainty in LLMs.