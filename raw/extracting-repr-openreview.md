---
title: "Extracting Representations in LLMs Robust to Distribution Shifts"
url: "https://openreview.net/forum?id=KzH1cLVU1R"
source: "openreview"
author: "Sweta Karlekar, Claudia Shi, Aahlad Manas Puli, Carolina Zheng, Maggie Makar et al."
date: "2026-04-23"
captured: "2026-05-13"
tags:
  - iclr-2026
  - openreview
  - mechanistic-interpretability
  - concept-extraction
  - large-language-models
  - transformers
  - representation-learning
related:
  - "wiki/papers/extracting-repr.md"
---

# Extracting Representations in LLMs Robust to Distribution Shifts

**OpenReview:** [KzH1cLVU1R](https://openreview.net/forum?id=KzH1cLVU1R)
**Venue:** UCRL@ICLR2026 Poster

## Abstract

Transformer-based large language models (LLMs) encode many high-level concepts as linear directions in the latent activation space.
Isolating such concept directions enables both the measurement of said concepts and interventions to modify them. 
Directions extracted from one dataset, however, often fail to generalize to new contexts or environments. 
We introduce Context-Aided Representation Extraction (CARE), a method that decomposes concept representations into two complementary components: (1) an invariant direction capturing shared aspects of the concept across environments, and (2) environment-specific directions capturing contextual variations.
We evaluate CARE on subject-verb agreement and harmful prompt detection across datasets with varying degrees of induced correlation between concept labels and environmental attributes. Our results demonstrate that CARE achieves robust performance on both measurement and intervention under distribution shift. 
A fitted CARE model reveals whether concepts admit unified representations or require multiple directions to fully capture their structure.
With this, CARE provides insight into the complexity of how concepts are encoded in language models and provides measurement and intervention strategies that are robust to distribution shift.

**TL;DR:** CARE extracts true behavior representations from LLMs by separating them from dataset artifacts and context effects, enabling more robust behavior prediction, removal, and editing.