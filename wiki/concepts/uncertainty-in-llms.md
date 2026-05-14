---
title: "Uncertainty in LLMs"
type: "concept"
tags: [uncertainty, llms, calibration, reliability]
related:
  - "wiki/concepts/llm-evaluation.md"
  - "wiki/concepts/inference-time-scaling.md"
  - "wiki/summaries/iclr-2026-workshop-world-models.md"
  - "wiki/summaries/iclr-2026-workshop-icbinb-llms.md"
  - "wiki/summaries/iclr-2026-workshop-trustworthy-ai.md"
  - "wiki/articles/trustworthy-ai-workshop.md"
  - "wiki/articles/icbinb-llms-workshop.md"
  - "wiki/papers/anatomy-of-uncertainty-llms.md"
sources:
  - "raw/anatomy-uncertainty-openreview.md"
  - "raw/uncertainty-tree-openreview.md"
  - "raw/trust-llms-openreview.md"
  - "raw/iclr-2026-workshop-trustworthy-ai.md"
  - "raw/iclr-2026-workshop-icbinb-llms.md"
---

# Uncertainty in LLMs

## Definition

Uncertainty in LLMs is the problem of representing when a model's answer should
be treated as ambiguous, undersupported, unstable, or otherwise unreliable.
Unlike simple classification confidence, language-model uncertainty must account
for multi-token generation, branching semantics, retrieval gaps, and interaction
context.

ICLR 2026 surfaced this as a practical systems issue rather than a purely
statistical one. [The Anatomy of Uncertainty in LLMs](../papers/anatomy-of-uncertainty-llms.md)
proposes decomposing uncertainty into input ambiguity, knowledge gaps, and
decoding randomness, while [Challenges in Inference-Time Scaling with
Uncertainty-Aware Tree Search](../papers/uncertainty-aware-tree-search.md)
shows that uncertainty estimates themselves can fail under search-induced
distribution shift.

The conference workshop ecosystem treated uncertainty as a core part of
trustworthy deployment, not an optional dashboard metric. That directly connects
this concept to [LLM Evaluation](llm-evaluation.md) and [Inference-Time
Scaling](inference-time-scaling.md).

## Key Ideas

- **Uncertainty is multi-source**: ambiguity in the prompt, missing knowledge,
  and stochastic decoding can dominate in different regimes.
- **Semantic variation matters**: [When Can You TRUST Large Language Models?](../papers/when-can-you-trust-llms.md)
  measures uncertainty across multiple rollouts rather than only next-token
  probabilities.
- **Process uncertainty is useful but fragile**: uncertainty-aware tree search
  works only if the uncertainty model remains calibrated off distribution.
- **Calibration is interaction-dependent**: expert-level questions and
  conversational settings often reveal overconfidence most sharply.
- **Uncertainty should inform control**: search, ranking, refusal, and steering
  policies all need access to confidence information.
- **Useful uncertainty must be actionable**: the goal is not just reporting a
  score, but changing system behavior under risk.

## Related Work at ICLR 2026

- [The Anatomy of Uncertainty in LLMs](../papers/anatomy-of-uncertainty-llms.md)
  decomposes uncertainty into ambiguity, knowledge gaps, and decoding noise.
- [Challenges in Inference-Time Scaling with Uncertainty-Aware Tree Search](../papers/uncertainty-aware-tree-search.md)
  highlights the distribution-shift problem for uncertainty-guided search.
- [When Can You TRUST Large Language Models?](../papers/when-can-you-trust-llms.md)
  proposes rollout-based semantic uncertainty scores.
- [Workshop: Principled Design for Trustworthy AI](../articles/trustworthy-ai-workshop.md)
  treats uncertainty as part of a trustworthy-AI stack.
- [Workshop: I Can't Believe It's Not Better](../articles/icbinb-llms-workshop.md)
  links uncertainty to reward hacking, multilingual reliability, and factuality.

## Open Questions

- Which uncertainty estimates remain well calibrated under search, tool use, and
  long-context interaction?
- How should systems expose uncertainty to users without encouraging complacency
  or over-refusal?
- Can we decompose uncertainty online during dialogue or agent execution?
- What forms of uncertainty are most useful for intervention, not just for
  reporting?
