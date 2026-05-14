---
title: "LLM Evaluation"
type: "concept"
tags: [llm-evaluation, reliability, benchmarking, alignment]
related:
  - "wiki/concepts/data-contamination.md"
  - "wiki/concepts/multi-turn-conversation.md"
  - "wiki/concepts/value-alignment.md"
  - "wiki/summaries/iclr-2026-oral-session-2d-llms-evaluation.md"
  - "wiki/summaries/iclr-2026-workshop-data-fm.md"
  - "wiki/summaries/iclr-2026-workshop-icbinb-llms.md"
  - "wiki/summaries/prolific-evaluation-infrastructure-expo-talk.md"
  - "wiki/summaries/scale-ai-new-frontier-eval-rl-expo-talk.md"
  - "wiki/articles/icbinb-llms-workshop.md"
  - "wiki/articles/scale-ai-eval-rl-talk.md"
sources:
  - "raw/iclr-2026-oral-session-2d-llms-evaluation.md"
  - "raw/micro-bench-openreview.md"
  - "raw/codec-openreview.md"
  - "raw/iclr-2026-workshop-icbinb-llms.md"
  - "raw/prolific-evaluation-infrastructure-expo-talk.md"
  - "raw/scale-ai-new-frontier-eval-rl-expo-talk.md"
---

# LLM Evaluation

## Definition

LLM evaluation is the study of how to measure model capability, reliability,
alignment, and deployment risk in ways that survive contact with real use.
ICLR 2026 repeatedly emphasized that evaluation is not just about ranking models
on static leaderboards; it is about understanding what a score actually means,
which failure modes it hides, and which behaviors it will incentivize.

The conference's oral session on “LLMs and Evaluation” made this especially
clear. Papers on multi-turn failure, micro-benchmark reliability, deceptive
behavior, preference structure, and value measurement all pointed to the same
lesson: simple single-number scores compress away too much structure. Evaluation
must track interaction setting, contamination, uncertainty, and whose values are
being represented.

That framing connects evaluation to infrastructure. The
[Prolific evaluation talk](../articles/prolific-ai-leaderboard-talk.md) and the
[Scale AI evaluation talk](../articles/scale-ai-eval-rl-talk.md) both argue that
measurement systems actively steer future model behavior rather than merely
reporting it.

## Key Ideas

- **Reliability is distinct from raw aptitude**: [LLMs Get Lost In Multi-Turn
  Conversation](../papers/llms-get-lost-in-multi-turn-conversation.md) shows
  strong models can still become unreliable in interactive settings.
- **Cheap evaluation can be misleading**: [How Reliable is Language Model
  Micro-Benchmarking?](../papers/language-model-micro-benchmarking.md) finds
  that tiny benchmark subsets often fail to preserve model rankings.
- **Benchmark integrity matters**: [CoDeC](../papers/codec-data-contamination-detection.md)
  treats [Data Contamination](data-contamination.md) as a first-class evaluation
  failure mode.
- **Trust depends on task structure**: multi-turn tasks, expert-level questions,
  and real labor tasks expose failures that static single-turn benchmarks hide.
- **Values are part of evaluation**: [EigenBench](../papers/eigenbench-value-alignment.md)
  and [AdAEM](../papers/adaem-llm-value-measurement.md) treat alignment as a
  measurement problem, not only a training objective.
- **Human populations matter**: demographic disagreement in evaluation changes
  what a leaderboard score means.
- **Evaluation becomes training signal**: rubrics, judges, and verifiers often
  double as the reward layer for post-training or inference-time search.

## Related Work at ICLR 2026

- [Oral Session 2D: LLMs and Evaluation](../../raw/iclr-2026-oral-session-2d-llms-evaluation.md)
  clusters deception, reward hacking, multi-turn reliability, value measurement,
  and preference analysis in one session.
- [How Reliable is Language Model Micro-Benchmarking?](../papers/language-model-micro-benchmarking.md)
  argues that evaluation efficiency often trades off sharply against ranking
  reliability.
- [LLMs Get Lost In Multi-Turn Conversation](../papers/llms-get-lost-in-multi-turn-conversation.md)
  reframes conversational evaluation around underspecification and recovery.
- [CoDeC: Detecting Data Contamination in LLMs via In-Context Learning](../papers/codec-data-contamination-detection.md)
  provides a contamination detector that can be embedded into benchmark audits.
- [Workshop: I Can't Believe It's Not Better](../articles/icbinb-llms-workshop.md)
  treats failure analysis itself as an evaluation methodology.
- [Prolific on Evaluation Infrastructure](../articles/prolific-ai-leaderboard-talk.md)
  and [Scale AI on Evaluation and RL Frontiers](../articles/scale-ai-eval-rl-talk.md)
  push toward scenario-aware, deployment-aware evaluation systems.

## Open Questions

- What should replace static leaderboards for interactive and long-horizon agents?
- How do we separate true capability gains from contamination, prompt quirks, or
  evaluator bias?
- Which uncertainty estimates are practical enough to become default reporting
  in deployed systems?
- How can evaluation remain informative when models, tasks, and human norms all
  co-evolve rapidly?
