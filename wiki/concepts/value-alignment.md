---
title: "Value Alignment"
type: "concept"
tags: [value-alignment, alignment, evaluation, human-feedback]
related:
  - "wiki/concepts/llm-evaluation.md"
  - "wiki/concepts/reward-hacking.md"
  - "wiki/summaries/iclr-2026-oral-session-2d-llms-evaluation.md"
  - "wiki/summaries/prolific-evaluation-infrastructure-expo-talk.md"
  - "wiki/articles/prolific-ai-leaderboard-talk.md"
  - "wiki/papers/eigenbench-value-alignment.md"
  - "wiki/papers/adaem-llm-value-measurement.md"
sources:
  - "raw/eigenbench-openreview.md"
  - "raw/adaem-openreview.md"
  - "raw/iclr-2026-oral-session-2d-llms-evaluation.md"
  - "raw/prolific-evaluation-infrastructure-expo-talk.md"
---

# Value Alignment

## Definition

Value alignment is the problem of getting AI systems to behave in ways that are
consistent with human values, norms, and constraints. At ICLR 2026, the most
visible work on this topic focused less on solving alignment end-to-end and more
on measuring value differences, value drift, and disagreement between models and
human populations.

That measurement focus matters because values are rarely available as objective
ground-truth labels. [EigenBench](../papers/eigenbench-value-alignment.md)
treats alignment as a comparative, constitution-conditioned judgment problem,
while [AdAEM](../papers/adaem-llm-value-measurement.md) argues that static value
question sets quickly become uninformative as models converge on generic safety
language.

Value alignment therefore appears in this repo as both a normative question and
a benchmarking question, closely tied to [LLM Evaluation](llm-evaluation.md) and
to the design of human-feedback pipelines.

## Key Ideas

- **Alignment is plural, not scalar**: different constitutions, cultures, and
  user groups can disagree legitimately about preferred behavior.
- **Measurement without labels is possible**: EigenBench aggregates model
  judgments with an EigenTrust-style procedure instead of relying on one gold
  answer for subjective scenarios.
- **Static surveys go stale**: AdAEM adaptively generates new questions to keep
  pace with changing model capabilities and controversies.
- **Preference data encode hidden assumptions**: the
  [Prolific evaluation article](../articles/prolific-ai-leaderboard-talk.md)
  stresses that evaluator sampling changes the meaning of “aligned.”
- **Alignment metrics can be gamed**: once a value benchmark becomes a target,
  it risks becoming another proxy objective.
- **Good alignment evaluation must expose disagreement**: demographic structure,
  scenario design, and task framing all matter.

## Related Work at ICLR 2026

- [EigenBench: A Comparative Behavioral Measure of Value Alignment](../papers/eigenbench-value-alignment.md)
  proposes comparative scoring under a specified constitution.
- [AdAEM: An Adaptively and Automated Extensible Measurement of LLMs' Value
  Difference](../papers/adaem-llm-value-measurement.md) uses adaptive question
  generation to surface informative value boundaries.
- [What's In My Human Feedback?](../papers/whats-in-my-human-feedback.md)
  analyzes which preferences real feedback datasets actually encode.
- [Oral Session 2D: LLMs and Evaluation](../../raw/iclr-2026-oral-session-2d-llms-evaluation.md)
  grouped AdAEM and EigenBench with broader trustworthiness work.
- [Prolific on Evaluation Infrastructure](../articles/prolific-ai-leaderboard-talk.md)
  adds a demographic and deployment-aware lens to value measurement.

## Open Questions

- How should alignment benchmarks represent genuine moral and cultural pluralism?
- Can adaptive value benchmarks avoid becoming contaminated or overfit targets?
- What is the right balance between black-box behavioral metrics and deeper
  causal understanding of learned values?
- How should value-alignment scores be reported when human evaluators disagree?
