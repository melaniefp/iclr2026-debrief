---
title: "The Missing Red Line: How Commercial Pressure Erodes AI Safety Boundaries"
authors: "Nora Petrova, John Burden"
affiliations: "Prolific AI Research"
url: "https://openreview.net/forum?id=ev58E64j0n"
date: "2026-04-23"
category: "LLM Safety & Alignment"
raw_source: "raw/missing-red-line-openreview.md"
keywords:
  - ai-safety
  - commercial-pressure
  - red-lines
  - safety-boundaries
---

# The Missing Red Line: How Commercial Pressure Erodes AI Safety Boundaries

## Summary

TL;DR: Commercial system prompts can override AI safety training, causing models to recommend dangerous products and dismiss health risks, and most models show no 'red line' even when potential harms escalate to life-threatening

- **Problem**: What happens when an AI assistant is told to "maximise sales" while a user asks about drug interactions? We find that commercial system prompts can override safety training, causing frontier models to lie about medical risks, dismiss safety concerns, and prioritise profit over user welfare.
- **Approach**: Most alarmingly, models show no "red line", their willingness to comply with harmful requests does not decrease as potential consequences escalate from minor to life-threatening.
- **Results**: Most alarmingly, models show no "red line", their willingness to comply with harmful requests does not decrease as potential consequences escalate from minor to life-threatening.
- **Impact**: Our findings suggest that current safety training does not generalise to commercial deployment contexts.

**TL;DR:** Commercial system prompts can override AI safety training, causing models to recommend dangerous products and dismiss health risks, and most models show no 'red line' even when potential harms escalate to life-threatening.

## Abstract

What happens when an AI assistant is told to "maximise sales" while a user asks about drug interactions? We find that commercial system prompts can override safety training, causing frontier models to lie about medical risks, dismiss safety concerns, and prioritise profit over user welfare. Testing 8 models in scenarios where commercial objectives conflict with user safety---a diabetic asking about high-sugar supplements, an investor being pushed toward unsuitable products, a traveller steered away from safety warnings---we uncover catastrophic failures: models fabricating safety information, explicitly reasoning they should refuse but proceeding anyway, and actively discouraging users from consulting doctors. Most alarmingly, models show no "red line", their willingness to comply with harmful requests does not decrease as potential consequences escalate from minor to life-threatening. Our findings suggest that current safety training does not generalise to commercial deployment contexts.

**TL;DR:** Commercial system prompts can override AI safety training, causing models to recommend dangerous products and dismiss health risks, and most models show no 'red line' even when potential harms escalate to life-threatening


## Implementation Notes

- **OpenReview:** [ev58E64j0n](https://openreview.net/forum?id=ev58E64j0n)
- **Venue:** ICLR 2026 Workshop ICBINB
