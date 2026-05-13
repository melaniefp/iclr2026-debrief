---
title: "Neural Scaling Laws"
type: concept
tags:
  - deep-learning-theory
  - scaling
  - language-models
related:
  - "wiki/concepts/deep-learning-theory.md"
  - "wiki/concepts/marin-project.md"
  - "wiki/concepts/open-source-ai.md"
  - "wiki/concepts/hyperball-optimizer.md"
  - "wiki/articles/marin-open-development-frontier-ai.md"
sources:
  - "raw/iclr-2026-workshop-sci4dl/README.md"
  - "raw/iclr-2026-invited-talk-marin-open-development-frontier-ai-talk/"
  - "raw/learningmechanics-pub.md"
  - "raw/fantastic-pretraining-optimizers-weight-norm-theory.md"
  - "wiki/papers/hyperp-hypersphere-parameterization.md"
---

# Neural Scaling Laws

Neural scaling laws describe the empirical power-law relationships between model performance and factors such as model size, dataset size, and compute budget. At Sci4DL (ICLR 2026), Matthieu Wyart presented on deriving neural scaling laws from the statistics of natural language, and Bruno Loureiro contributed a talk on optimal scaling laws for hierarchical multi-index models. These results connect statistical physics approaches with practical scaling behavior observed in large language models.

In his ICLR 2026 invited talk, Percy Liang demonstrated the practical application of scaling laws through the Marin project. Key insights include: scaling laws don't happen automatically — they require a well-designed **scaling recipe** (a function from compute budget to hyperparameters); the Chinchilla isoflop methodology can be extended to predict loss at 300× larger scale when paired with stable optimizers; and algorithmic efficiency has been doubling approximately every eight months.

## Key ideas

- Performance follows power-law curves as model size, data, or compute increases
- Scaling exponents can be derived from properties of natural language statistics
- Statistical physics frameworks (e.g., hierarchical multi-index models) provide theoretical grounding for observed scaling behavior
- Understanding scaling laws helps predict the returns of increasing model or dataset size
- **Scaling recipes** map compute budgets to full hyperparameter configurations — they are a prerequisite for clean scaling laws
- **Isoflop curves** (Chinchilla method): sweep model sizes at fixed compute budgets, find optima, then fit a power law for extrapolation
- Hyperparameters like learning rate are scale-dependent (e.g., optimal LR decreases as $n^{-0.3}$ with token count), but this dependence is itself predictable
- Optimizers that stabilize hyperparameters across scales (e.g., hyperball optimizer) dramatically improve scaling law reliability
- The "magic exponent" 0.32 for optimal LR vs. token count appears universal across optimizers (observed for both AdamW and MuonH under Frobenius-sphere constraint)

## Sources

- [Sci4DL Workshop (ICLR 2026)](../../raw/iclr-2026-workshop-sci4dl/README.md)
- [Marin invited talk (transcript + slides)](../../raw/iclr-2026-invited-talk-marin-open-development-frontier-ai-talk/README.md) — scaling recipes, isoflop methodology, 300× extrapolation, preregistration
- [HyperP paper](../papers/hyperp-hypersphere-parameterization.md) — Ren et al. (2026): confirms the 0.32 data-scaling exponent under hypersphere optimization and demonstrates 1.58× CEL

## Related concepts

- [Deep Learning Theory](deep-learning-theory.md)
- [Marin Project](marin-project.md)
- [Open-Source AI](open-source-ai.md)
