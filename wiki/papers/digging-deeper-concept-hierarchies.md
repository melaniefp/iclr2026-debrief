---
title: "Digging Deeper: Learning Multi-Level Concept Hierarchies"
authors: "Oscar Hill, Mateo Espinosa Zarlenga, Mateja Jamnik"
affiliations: "University of Cambridge, University of Manchester, University of Oxford"
url: "https://openreview.net/forum?id=GGBRe4yegd"
date: "2026-04-23"
category: "Interpretability"
raw_source: "raw/digging-deeper-openreview.md"
keywords:
  - concept-hierarchies
  - hierarchical-learning
  - interpretability
  - concept-models
---

# Digging Deeper: Learning Multi-Level Concept Hierarchies

## Summary

TL;DR: Concept-based models explain predictions using human-understandable concepts, but they typically rely on exhaustive annotations and treat concepts as flat and independent. To circumvent this, recent work has introduced *Hierarchical Concept Embedding Models* (HiCEMs) to explicitly model concept relationships, and *Concept Splitting* to discover sub-concepts using only coarse annotations.

- **Problem**: Concept-based models explain predictions using human-understandable concepts, but they typically rely on exhaustive annotations and treat concepts as flat and independent.
- **Approach**: However, both methods are restricted to shallow hierarchies.
- **Results**: We overcome this limitation with *Multi-Level Concept Splitting* (MLCS), which discovers multi-level concept hierarchies from only top-level supervision, and *Deep-HiCEMs*, an architecture that represents these discovered hierarchies and enables interventions at multiple levels of abstraction.
- **Impact**: Experiments show that MLCS discovers human-interpretable concepts absent during training and that Deep-HiCEMs maintain high accuracy while supporting test-time concept interventions that can improve task performance..

## Abstract

Concept-based models explain predictions using human-understandable concepts, but they typically rely on exhaustive annotations and treat concepts as flat and independent. To circumvent this, recent work has introduced *Hierarchical Concept Embedding Models* (HiCEMs) to explicitly model concept relationships, and *Concept Splitting* to discover sub-concepts using only coarse annotations. However, both methods are restricted to shallow hierarchies. We overcome this limitation with *Multi-Level Concept Splitting* (MLCS), which discovers multi-level concept hierarchies from only top-level supervision, and *Deep-HiCEMs*, an architecture that represents these discovered hierarchies and enables interventions at multiple levels of abstraction. Experiments show that MLCS discovers human-interpretable concepts absent during training and that Deep-HiCEMs maintain high accuracy while supporting test-time concept interventions that can improve task performance.


## Implementation Notes

- **OpenReview:** [GGBRe4yegd](https://openreview.net/forum?id=GGBRe4yegd)
- **Venue:** UCRL@ICLR2026 Poster
