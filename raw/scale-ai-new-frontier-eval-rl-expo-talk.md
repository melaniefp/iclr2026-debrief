---
title: "Scale AI: New Frontier of AI: Eval, RL, and What's Next"
url: "https://iclr.cc/virtual/2026/expo-talk-panel/10020578"
source: "other"
author: "Scale AI"
date: "2026-04-24"
captured: "2026-05-13"
tags:
  - iclr-2026
  - expo-talk
  - ai-evaluation
  - reinforcement-learning
  - frontier-models
  - ai-agents
aliases:
  - "New Frontier of AI"
  - "Scale AI ICLR 2026 Expo Talk"
related:
  - "raw/iclr-2026-oral-session-2d-llms-evaluation.md"
  - "wiki/concepts/neural-scaling-laws.md"
  - "wiki/articles/scale-ai-eval-rl-talk.md"
---

# Scale AI: New Frontier of AI: Eval, RL, and What's Next

**ICLR 2026 Expo Talk Panel** — Fri, Apr 24, 2026 · 12:45 PM – 1:45 PM (BRT, UTC-3)

## Abstract

As large language models (LLMs) evolve from short-burst chatbots into long-horizon autonomous agents, progress is increasingly bottlenecked by verification asymmetry: rapid gains in domains with cheap correctness signals (e.g., math and code) contrast sharply with limited progress in tasks with weak or delayed verification, such as research planning and strategic decision-making. This talk argues that evaluation and reinforcement learning (RL) beyond easily verifiable domains are the next critical frontier for AI capability.

We present results from three new evaluation frameworks:

- **Humanity's Last Exam (HLE)** — Shows that frontier models are frequently wrong and overconfident at the human-expert level.
- **Remote Labor Index (RLI)** — Demonstrates that current agents automate only ~2.5% of real, paid freelance work.
- **Visual ToolBench** — Reveals that 70–80% of multimodal agent failures stem from visual perception rather than reasoning.

To close these gaps, we introduce **Rubrics as Rewards (RaR)** within a **Group Relative Policy Optimization (GRPO)** framework. We show that Dynamic Rubrics, which adaptively elicit evaluation criteria by contrasting model outputs during training, outperform static human-written rubrics and reduce reward hacking in the high-reward regime. These findings motivate a shift from static benchmarks to high-fidelity RL environments, such as **Scale Gymnasium**, that train agents through interaction rather than imitation.

## Key Concepts

- **Verification asymmetry** — The gap between domains with cheap correctness signals (math, code) and those with weak/delayed verification (research planning, strategy)
- **Rubrics as Rewards (RaR)** — Using evaluation rubrics as reward signals for RL training
- **Dynamic Rubrics** — Adaptively generated evaluation criteria based on contrasting model outputs during training
- **Group Relative Policy Optimization (GRPO)** — RL framework used with RaR for training beyond verifiable domains
- **Scale Gymnasium** — High-fidelity RL environments for training agents through interaction

## Evaluation Frameworks Presented

| Framework | Finding |
|-----------|---------|
| Humanity's Last Exam (HLE) | Frontier models frequently wrong and overconfident at expert level |
| Remote Labor Index (RLI) | Current agents automate only ~2.5% of real freelance work |
| Visual ToolBench | 70–80% of multimodal agent failures from visual perception, not reasoning |
