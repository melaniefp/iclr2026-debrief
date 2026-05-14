---
title: "Digging Deeper: Learning Multi-Level Concept Hierarchies"
url: "https://openreview.net/forum?id=GGBRe4yegd"
source: "openreview"
author: "Oscar Hill, Mateo Espinosa Zarlenga, Mateja Jamnik"
date: "2026-04-23"
captured: "2026-05-13"
tags:
  - iclr-2026
  - openreview
  - explainable-artificial-intelligence
  - concept-based-explainability
  - concept-discovery
  - concept-hierarchy
  - concept-bottleneck-models
related:
  - "wiki/papers/digging-deeper.md"
---

# Digging Deeper: Learning Multi-Level Concept Hierarchies

**OpenReview:** [GGBRe4yegd](https://openreview.net/forum?id=GGBRe4yegd)
**Venue:** UCRL@ICLR2026 Poster

## Abstract

Concept-based models explain predictions using human-understandable concepts, but they typically rely on exhaustive annotations and treat concepts as flat and independent. To circumvent this, recent work has introduced *Hierarchical Concept Embedding Models* (HiCEMs) to explicitly model concept relationships, and *Concept Splitting* to discover sub-concepts using only coarse annotations. However, both methods are restricted to shallow hierarchies. We overcome this limitation with *Multi-Level Concept Splitting* (MLCS), which discovers multi-level concept hierarchies from only top-level supervision, and *Deep-HiCEMs*, an architecture that represents these discovered hierarchies and enables interventions at multiple levels of abstraction. Experiments show that MLCS discovers human-interpretable concepts absent during training and that Deep-HiCEMs maintain high accuracy while supporting test-time concept interventions that can improve task performance.