---
title: "Stochastic Thermodynamics"
type: concept
tags:
  - physics
  - thermodynamics
  - diffusion-models
  - free-energy
  - information-theory
related:
  - "wiki/concepts/spontaneous-symmetry-breaking.md"
  - "wiki/concepts/deep-learning-theory.md"
  - "wiki/concepts/ai-for-materials.md"
  - "wiki/articles/welling-physics-ai-materials-talk.md"
sources:
  - "raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/"
---

# Stochastic Thermodynamics

Stochastic thermodynamics extends classical thermodynamics to small, far-from-equilibrium systems where fluctuations matter. It provides exact equalities — not just inequalities — for quantities like entropy production, work, and free energy along individual stochastic trajectories. The mathematics turns out to be virtually identical to probabilistic AI methods.

## Key ideas

- **Crooks' fluctuation theorem**: The ratio of forward and time-reversed path probabilities equals $e^{\sigma_{\text{tot}}}$, where $\sigma_{\text{tot}}$ is the total entropy production. This is exact, not an approximation.
- **Jarzynski equality**: $\langle e^{-W} \rangle = e^{-\Delta F}$ — averaging the exponential of negative work over many non-equilibrium trajectories yields the equilibrium free energy difference. Discovered independently of (but equivalent to) annealed importance sampling in ML (Radford Neal).
- **Dissipated work bound**: Recent results show $W_{\text{diss}} \geq \mathcal{W}_2^2(p_0, p_T) / T$, where $\mathcal{W}_2$ is the 2-Wasserstein distance. This implies a fundamental speed-energy trade-off: faster distribution changes require more energy — a potential limit on the speed of "thought" in neural systems.
- **Time-reversal symmetry breaking**: At the microscopic level, physics is time-reversible. Stochastic thermodynamics describes systems where this symmetry is broken, leading to entropy production and information loss — described by the same Markov chain mathematics used in AI.

## Connection to machine learning

Max Welling's [ICLR 2026 invited talk](../../raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/README.md) presents a detailed dictionary between ML and physics concepts:

| Machine Learning | Stochastic Thermodynamics |
|:---|:---|
| Variational free energy / ELBO | Thermodynamic free energy |
| E-step (minimize over $q$) | Relaxation (entropy/heat generation) |
| M-step (learning) | Performing work on the system |
| Diffusion models | Non-equilibrium thermodynamic processes |
| Stochastic normalizing flows | Escorted free energy estimation |
| Optimal transport CNFs | Counter-diabatic driving |
| Annealed importance sampling | Jarzynski equality |

The original diffusion model paper (Sohl-Dickstein et al.) was titled "Deep Unsupervised Learning Using Non-equilibrium Thermodynamics," making the connection explicit from the start.

## Application: free energy estimation for drug discovery

The Jarzynski equality enables estimation of binding free energies — how strongly a drug-like molecule binds to a protein target. The approach: train a flow matching model to drive molecular configurations between unbound and bound states, measure work along each trajectory, and compute $\Delta F$ via the Jarzynski equality. The generalized Jarzynski equality with optimal transport paths achieves theoretically zero-variance estimates.

## Sources

- [Max Welling invited talk](../../raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/README.md) — Detailed exposition of the ML–physics dictionary and free energy applications

## Related concepts

- [Spontaneous Symmetry Breaking](spontaneous-symmetry-breaking.md) — Another physics principle applied to AI
- [AI for Materials](ai-for-materials.md) — Application domain for free energy methods
- [Deep Learning Theory](deep-learning-theory.md) — Theoretical foundations
