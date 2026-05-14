---
title: "AdAEM: An Adaptively and Automated Extensible Measurement of LLMs' Value Difference"
authors: "Various"
affiliations: "Various"
url: "https://openreview.net/forum?id=qNlTH4kYJZ"
date: "2026-04-23"
category: "LLM Evaluation"
raw_source: "raw/adaem-openreview.md"
keywords:
  - value-alignment
  - cultural-adaptability
  - information-theory
  - LLM-values
---

# AdAEM: An Adaptively and Automated Extensible Measurement of LLMs' Value Difference

## Summary

TL;DR: This paper proposes aa novel dynamic and automated evaluation framework to probe LLMs' value orientations and value differences

- **Problem**: Assessing Large Language Models’ (LLMs) underlying value differences enables comprehensive comparison of their misalignment, cultural adaptability, and biases.
- **Approach**: This is achieved by probing the internal value boundaries of a diverse set of LLMs developed across cultures and time periods in an in-context optimization manner.
- **Results**: We use AdAEM to generate novel questions and conduct an extensive analysis, demonstrating our method’s validity and effectiveness, laying the groundwork for better interdisciplinary research on LLMs’ values and alignment.
- **Impact**: Codes and the generated evaluation questions are released at https://github.com/ValueCompass/AdAEM.

**TL;DR:** This paper proposes aa novel dynamic and automated evaluation framework to probe LLMs' value orientations and value differences.

## Abstract

Assessing Large Language Models’ (LLMs) underlying value differences enables comprehensive comparison of their misalignment, cultural adaptability, and biases. Nevertheless, current value measurement methods face the informativeness challenge: with often outdated, contaminated, or generic test questions, they can only capture the orientations on comment safety values, e.g., HHH, shared among different LLMs, leading to indistinguishable and uninformative results. To address this problem, we introduce AdAEM, a novel, self-extensible evaluation algorithm for revealing LLMs’ inclinations. Distinct from static benchmarks, AdAEM automatically and adaptively generates and extends its test questions. This is achieved by probing the internal value boundaries of a diverse set of LLMs developed across cultures and time periods in an in-context optimization manner. Such a process theoretically maximizes an information-theoretic objective to extract diverse controversial topics that can provide more distinguishable and informative insights about models’ value differences. In this way, AdAEM is able to co-evolve with the development of LLMs, consistently tracking their value dynamics. We use AdAEM to generate novel questions and conduct an extensive analysis, demonstrating our method’s validity and effectiveness, laying the groundwork for better interdisciplinary research on LLMs’ values and alignment. Codes and the generated evaluation questions are released at https://github.com/ValueCompass/AdAEM.

**TL;DR:** This paper proposes aa novel dynamic and automated evaluation framework to probe LLMs' value orientations and value differences

## Review Summary

**Decision:** Accept (Oral)

**Reviewer ratings:**
- Rating: 8
- Rating: 4
- Rating: 8
- Rating: 8

See [OpenReview discussion](https://openreview.net/forum?id=qNlTH4kYJZ) for full reviews.

## Implementation Notes

- **OpenReview:** [qNlTH4kYJZ](https://openreview.net/forum?id=qNlTH4kYJZ)
- **Venue:** ICLR 2026 Oral
