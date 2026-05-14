---
title: "Concept Representation Learning"
type: "concept"
tags: [concept-learning, representation-learning, interpretability, causal-representation-learning]
related:
  - "wiki/summaries/iclr-2026-workshop-unicrl-concept-representation.md"
  - "wiki/concepts/concept-bottleneck-models.md"
  - "wiki/concepts/mechanistic-interpretability.md"
  - "wiki/articles/icbinb-llms-workshop.md"
  - "wiki/papers/extracting-representations-llms-distribution-shifts.md"
  - "wiki/papers/digging-deeper-concept-hierarchies.md"
sources:
  - "raw/iclr-2026-workshop-unicrl-concept-representation.md"
  - "raw/info-theoretic-leakage-openreview.md"
  - "raw/digging-deeper-openreview.md"
  - "raw/extracting-repr-openreview.md"
  - "raw/sim-concept-bottleneck-openreview.md"
---

# Concept Representation Learning

## Definition

Concept representation learning is the problem of discovering or constructing
latent variables that correspond to semantically meaningful, reusable, and often
intervenable abstractions. Rather than treating representations as opaque
features, this line of work asks whether models can organize knowledge into units
that line up with human concepts, causal factors, or stable task structure.

The [UniCRL workshop capture](../../raw/iclr-2026-workshop-unicrl-concept-representation.md)
shows how broad this agenda became at ICLR 2026. It explicitly brought together
neuro-symbolic AI, explainability, and causal representation learning, treating
concepts as the shared interface between perception, reasoning, and human
interaction.

In the repo, this concept sits upstream of both
[Concept Bottleneck Models](concept-bottleneck-models.md) and
[Mechanistic Interpretability](mechanistic-interpretability.md). The former asks
how to build systems around named concepts; the latter often asks how to recover
concept-like structure from already-trained systems.

## Key Ideas

- **High-quality concepts should be stable and useful**: semantics alone are not
  enough if the representation fails under distribution shift or intervention.
- **Leakage is a representational problem**: if a concept carries unrelated
  information, it ceases to be a clean abstraction.
- **Hierarchy matters**: concepts often live at multiple levels of granularity,
  from coarse labels to fine-grained sub-concepts.
- **Different modalities need different interfaces**: concepts may be scalar,
  textual, visual, or latent directions inside LLM activations.
- **Robustness reveals concept quality**: CARE-style invariant and environment-
  specific decompositions test whether a concept generalizes across contexts.
- **Causal and symbolic agendas meet here**: concepts are often the units on
  which explanation, intervention, and reasoning can agree.

## Related Work at ICLR 2026

- The [UniCRL workshop](../../raw/iclr-2026-workshop-unicrl-concept-representation.md)
  explicitly frames concepts as the lingua franca linking XAI, NeSy, and causal
  representation learning.
- [Extracting Representations in LLMs Robust to Distribution Shifts](../papers/extracting-representations-llms-distribution-shifts.md)
  proposes CARE, separating invariant concept directions from context-specific
  variation.
- [Digging Deeper: Learning Multi-Level Concept Hierarchies](../papers/digging-deeper-concept-hierarchies.md)
  pushes concept learning beyond flat taxonomies.
- [An Information-Theoretic Approach to Benign Leakage in Static Concept
  Embedding Models](../papers/info-theoretic-benign-leakage.md) studies when
  leakage is harmful, limited, or performance-preserving.
- [Simulating Concept Bottlenecks with Vision-Language Models](../papers/simulating-concept-bottlenecks-vlm.md)
  shows that natural-language descriptions can themselves be concept carriers.

## Open Questions

- What makes a learned concept “good” enough for intervention or symbolic use?
- How should concept quality be evaluated across modalities and levels of
  abstraction?
- Can causal, linguistic, and visual concepts share one common representational
  space without becoming too vague?
- When do robust representations require multiple context-specific directions
  rather than one universal concept axis?
