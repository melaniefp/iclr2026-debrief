---
title: "Query Timing Produces Opposite Positional Biases Between LLMs and Humans"
authors: "Jasin Cekinmez, Addison J. Wu, Thomas L. Griffiths"
affiliations: "Princeton University"
url: "https://openreview.net/forum?id=IgMZ1qT7iR"
date: "2026-04-23"
category: "LLM Evaluation"
raw_source: "raw/query-timing-openreview.md"
keywords:
  - positional-bias
  - query-timing
  - human-AI-comparison
  - cognitive-science
---

# Query Timing Produces Opposite Positional Biases Between LLMs and Humans

## Summary

TL;DR: Positional biases such as recency and primacy effects have been documented in large language models (LLMs), yet the underlying mechanism by which these models make their evaluations remains poorly understood. Both $\textit{primacy}$ and $\textit{recency}$ biases have been observed in human judgments in response to evidence, but recent work suggest that $\textit{when}$ the listener updates their beliefs -- during the presentation of evidence or only at the end -- influences the presence of such effects.

- **Problem**: Positional biases such as recency and primacy effects have been documented in large language models (LLMs), yet the underlying mechanism by which these models make their evaluations remains poorly understood.
- **Approach**: We investigate whether a similar phenomenon holds for LLMs, finding divergence from human behavior across many models.
- **Results**: We investigate whether a similar phenomenon holds for LLMs, finding divergence from human behavior across many models.
- **Impact**: Furthermore, we find that such positional biases are more exacerbated in newer models compared to their predecessors, raising concerns about the reliability and robustness of LLM-based evaluations in settings where evidence order should be irrelevant..

## Abstract

Positional biases such as recency and primacy effects have been documented in large language models (LLMs), yet the underlying mechanism by which these models make their evaluations remains poorly understood. Both $\textit{primacy}$ and $\textit{recency}$ biases have been observed in human judgments in response to evidence, but recent work suggest that $\textit{when}$ the listener updates their beliefs -- during the presentation of evidence or only at the end -- influences the presence of such effects. We investigate whether a similar phenomenon holds for LLMs, finding divergence from human behavior across many models. Furthermore, we find that such positional biases are more exacerbated in newer models compared to their predecessors, raising concerns about the reliability and robustness of LLM-based evaluations in settings where evidence order should be irrelevant.


## Implementation Notes

- **OpenReview:** [IgMZ1qT7iR](https://openreview.net/forum?id=IgMZ1qT7iR)
- **Venue:** ICLR 2026 Workshop ICBINB
