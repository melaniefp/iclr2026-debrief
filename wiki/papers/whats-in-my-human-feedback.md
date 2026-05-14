---
title: "What's In My Human Feedback? Learning Interpretable Descriptions of Preference Data"
authors: "Rajiv Movva, Smitha Milli, Sewon Min, Emma Pierson"
affiliations: "UC Berkeley, FAIR at Meta"
url: "https://openreview.net/forum?id=sC6A1bFDUt"
date: "2026-04-23"
category: "LLM Evaluation"
raw_source: "raw/wimhf-openreview.md"
keywords:
  - rlhf
  - interpretability
  - reward-modeling
  - preference-data
---

# What's In My Human Feedback? Learning Interpretable Descriptions of Preference Data

## Summary

TL;DR: We present WIMHF, a method to describe the preferences encoded by human feedback; produce insights from seven widely-used datasets; and show that the method enables new approaches to data curation and personalization.

- **Problem**: Human feedback can alter language models in unpredictable and undesirable ways, as practitioners lack a clear understanding of what feedback data encodes.
- **Approach**: These features reveal a wide diversity in what humans prefer, and the role of dataset-level context: for example, users on Reddit prefer informality and jokes, while annotators in HH-RLHF and PRISM disprefer them.
- **Results**: They also allow fine-grained *personalization*: on the Community Alignment dataset, we learn annotator-specific weights over subjective features that improve preference prediction.
- **Impact**: WIMHF provides a human-centered analysis method for practitioners to better understand and use preference data.

**TL;DR:** We present WIMHF, a method to describe the preferences encoded by human feedback; produce insights from seven widely-used datasets; and show that the method enables new approaches to data curation and personalization..

## Abstract

Human feedback can alter language models in unpredictable and undesirable ways, as practitioners lack a clear understanding of what feedback data encodes. While prior work studies preferences over certain attributes (e.g., length or sycophancy), automatically extracting relevant features without pre-specifying hypotheses remains challenging. We introduce *What's In My Human Feedback?* (WIMHF), a method to explain feedback data using sparse autoencoders. WIMHF characterizes both (1) the preferences a dataset is capable of measuring and (2) the preferences that the annotators actually express. Across 7 datasets, WIMHF identifies a small number of human-interpretable features that account for the majority of the preference prediction signal achieved by black-box models. These features reveal a wide diversity in what humans prefer, and the role of dataset-level context: for example, users on Reddit prefer informality and jokes, while annotators in HH-RLHF and PRISM disprefer them. WIMHF also surfaces potentially unsafe preferences, such as that LMArena users tend to vote against refusals, often in favor of toxic content. The learned features enable effective *data curation*: re-labeling the harmful examples in Arena yields large safety gains (+37%) with no cost to general performance. They also allow fine-grained *personalization*: on the Community Alignment dataset, we learn annotator-specific weights over subjective features that improve preference prediction. WIMHF provides a human-centered analysis method for practitioners to better understand and use preference data.

**TL;DR:** We present WIMHF, a method to describe the preferences encoded by human feedback; produce insights from seven widely-used datasets; and show that the method enables new approaches to data curation and personalization.

## Review Summary

**Decision:** Accept (Oral)

**Reviewer ratings:**
- Rating: 4
- Rating: 8
- Rating: 8
- Rating: 6

See [OpenReview discussion](https://openreview.net/forum?id=sC6A1bFDUt) for full reviews.

## Implementation Notes

- **OpenReview:** [sC6A1bFDUt](https://openreview.net/forum?id=sC6A1bFDUt)
- **Venue:** ICLR 2026 Oral
