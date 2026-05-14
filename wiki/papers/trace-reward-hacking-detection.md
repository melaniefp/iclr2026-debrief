---
title: "Is it Thinking or Cheating? Detecting Implicit Reward Hacking by Measuring Reasoning Effort"
authors: "Various"
affiliations: "Various"
url: "https://openreview.net/forum?id=Gk7gLAtVDO"
date: "2026-04-23"
category: "LLM Safety & Alignment"
raw_source: "raw/trace-reward-openreview.md"
keywords:
  - reward-hacking
  - chain-of-thought
  - reasoning-effort
  - TRACE
---

# Is it Thinking or Cheating? Detecting Implicit Reward Hacking by Measuring Reasoning Effort

## Summary

TL;DR: TRACE detects implicit reward hacking by measuring how quickly truncated reasoning suffices to pass verification, outperforming CoT monitoring and enabling hidden loopholes discovery.

- **Problem**: Reward hacking, where a reasoning model exploits loopholes in a reward function to achieve high rewards without solving the intended task, poses a significant threat.
- **Approach**: TRACE quantifies effort by measuring how early a model's reasoning becomes sufficient to obtain the reward.
- **Results**: We further show that TRACE can discover unknown loopholes during training.
- **Impact**: Overall, TRACE offers a scalable unsupervised approach for oversight where current monitoring methods prove ineffective.

**TL;DR:** TRACE detects implicit reward hacking by measuring how quickly truncated reasoning suffices to pass verification, outperforming CoT monitoring and enabling hidden loopholes discovery..

## Abstract

Reward hacking, where a reasoning model exploits loopholes in a reward function to achieve high rewards without solving the intended task, poses a significant threat. This behavior may be explicit, i.e. verbalized in the model's chain-of-thought (CoT), or implicit, where the CoT appears benign thus bypasses CoT monitors. To detect implicit reward hacking, we propose TRACE (Truncated Reasoning AUC Evaluation). Our key observation is that hacking occurs when exploiting the loophole is easier than solving the actual task. This means that the model is using less "effort" than required to achieve high reward.  TRACE quantifies effort by measuring how early a model's reasoning becomes sufficient to obtain the reward. We progressively truncate a model's CoT at various lengths, force the model to answer, and estimate the expected reward at each cutoff. A hacking model, which takes a shortcut, will achieve a high expected reward with only a small fraction of its CoT, yielding a large area under the reward-vs-length curve. TRACE achieves over 65% gains over our strongest 72B CoT monitor in math reasoning, and over 30% gains over a 32B monitor in coding. We further show that TRACE can discover unknown loopholes during training. Overall, TRACE offers a scalable unsupervised approach for oversight where current monitoring methods prove ineffective.

**TL;DR:** TRACE detects implicit reward hacking by measuring how quickly truncated reasoning suffices to pass verification, outperforming CoT monitoring and enabling hidden loopholes discovery.

## Review Summary

**Decision:** Accept (Oral)

**Reviewer ratings:**
- Rating: 6
- Rating: 8
- Rating: 8
- Rating: 8

See [OpenReview discussion](https://openreview.net/forum?id=Gk7gLAtVDO) for full reviews.

## Implementation Notes

- **OpenReview:** [Gk7gLAtVDO](https://openreview.net/forum?id=Gk7gLAtVDO)
- **Venue:** ICLR 2026 Oral
