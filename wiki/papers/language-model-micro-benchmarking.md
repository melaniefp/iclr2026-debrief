---
title: "How Reliable is Language Model Micro-Benchmarking?"
authors: "Various"
affiliations: "Various"
url: "https://openreview.net/forum?id=cReExMQLiK"
date: "2026-04-23"
category: "LLM Evaluation"
raw_source: "raw/micro-bench-openreview.md"
keywords:
  - micro-benchmarking
  - evaluation-methodology
  - model-ranking
  - benchmark-design
---

# How Reliable is Language Model Micro-Benchmarking?

## Summary

TL;DR: Micro-benchmarking offers a solution to the often prohibitive time and cost of language model development: evaluate on a very small subset of existing benchmarks. Can these micro-benchmarks, however, rank models as consistently as the full benchmarks they replace? And can they rank models more consistently than selecting a random subset of data points? In many scenarios, we find that the answer is no.

- **Problem**: Micro-benchmarking offers a solution to the often prohibitive time and cost of language model development: evaluate on a very small subset of existing benchmarks.
- **Approach**: This approach can determine which model pairs can be ranked correctly by a micro-benchmark, allowing for a finer-grained analysis of the trade-off between micro-benchmark size and reliability.
Prior work has suggested selecting as few as 10 examples; we find that no micro-benchmarking method can consistently rank model pairs 3.5 points of accuracy apart on MMLU-Pro or 4 points apart on BIG-bench Hard.
- **Results**: When comparing only 8B instruction-tuned models on MMLU-Pro micro-benchmarks with 25 examples, we find that more than half of pairwise comparisons are not likely to be preserved.
- **Impact**: Our work provides actionable guidance for both micro-benchmark users and developers in navigating the trade-off between evaluation efficiency and reliability..

## Abstract

Micro-benchmarking offers a solution to the often prohibitive time and cost of language model development: evaluate on a very small subset of existing benchmarks. Can these micro-benchmarks, however, rank models as consistently as the full benchmarks they replace? And can they rank models more consistently than selecting a random subset of data points? In many scenarios, we find that the answer is no. We introduce a meta-evaluation measure for micro-benchmarking which investigates how well a micro-benchmark can rank two models as a function of their performance difference on the full benchmark. This approach can determine which model pairs can be ranked correctly by a micro-benchmark, allowing for a finer-grained analysis of the trade-off between micro-benchmark size and reliability.
Prior work has suggested selecting as few as 10 examples; we find that no micro-benchmarking method can consistently rank model pairs 3.5 points of accuracy apart on MMLU-Pro or 4 points apart on BIG-bench Hard. In order to consistently rank model pairs with relatively similar performances, we show that often as many as 250 examples must be selected, at which point random sampling is competitive with existing micro-benchmarking methods. When comparing only 8B instruction-tuned models on MMLU-Pro micro-benchmarks with 25 examples, we find that more than half of pairwise comparisons are not likely to be preserved. Our work provides actionable guidance for both micro-benchmark users and developers in navigating the trade-off between evaluation efficiency and reliability.

## Review Summary

**Decision:** Accept (Oral)

**Reviewer ratings:**
- Rating: 4
- Rating: 8
- Rating: 8
- Rating: 6

See [OpenReview discussion](https://openreview.net/forum?id=cReExMQLiK) for full reviews.

## Implementation Notes

- **OpenReview:** [cReExMQLiK](https://openreview.net/forum?id=cReExMQLiK)
- **Venue:** ICLR 2026 Oral
