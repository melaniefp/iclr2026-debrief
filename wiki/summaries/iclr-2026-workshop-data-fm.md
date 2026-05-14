---
title: "Summary: DATA-FM Workshop"
type: "summary"
tags:
  - iclr-2026
  - workshop
  - data-quality
  - foundation-models
  - llm-evaluation
related:
  - "wiki/articles/data-fm-workshop.md"
  - "wiki/concepts/llm-evaluation.md"
  - "wiki/concepts/data-contamination.md"
sources:
  - "raw/iclr-2026-workshop-data-fm.md"
---

# Summary: DATA-FM Workshop

**TL;DR:** DATA-FM framed data as the core systems bottleneck for modern foundation models, tying together post-training, multimodality, memorization risk, and evaluation quality in one workshop agenda.

The workshop description makes a strong claim: the next wave of progress in foundation models depends less on raw parameter scale and more on how data are collected, curated, mixed, filtered, and evaluated. It connects reinforcement learning with verifiable rewards, multimodal alignment, agent logs, privacy, copyright, and fairness into one shared data-centric lens.

The invited program reinforces that framing. Baharan Mirzasoleiman focuses on post-training data curation for reasoning models, Sewon Min reframes data fragmentation as a systems and architecture problem, Juan Carlos Niebles pushes toward physical-world multimodal data, and Fred Sala treats benchmark design itself as a data-design problem. Together, these talks turn “data quality” from a vague slogan into a concrete research agenda.

The contributed talks broaden that agenda with work on domain mixing, evaluation under repeated sampling, memorization of factual knowledge, anchored decoding for copyright risk, and multimodal data mixtures. A useful pattern across the program is that data problems rarely stay local: a decision made for pretraining also shapes robustness, contamination risk, and downstream evaluation validity.

For the rest of this wiki, DATA-FM pairs naturally with the longer [workshop article](../articles/data-fm-workshop.md), the broader [LLM Evaluation](../concepts/llm-evaluation.md) concept page, and work on [Data Contamination](../concepts/data-contamination.md). It is one of the clearest workshop captures showing how data curation, measurement, and deployment risk now sit on the same critical path.
