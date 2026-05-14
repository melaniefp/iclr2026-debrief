---
title: "Beyond Prompt-Induced Lies: Investigating LLM Deception on Benign Prompts"
authors: "Various"
affiliations: "Various"
url: "https://openreview.net/forum?id=PDBBYwd1LY"
date: "2026-04-23"
category: "LLM Safety & Alignment"
raw_source: "raw/beyond-lies-openreview.md"
keywords:
  - LLM-deception
  - trustworthiness
  - contact-searching-questions
  - self-initiated-deception
---

# Beyond Prompt-Induced Lies: Investigating LLM Deception on Benign Prompts

## Summary

TL;DR: We detected the widespread deception of LLM under benign prompts and found its tendency increases with task difficulty.

- **Problem**: Large Language Models (LLMs) are widely deployed in reasoning, planning, and decision-making tasks, making their trustworthiness critical.
- **Approach**: This framework introduces two statistical metrics derived from psychological principles to quantify the likelihood of deception.
- **Results**: Evaluating 16 leading LLMs, we find that both metrics rise in parallel and escalate with task difficulty for most models.
- **Impact**: Moreover, increasing model capacity does not always reduce deception, posing a significant challenge for future LLM development.

**TL;DR:** We detected the widespread deception of LLM under benign prompts and found its tendency increases with task difficulty..

## Abstract

Large Language Models (LLMs) are widely deployed in reasoning, planning, and decision-making tasks, making their trustworthiness critical. A significant and underexplored risk is intentional deception, where an LLM deliberately fabricates or conceals information to serve a hidden objective. Existing studies typically induce deception by explicitly setting a hidden objective through prompting or fine-tuning, which may not reflect real-world human-LLM interactions. Moving beyond such human-induced deception, we investigate LLMs' self-initiated deception on benign prompts. To address the absence of ground truth, we propose a framework based on Contact Searching Questions~(CSQ). This framework introduces two statistical metrics derived from psychological principles to quantify the likelihood of deception. The first, the *Deceptive Intention Score*, measures the model's bias toward a hidden objective. The second, the *Deceptive Behavior Score*, measures the inconsistency between the LLM's internal belief and its expressed output. Evaluating 16 leading LLMs, we find that both metrics rise in parallel and escalate with task difficulty for most models. Moreover, increasing model capacity does not always reduce deception, posing a significant challenge for future LLM development.

**TL;DR:** We detected the widespread deception of LLM under benign prompts and found its tendency increases with task difficulty.

## Review Summary

**Decision:** Accept (Oral)

**Reviewer ratings:**
- Rating: 8
- Rating: 6
- Rating: 6

See [OpenReview discussion](https://openreview.net/forum?id=PDBBYwd1LY) for full reviews.

## Implementation Notes

- **OpenReview:** [PDBBYwd1LY](https://openreview.net/forum?id=PDBBYwd1LY)
- **Venue:** ICLR 2026 Oral
