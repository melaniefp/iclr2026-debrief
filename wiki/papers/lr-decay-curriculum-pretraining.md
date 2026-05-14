---
title: "How LR Decay Wastes Your Best Data in Curriculum-Based LLM Pretraining"
authors: "Kairong Luo, Zhenbo Sun, Haodong Wen, Xinyu Shi, Jiarui Cui, Chenyi Dang, Kaifeng Lyu, Wenguang Chen"
affiliations: "Tsinghua University, Peng Cheng Laboratory"
url: "https://openreview.net/forum?id=T5wkZJqzkz"
date: "2026-04-23"
category: "Optimization"
raw_source: "raw/lr-decay-openreview.md"
keywords:
  - learning-rate-scheduling
  - curriculum-learning
  - LLM-pretraining
  - data-ordering
---

# How LR Decay Wastes Your Best Data in Curriculum-Based LLM Pretraining

## Summary

TL;DR: Use model weight average to enhance curriculum learning in LLM pretraining.

- **Problem**: Due to the scarcity of high-quality data, large language models (LLMs) are often trained on mixtures of data with varying quality levels, even after sophisticated data curation.
- **Approach**: We find that while curriculum-based training substantially outperforms random shuffling when using a constant LR, its advantage diminishes under standard LR decay schedules.
- **Results**: By combining these strategies, we improve the average score on a suite of standard benchmarks by 1.64% over random shuffling, without additional data refinement.
- **Impact**: Validated on 1.5B-parameter models trained over 30B tokens with various data-quality metrics, our findings call for a re-evaluation of curriculum-based LLM pretraining and underscore the potential of co-designing data curricula with optimization methods.

**TL;DR:** Use model weight average to enhance curriculum learning in LLM pretraining..

## Abstract

Due to the scarcity of high-quality data, large language models (LLMs) are often trained on mixtures of data with varying quality levels, even after sophisticated data curation. A natural approach to better leverage high-quality data is curriculum-based pretraining, where the model is trained on data sorted in ascending order of quality as determined by a quality metric. However, prior studies have reported limited improvements from such curriculum-based pretraining strategies. This work identifies a critical factor constraining these methods: the incompatibility between the ascending data quality order and the decaying learning rate (LR) schedule. We find that while curriculum-based training substantially outperforms random shuffling when using a constant LR, its advantage diminishes under standard LR decay schedules. Our experiments show this incompatibility can be mitigated by two simple strategies: (1) employing a more moderate LR decay schedule, where the final LR is only moderately smaller than the peak LR, and (2) replacing LR decay with model averaging, i.e., computing a weighted average of the final few checkpoints. By combining these strategies, we improve the average score on a suite of standard benchmarks by 1.64% over random shuffling, without additional data refinement. Validated on 1.5B-parameter models trained over 30B tokens with various data-quality metrics, our findings call for a re-evaluation of curriculum-based LLM pretraining and underscore the potential of co-designing data curricula with optimization methods.

**TL;DR:** Use model weight average to enhance curriculum learning in LLM pretraining.

## Review Summary

**Decision:** Accept (Oral)

**Reviewer ratings:**
- Rating: 6
- Rating: 6
- Rating: 6

See [OpenReview discussion](https://openreview.net/forum?id=T5wkZJqzkz) for full reviews.

## Implementation Notes

- **OpenReview:** [T5wkZJqzkz](https://openreview.net/forum?id=T5wkZJqzkz)
- **Venue:** ICLR 2026 Oral
