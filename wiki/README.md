# Wiki

Curated knowledge base for ICLR 2026 research. Contains paper summaries, concept definitions, short summaries of raw captures, and longer-form synthesis articles — all cross-linked into a unified knowledge graph with references back to source material in [`raw/`](../raw/).

## Structure

```
wiki/
  papers/      # Paper summaries with contributions, findings, and notes
  concepts/    # Concept articles defining key ideas, methods, and topics
  summaries/   # Short summaries of individual raw/ entries
  articles/    # Longer-form articles synthesizing multiple sources into topic overviews
```

## Conventions

- Use standard markdown links (`[text](path)`) for all cross-references
- Every file **must** have YAML frontmatter (see schema below)
- Backlinks should be bidirectional: if A links to B, B should link back to A
- Concept pages are the backbone — they connect papers, raw captures, and articles

## Frontmatter schema

```yaml
---
title: "Concept or article title"
type: "concept | summary | article"
tags:
  - tag1
  - tag2
related:
  - "wiki/concepts/linked-concept.md"
sources:
  - "raw/slug.md"
  - "wiki/papers/paper-title.md"
---
```

### Field reference

| Field     | Required | Description                                        |
|-----------|----------|----------------------------------------------------|
| `title`   | ✅       | Title of the wiki page                              |
| `type`    | ✅       | One of: `concept`, `summary`, `article`             |
| `tags`    | ✅       | List of topic tags for indexing                     |
| `related` |          | Links to related wiki pages                         |
| `sources` |          | Links to source material in `raw/` or `wiki/papers/`  |

## Index

### Concepts

- [AI for Materials](concepts/ai-for-materials.md) — AI-driven materials discovery, ML force fields, and CuspAI
- [Consistency Models](concepts/consistency-models.md) — Flow maps anchored to t=0 enabling single-step diffusion sampling
- [Deep Learning Theory](concepts/deep-learning-theory.md) — Why deep networks generalize and how optimization enables training
- [Edge of Stability](concepts/edge-of-stability.md) — Hessian eigenvalue dynamics at the stability threshold during training
- [Equivariant Networks](concepts/equivariant-networks.md) — Architectures with built-in symmetry constraints (translation, rotation, SE(3))
- [Flow Maps](concepts/flow-maps.md) — Neural networks predicting the integral of diffusion velocity fields for few-step sampling
- [Hyperball Optimizer](concepts/hyperball-optimizer.md) — Hypersphere-constrained optimizer enabling stable hyperparameter transfer across scales
- [Knowledge Distillation](concepts/knowledge-distillation.md) — Transferring knowledge from teacher to student models via soft targets and distribution matching
- [Marin Project](concepts/marin-project.md) — Openly-developed frontier language model with scaling recipes and preregistration
- [Mechanistic Interpretability](concepts/mechanistic-interpretability.md) — Reverse-engineering internal computations of neural networks
- [Neural Scaling Laws](concepts/neural-scaling-laws.md) — Power-law relationships between model performance, size, and compute
- [On-Policy Distillation](concepts/on-policy-distillation.md) — Dense token-level supervision from teachers via reverse KL on student rollouts (OPD/MOPD)
- [Open-Source AI](concepts/open-source-ai.md) — Spectrum of openness from closed APIs to open development
- [Spontaneous Symmetry Breaking](concepts/spontaneous-symmetry-breaking.md) — Phase transitions and wave-based memory in neural networks
- [Stochastic Thermodynamics](concepts/stochastic-thermodynamics.md) — Non-equilibrium physics meets probabilistic AI and diffusion models

### Summaries

#### Conference schedules
- [ICLR 2026 Conference Schedule](summaries/iclr-2026-conference-schedule.md) — Source: [raw/iclr-2026-conference-schedule.md](../raw/iclr-2026-conference-schedule.md)

#### Workshop captures
- [Sci4DL Workshop](summaries/iclr-2026-workshop-sci4dl.md) — Source: [raw/iclr-2026-workshop-sci4dl/](../raw/iclr-2026-workshop-sci4dl/README.md)

#### Blogs and websites
- [Flow Maps: Learning the integral of a diffusion model](summaries/flow-maps-learning-integral-diffusion-model.md) — Source: [raw/flow-maps-learning-integral-diffusion-model.md](../raw/flow-maps-learning-integral-diffusion-model.md)
- [Multi-Teacher On-Policy Distillation](summaries/multi-teacher-on-policy-distillation.md) — Source: [raw/multi-teacher-on-policy-distillation-new-post-training.md](../raw/multi-teacher-on-policy-distillation-new-post-training.md)
- [Learning Mechanics Blog](summaries/learningmechanics-pub.md) — Source: [raw/learningmechanics-pub.md](../raw/learningmechanics-pub.md)
- [Hyperball Optimization (Fantastic Optimizers 2.1)](summaries/fantastic-pretraining-optimizers-hyperball.md) — Source: [raw/fantastic-pretraining-optimizers-hyperball.md](../raw/fantastic-pretraining-optimizers-hyperball.md)
- [Weight Norm Theory (Fantastic Optimizers 2.2)](summaries/fantastic-pretraining-optimizers-weight-norm-theory.md) — Source: [raw/fantastic-pretraining-optimizers-weight-norm-theory.md](../raw/fantastic-pretraining-optimizers-weight-norm-theory.md)

#### Invited talks
- [Marin: Open Development of Frontier AI](summaries/iclr-2026-invited-talk-marin.md) — Source: [Percy Liang invited talk](../raw/iclr-2026-invited-talk-marin-open-development-frontier-ai-talk/README.md)
- [From Physics to AI to Materials](summaries/iclr-2026-invited-talk-welling.md) — Source: [Max Welling invited talk](../raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/README.md)

### Articles

- [How Does Gradient Descent Actually Work? Jeremy Cohen on the Edge of Stability](articles/edge-of-stability-cohen-talk.md) — Deep dive into Cohen's Sci4DL talk on self-stabilization dynamics
- [Marin: How Open Development and Scaling Recipes Are Changing Frontier AI](articles/marin-open-development-frontier-ai.md) — Synthesis of Percy Liang's ICLR 2026 keynote on scaling recipes, preregistration, and open development
- [From Physics to AI to Materials: Max Welling's ICLR 2026 Keynote](articles/welling-physics-ai-materials-talk.md) — Synthesis of Welling's talk on symmetry breaking, stochastic thermodynamics, and CuspAI
- [Some Insights into LLM Reasoning: Julia Kempe on Why RL Unlocks Chain-of-Thought](articles/kempe-llm-reasoning-insights.md) — Synthesis of Kempe's Sci4DL talk on RLVF mechanisms, length calibration, and self-play curriculum

## Maintaining the wiki

- **`wiki-update`** skill — Scans for new content and updates summaries, concepts, and backlinks
- **`wiki-article`** skill — Synthesizes multiple sources into a longer-form article
