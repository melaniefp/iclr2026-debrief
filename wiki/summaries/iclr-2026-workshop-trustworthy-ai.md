---
title: "Summary: Trustworthy AI Workshop"
type: "summary"
tags:
  - iclr-2026
  - workshop
  - trustworthy-ai
  - interpretability
  - uncertainty
related:
  - "wiki/articles/trustworthy-ai-workshop.md"
  - "wiki/concepts/mechanistic-interpretability.md"
  - "wiki/concepts/uncertainty-in-llms.md"
  - "wiki/concepts/value-alignment.md"
sources:
  - "raw/iclr-2026-workshop-trustworthy-ai.md"
---

# Summary: Trustworthy AI Workshop

**TL;DR:** The Trustworthy AI workshop organized interpretability, robustness, uncertainty, and safety into one end-to-end design agenda for building models that can be trusted beyond the lab.

The workshop description is unusually explicit that trustworthiness must be addressed across the full lifecycle: training, evaluation, inference-time monitoring, and deployment. Its six pillars cover interpretable and intervenable models, inference-time safeguards, multimodal trust challenges, robustness and threat models, deployment-oriented evaluation, and safety in LLM agents.

That breadth is matched by the keynote schedule. Mihaela van der Schaar emphasizes dynamical understanding and causality, Fernanda Viégas argues for user-facing interpretability, Hamed Hassani focuses on catastrophic forgetting, Violet Peng presents compute-efficient safety interventions, and Yan Liu pushes on feature interaction as actionable interpretability. The result is a workshop that treats trust as a systems property rather than a narrow audit metric.

The spotlight and poster lists extend that stance across adversarial attacks, sparse autoencoders, subgroup fairness, calibration, RAG failures, multimodal robustness, and agent supervision. A consistent theme is that trustworthy behavior depends on both internal representations and external process design: better mechanisms, better monitors, and better deployment practices all matter.

Within this repo, the capture connects directly to the more detailed [Trustworthy AI workshop article](../articles/trustworthy-ai-workshop.md), to [Mechanistic Interpretability](../concepts/mechanistic-interpretability.md), and to [Uncertainty in LLMs](../concepts/uncertainty-in-llms.md). It is also a useful bridge to broader questions of [Value Alignment](../concepts/value-alignment.md) and intervention design.
