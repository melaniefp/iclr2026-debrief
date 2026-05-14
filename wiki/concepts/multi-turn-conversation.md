---
title: "Multi-Turn Conversation"
type: "concept"
tags: [multi-turn, conversation, llm-evaluation, reliability]
related:
  - "wiki/concepts/llm-evaluation.md"
  - "wiki/concepts/uncertainty-in-llms.md"
  - "wiki/summaries/iclr-2026-oral-session-2d-llms-evaluation.md"
  - "wiki/articles/llms-get-lost-multi-turn-talk.md"
  - "wiki/articles/scale-ai-eval-rl-talk.md"
  - "wiki/papers/llms-get-lost-in-multi-turn-conversation.md"
sources:
  - "raw/llms-get-lost-in-multi-turn-conversation-src/README.md"
  - "raw/llms-get-lost-in-multi-turn-conversation-talk/README.md"
  - "raw/iclr-2026-oral-session-2d-llms-evaluation.md"
---

# Multi-Turn Conversation

## Definition

Multi-turn conversation is the interactive setting where a user reveals intent,
constraints, and corrections across several exchanges rather than in one fully
specified prompt. For deployed assistants this is the normal case, but ICLR 2026
showed that current LLMs remain much less reliable in this regime than standard
single-turn benchmarks suggest.

The key conference result was [LLMs Get Lost In Multi-Turn Conversation](../papers/llms-get-lost-in-multi-turn-conversation.md),
which used sharded simulations to compare identical tasks in single-turn and
underspecified multi-turn formats. The main finding was not a total loss of
capability, but a large rise in unreliability: models commit early, build the
wrong latent task state, and fail to recover.

This makes multi-turn conversation a core benchmark concept for agentic systems,
real-world evaluation, and human-AI interaction design.

## Key Ideas

- **Underspecification is the norm**: users often refine tasks over time instead
  of delivering the full instruction upfront.
- **Interaction structure itself matters**: the concat control in the paper shows
  that sharding information across turns hurts more than merely rephrasing it.
- **Early commitment is costly**: premature answers create path dependence that
  later clarifications do not fully erase.
- **Reliability and aptitude diverge**: strong models still “know” the task, but
  their trajectories become unstable across runs.
- **Memory aids only partly help**: recap and snowball strategies recover some
  performance but do not solve the underlying revision problem.
- **Conversation is an evaluation setting, not just a UX wrapper**: a model that
  looks strong in one-shot prompts can fail badly in iterative collaboration.

## Related Work at ICLR 2026

- [LLMs Get Lost In Multi-Turn Conversation](../papers/llms-get-lost-in-multi-turn-conversation.md)
  introduces sharded simulation, the aptitude-versus-unreliability split, and a
  39% average performance drop.
- [LLMs Get Lost in Multi-Turn Conversation — Summary](../articles/llms-get-lost-multi-turn-talk.md)
  interprets the failure as conversational brittleness rather than simple lack
  of reasoning ability.
- [Oral Session 2D: LLMs and Evaluation](../../raw/iclr-2026-oral-session-2d-llms-evaluation.md)
  situates the paper alongside evaluation and alignment work.
- [Scale AI on Evaluation and RL Frontiers](../articles/scale-ai-eval-rl-talk.md)
  reinforces why interactive, real-work settings expose weaknesses that static
  tasks miss.

## Open Questions

- How should models represent latent user intent so they can revise it cleanly?
- Can conversational uncertainty estimates prevent premature commitment?
- What forms of memory or planning help without increasing verbosity and drift?
- Which multi-turn benchmarks best predict reliability in real agent workflows?
