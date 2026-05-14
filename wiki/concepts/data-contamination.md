---
title: "Data Contamination"
type: "concept"
tags: [data-contamination, memorization, benchmarking, llm-evaluation]
related:
  - "wiki/concepts/llm-evaluation.md"
  - "wiki/concepts/model-collapse.md"
  - "wiki/articles/prolific-ai-leaderboard-talk.md"
  - "wiki/papers/codec-data-contamination-detection.md"
  - "wiki/papers/language-model-micro-benchmarking.md"
sources:
  - "raw/codec-openreview.md"
  - "raw/prolific-evaluation-infrastructure-expo-talk.md"
  - "raw/micro-bench-openreview.md"
---

# Data Contamination

## Definition

Data contamination is the leakage of benchmark or evaluation content into a
model's training data, post-training data, or cached synthetic data pipeline.
When contamination occurs, strong benchmark performance may reflect memorization
or exposure rather than transferable capability.

At ICLR 2026, contamination was treated as a benchmark-integrity issue rather
than a niche audit concern. [CoDeC](../papers/codec-data-contamination-detection.md)
proposes a practical black-box detector based on how in-context examples change
model behavior, providing a way to estimate whether a benchmark is acting more
like a memory probe than a generalization test.

This concept also overlaps with broader concerns about synthetic-data loops and
measurement infrastructure. If evaluation data are contaminated, then leaderboards
can quietly reward memorization and distort downstream training choices.

## Key Ideas

- **Contamination corrupts interpretation**: a high score may no longer imply the
  model can solve unseen tasks of the same type.
- **Open-weight opacity makes the problem harder**: undisclosed pretraining mixes
  make it difficult to know whether a benchmark was seen.
- **Black-box detection is possible**: CoDeC uses the effect of in-context
  examples as a signal for memorization-like behavior.
- **Contamination is not binary**: datasets can be partially seen, indirectly
  paraphrased, or leaked through synthetic derivatives.
- **Evaluation and data governance are linked**: benchmark integrity depends on
  documentation, auditing, and disciplined reuse policies.
- **Contamination interacts with other evaluation shortcuts**: micro-benchmarks
  and public leaderboards can amplify the damage once leaked items are known.

## Related Work at ICLR 2026

- [CoDeC: Detecting Data Contamination in LLMs via In-Context Learning](../papers/codec-data-contamination-detection.md)
  introduces contamination scores that separate seen from unseen datasets.
- [How Reliable is Language Model Micro-Benchmarking?](../papers/language-model-micro-benchmarking.md)
  complements the contamination story by asking whether small benchmark slices
  preserve meaningful rankings at all.
- [Prolific on Evaluation Infrastructure](../articles/prolific-ai-leaderboard-talk.md)
  argues that trustworthy measurement needs stronger data and scenario design.
- [LLM Evaluation](llm-evaluation.md) is the broader umbrella concept under which
  contamination becomes a first-order benchmarking concern.

## Open Questions

- How can labs report contamination risk when training corpora are only partly
  documented or are continually updated?
- What benchmark release practices reduce contamination without blocking useful
  public evaluation?
- Can contamination detectors distinguish memorization from legitimate transfer?
- How should contaminated benchmarks be used once leakage is suspected but not
  precisely quantified?
