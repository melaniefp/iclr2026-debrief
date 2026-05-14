---
title: "Prolific: Your Models Are Outgrowing Your Evaluations: Lessons from Building Evaluation Infrastructure for Frontier AI"
url: "https://iclr.cc/virtual/2026/expo-talk-panel/10020582"
source: "other"
author: "Prolific"
date: "2026-04-25"
captured: "2026-05-13"
tags:
  - iclr-2026
  - expo-talk
  - ai-evaluation
  - ai-safety
  - human-evaluation
  - frontier-models
aliases:
  - "Prolific ICLR 2026 Expo Talk"
  - "HUMAINE Framework"
related:
  - "raw/scale-ai-new-frontier-eval-rl-expo-talk.md"
  - "raw/iclr-2026-oral-session-2d-llms-evaluation.md"
  - "wiki/concepts/neural-scaling-laws.md"
  - "wiki/articles/prolific-ai-leaderboard-talk.md"
---

# Prolific: Your Models Are Outgrowing Your Evaluations

**ICLR 2026 Expo Talk Panel** — Sat, Apr 25, 2026 · 12:45 PM – 1:45 PM (BRT, UTC-3)

## Abstract

The capabilities of frontier AI systems are advancing faster than the methods used to evaluate them. Benchmark saturation, unrepresentative preference data, and safety evaluations that fail to reflect real deployment conditions have created a widening gap between measured performance and real-world impact. Closing this gap requires treating evaluation not as an afterthought to model development, but as a first-class infrastructure problem — one that demands scientific rigor in data collection design, representative and verified human populations, and evaluation paradigms that go beyond static benchmarks.

In this talk, we present Prolific's approach to building evaluation methodology and infrastructure for frontier AI. Prolific supports over 200,000 verified participants across 45 countries and has underpinned the data and methodology of more than 30,000 publications. We describe how we build on this foundation to develop evaluations that serve the needs of leading AI labs and research institutions: from demographically stratified preference studies and adversarial red-teaming to domain expert evaluation and alignment data collection.

We share what we have learned from designing evaluations that capture realistic scenarios and surface failures that matter.

## Case Studies

### 1. HUMAINE Framework — "Unpacking Human Preference for LLMs: Demographically Aware Evaluation"

Reveals how aggregate leaderboards conceal systematic preference disagreement across populations and how evaluation dimensions like trust and safety demand different methodological approaches than standard open-ended comparison.

### 2. Missing Red Line — "How Commercial Pressure Erodes AI Safety Boundaries"

An adversarial audit showing that even mild commercial objectives embedded in system prompts can override model safety training, even in scenarios with life-threatening consequences.

## Key Concepts

- **Evaluation infrastructure** — Treating AI evaluation as a first-class infrastructure problem rather than an afterthought
- **Benchmark saturation** — The phenomenon where AI systems saturate existing benchmarks, making them less informative
- **Demographically stratified evaluation** — Preference studies that account for population-level disagreement rather than using aggregate scores
- **Adversarial red-teaming** — Systematic testing of model safety boundaries using adversarial inputs
- **Verification gap** — The widening gap between measured model performance on benchmarks and real-world deployment impact
