---
title: "Marin Project"
type: concept
tags:
  - open-source
  - frontier-models
  - scaling-laws
  - language-models
  - preregistration
related:
  - "wiki/concepts/open-source-ai.md"
  - "wiki/concepts/neural-scaling-laws.md"
  - "wiki/concepts/hyperball-optimizer.md"
  - "wiki/articles/marin-open-development-frontier-ai.md"
sources:
  - "raw/iclr-2026-invited-talk-marin-open-development-frontier-ai-talk/"
---

# Marin Project

Marin is an openly-developed language model project led by Percy Liang at Stanford and OpenAthena. Its goal is to train the best language model possible given available resources — and to do so with full transparency, publishing every experiment, failure, and design decision on GitHub.

## Key ideas

- **Open development on GitHub**: Every experiment is conducted in public via GitHub issues and PRs. Community members can suggest ideas, review results, and even run experiments. This goes beyond open-source (releasing code + data) to making the research *process* itself open.
- **Scaling recipes over individual runs**: Rather than tuning hyperparameters per run, Marin develops functions that map compute budget → hyperparameter settings. This enables principled extrapolation from small-scale experiments to large-scale training.
- **Hyperball optimizer**: A key technical contribution — normalizes weight updates onto a hypersphere, providing explicit control over weight norms. Yields 20–30% speedups over Adam and Muon, with hyperparameters that transfer stably across model scales.
- **Preregistration**: Marin publicly posts predicted losses before large runs complete, inspired by scientific preregistration. Demonstrated 300× extrapolation (from small isoflop curves to large-scale runs) within 0.005 nats of predicted loss.
- **Mixture-of-experts**: After validating dense model scaling, Marin extended to MoE architectures, achieving 3.76× compute efficiency gains with further improvements from architecture ablations.
- **Cross-modal generalization**: The same scaling infrastructure and recipes have been applied to audio modeling and DNA sequence modeling, validating the generality of the approach.
- **Data strategy**: Accumulating 18T tokens from community-curated open datasets (DCLM, Nemotron CC, Hugging Face, etc.) with permissive licenses. Mixture and curriculum optimization is ongoing work.

## Timeline

- **November 2024**: First expedition — 8B parameter "YOLO" training run on DCLM data
- **2025**: Second expedition — 32B parameter model (best open-source base model briefly)
- **2025–2026**: Developed scaling recipes, hyperball optimizer, isoflop validation
- **April 2026**: ICLR 2026 invited talk; 120B parameter MoE run (16B active) in progress

## Sources

- [Marin invited talk (transcript + slides)](../../raw/iclr-2026-invited-talk-marin-open-development-frontier-ai-talk/README.md) — ICLR 2026 keynote with scaling recipe details, preregistration results, and Q&A

## Related concepts

- [Open-Source AI](open-source-ai.md)
- [Neural Scaling Laws](neural-scaling-laws.md)
