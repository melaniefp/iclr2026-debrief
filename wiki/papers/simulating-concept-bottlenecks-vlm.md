---
title: "Simulating Concept Bottlenecks with Vision-Language Models"
authors: "Karim Galliamov, Ivan Titov, Ilya Pershin"
affiliations: "University of Amsterdam, University of Edinburgh, Innopolis University"
url: "https://openreview.net/forum?id=aswvIu1Vgw"
date: "2026-04-23"
category: "Interpretability"
raw_source: "raw/sim-concept-bottleneck-openreview.md"
keywords:
  - concept-bottleneck-models
  - vision-language-models
  - VLMs
  - explainability
---

# Simulating Concept Bottlenecks with Vision-Language Models

## Summary

TL;DR: The paper shows how to turn a vision-language model into a concept bottleneck model by fine-tuning it to describe an image's concepts in natural language.

- **Problem**: Concept Bottleneck Models (CBMs) enhance transparency by first predicting human-interpretable concepts before producing the final decision, allowing experts to inspect and correct intermediate reasoning.
- **Approach**: We introduce LangCBM, which uses VLMs to generate textual descriptions of visual concepts, followed by a lightweight extraction and classification pipeline.
- **Results**: Training via supervised fine-tuning (SFT), optionally followed by reinforcement learning (RL), yields accurate concept predictions.
- **Impact**: Across synthetic and real-world benchmarks, LangCBM achieves competitive concept and label accuracy, as well as high post-intervention accuracy compared to alternative CBM formulations, establishing VLM-generated text as a viable, interpretable bottleneck representation.

**TL;DR:** The paper shows how to turn a vision-language model into a concept bottleneck model by fine-tuning it to describe an image's concepts in natural language..

## Abstract

Concept Bottleneck Models (CBMs) enhance transparency by first predicting human-interpretable concepts before producing the final decision, allowing experts to inspect and correct intermediate reasoning. We demonstrate that large vision–language models (VLMs) can naturally support this paradigm and act as a concept bottleneck by leveraging their parametric knowledge and generative capabilities. We introduce LangCBM, which uses VLMs to generate textual descriptions of visual concepts, followed by a lightweight extraction and classification pipeline. Training via supervised fine-tuning (SFT), optionally followed by reinforcement learning (RL), yields accurate concept predictions. Across synthetic and real-world benchmarks, LangCBM achieves competitive concept and label accuracy, as well as high post-intervention accuracy compared to alternative CBM formulations, establishing VLM-generated text as a viable, interpretable bottleneck representation.

**TL;DR:** The paper shows how to turn a vision-language model into a concept bottleneck model by fine-tuning it to describe an image's concepts in natural language.


## Implementation Notes

- **OpenReview:** [aswvIu1Vgw](https://openreview.net/forum?id=aswvIu1Vgw)
- **Venue:** UCRL@ICLR2026 Poster
