---
title: "Summary: Lifelong Agents Workshop"
type: "summary"
tags:
  - iclr-2026
  - workshop
  - lifelong-agents
  - continual-learning
  - agent-alignment
related:
  - "wiki/articles/lifelong-agents-workshop.md"
  - "wiki/concepts/world-models.md"
  - "wiki/concepts/human-robot-interaction.md"
sources:
  - "raw/iclr-2026-workshop-lifelong-agents.md"
---

# Summary: Lifelong Agents Workshop

**TL;DR:** The Lifelong Agents workshop argued that capable agents must keep learning, stay aligned, and adapt after deployment rather than freezing intelligence at training time.

The workshop description defines lifelong agents as systems that continuously learn, align, and evolve across their operational life. That framing brings continual learning, long-term alignment, memory, self-improvement, and deployment constraints into the same design problem. It also makes clear that agent progress cannot be reduced to one-shot benchmark performance.

The invited schedule spans robotics, safety, small-model deployment, and agent architecture. Sergey Levine brings an embodied, real-world data perspective; Natasha Jaques reframes safety as a multi-agent problem; and other speakers push on memory, context engineering, and efficient improvement over time. The overall signal is that lifelong agency is becoming a systems question about adaptation loops, not just a prompting trick.

The oral and poster selections reinforce that emphasis with work on context engineering, world modeling, text feedback, continual learning, and online memory. A recurring idea across the program is that agents need mechanisms for self-correction, uncertainty-aware action, and user-facing legibility if they are going to improve safely in long-running settings.

This capture pairs naturally with the longer [Lifelong Agents workshop article](../articles/lifelong-agents-workshop.md) and the repo's [World Models](../concepts/world-models.md) and [Human-Robot Interaction](../concepts/human-robot-interaction.md) concepts. It is one of the strongest workshop overviews for understanding how adaptation, alignment, and embodiment are converging.
