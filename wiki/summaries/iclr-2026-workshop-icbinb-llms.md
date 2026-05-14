---
title: "Summary: ICBINB LLMs Workshop"
type: "summary"
tags:
  - iclr-2026
  - workshop
  - llm-evaluation
  - reward-hacking
  - safety
related:
  - "wiki/articles/icbinb-llms-workshop.md"
  - "wiki/concepts/llm-evaluation.md"
  - "wiki/concepts/reward-hacking.md"
  - "wiki/concepts/uncertainty-in-llms.md"
sources:
  - "raw/iclr-2026-workshop-icbinb-llms.md"
---

# Summary: ICBINB LLMs Workshop

**TL;DR:** ICBINB turned negative results into first-class scientific evidence, focusing on where LLMs fail, why scaling often misleads, and how better diagnostics can convert failure into design guidance.

The workshop description explicitly argues that hallucination, brittle reasoning, alignment failures, and efficiency limits should be studied in their own right rather than treated as embarrassing side notes. That norm matters: it shifts the conversation from headline benchmark gains toward careful analysis of boundary conditions, shortcut learning, and failed interventions.

The invited talks make that agenda concrete. Adam Block analyzes how best-of-N search can amplify [reward hacking](../concepts/reward-hacking.md), Marta Garnelo contrasts LLMs with decision trees on tabular prediction, Aditi Raghunathan questions the creative limits of next-token prediction, Preslav Nakov foregrounds factuality and uncertainty, and Sewon Min asks whether mixture-of-experts models are actually modular. Each talk treats failure as a clue about model structure rather than just a benchmark deficit.

The rest of the program extends the same theme across hallucination detection, fairness, modality gaps, safety drift, multilingual reliability, and inference-time scaling. The workshop therefore sits squarely inside the broader [LLM Evaluation](../concepts/llm-evaluation.md) agenda, but with a sharper focus on diagnostic experiments and actionable negative results.

For this knowledge base, the page works best alongside the longer [ICBINB workshop article](../articles/icbinb-llms-workshop.md), the [Reward Hacking](../concepts/reward-hacking.md) concept page, and the repo's growing material on [Uncertainty in LLMs](../concepts/uncertainty-in-llms.md). It is one of the clearest captures of ICLR 2026's push toward more honest model science.
