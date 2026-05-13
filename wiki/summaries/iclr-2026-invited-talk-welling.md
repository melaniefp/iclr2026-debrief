---
title: "Summary: From Physics to AI to Materials — Max Welling (ICLR 2026)"
type: summary
tags:
  - invited-talk
  - physics
  - symmetry-breaking
  - equivariance
  - thermodynamics
  - materials-science
  - AI-for-science
related:
  - "wiki/concepts/spontaneous-symmetry-breaking.md"
  - "wiki/concepts/equivariant-networks.md"
  - "wiki/concepts/stochastic-thermodynamics.md"
  - "wiki/concepts/ai-for-materials.md"
  - "wiki/concepts/deep-learning-theory.md"
  - "wiki/articles/welling-physics-ai-materials-talk.md"
sources:
  - "raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/"
---

# Summary: From Physics to AI to Materials — Max Welling (ICLR 2026)

Max Welling argues that the ML community should reward paradigm-shifting ideas over incremental engineering, and demonstrates how physics principles can inspire fundamentally new AI methods with real-world impact.

## Part 1: Spontaneous symmetry breaking and waves in neural networks

Welling celebrates 10 years of [equivariant networks](../concepts/equivariant-networks.md), starting with Taco Cohen's 2016 group equivariant CNNs. He then proposes a new framework based on [spontaneous symmetry breaking](../concepts/spontaneous-symmetry-breaking.md) — the physics phenomenon where a symmetric system settles into an asymmetric ground state. Through a live demonstration with a stick, he shows the difference between explicit and spontaneous symmetry breaking, and introduces Goldstone modes: zero-energy oscillations that arise in the broken phase and can propagate information over long distances without loss.

Building on earlier work with Kuramoto oscillators and wave-based RNNs, Welling proposes "capsule" networks with internal structure (spins on spheres). When these networks operate at the edge of chaos — which he notes is also where the brain operates — information propagates through hundreds or thousands of layers via wave-like dynamics. Preliminary results show these symmetry-equipped RNNs outperform standard architectures on memory-intensive tasks with fewer parameters.

## Part 2: Stochastic thermodynamics and AI

Welling draws a deep analogy between probabilistic AI and [stochastic thermodynamics](../concepts/stochastic-thermodynamics.md). Key connections include: Crooks' fluctuation theorem relating forward/backward path distributions to entropy production; the Jarzynski equality enabling free energy estimation from non-equilibrium work measurements; and the equivalence between variational free energy (ELBO) in machine learning and thermodynamic free energy. He highlights a recent result showing that dissipated work is lower-bounded by the squared Wasserstein distance divided by time — suggesting a fundamental limit to the speed of "thought" (distribution changes in neural representations).

He applies this to drug discovery: using flow matching models to drive molecular dynamics simulations, then estimating binding free energies via the Jarzynski equality. Optimal transport paths reduce the high variance of naive estimators to theoretically zero.

## Part 3: CuspAI and AI for materials

Welling describes his startup [CuspAI](../concepts/ai-for-materials.md), which builds a platform for AI-driven materials discovery. The system works as a "search engine for materials" — a user provides property requirements, an agent orchestrates generative models and multi-scale simulations, and candidates are validated experimentally. He announces the open-source release of a JAX-based molecular dynamics toolkit (developed with NVIDIA), enabling GPU-native batched simulations with compiled machine learning force fields.

## Epilogue: Responsibility

Welling closes by comparing AI researchers to Oppenheimer — developers of a powerful dual-use technology. He urges the community to make conscious choices about their work and not look away from its consequences.
