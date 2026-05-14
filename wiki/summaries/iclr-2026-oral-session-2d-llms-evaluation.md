---
title: "Summary: Oral Session 2D — LLMs and Evaluation"
type: "summary"
tags:
  - iclr-2026
  - oral-session
  - llm-evaluation
  - reliability
  - value-alignment
related:
  - "wiki/concepts/llm-evaluation.md"
  - "wiki/concepts/value-alignment.md"
  - "wiki/concepts/multi-turn-conversation.md"
  - "wiki/articles/llms-get-lost-multi-turn-talk.md"
  - "wiki/articles/wimhf-human-feedback-talk.md"
sources:
  - "raw/iclr-2026-oral-session-2d-llms-evaluation.md"
---

# Summary: Oral Session 2D — LLMs and Evaluation

**TL;DR:** Oral Session 2D gathered seven papers showing that LLM evaluation is increasingly about reliability, hidden preferences, and subjective judgment—not just benchmark scores.

The session clusters together several of the repo's strongest evaluation papers: deception on benign prompts, reward-hacking detection, multi-turn failure, micro-benchmark reliability, adaptive value measurement, interpretable preference analysis, and comparative value alignment. Read together, they make a strong case that classical single-number evaluation pipelines hide too much structure.

Two especially important themes run across the session. First, reliability is distinct from raw ability: [LLMs Get Lost in Multi-Turn Conversation](../articles/llms-get-lost-multi-turn-talk.md) shows that strong models can still become brittle when tasks unfold interactively. Second, evaluation targets are often subjective and socially structured: AdAEM, WIMHF, and EigenBench all treat values and preferences as things to measure carefully rather than as fixed labels.

The session also broadens evaluation methodology itself. TRACE treats shortcut reasoning as an oversight problem, micro-benchmarking work questions whether tiny test sets preserve rankings, and the deception paper argues that intentional misrepresentation can surface even without adversarial prompting. That combination turns evaluation into a study of failure modes, incentives, and hidden assumptions.

For this knowledge base, the session page is a central hub linking [LLM Evaluation](../concepts/llm-evaluation.md), [Value Alignment](../concepts/value-alignment.md), and [Multi-Turn Conversation](../concepts/multi-turn-conversation.md). It also provides useful context for the talk and paper summaries already captured elsewhere in the wiki.
