---
title: "Spontaneous Symmetry Breaking"
type: concept
tags:
  - physics
  - deep-learning-theory
  - symmetry
  - equivariance
related:
  - "wiki/concepts/equivariant-networks.md"
  - "wiki/concepts/deep-learning-theory.md"
  - "wiki/articles/welling-physics-ai-materials-talk.md"
sources:
  - "raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/"
---

# Spontaneous Symmetry Breaking

Spontaneous symmetry breaking (SSB) occurs when a system with a symmetric energy landscape settles into an asymmetric ground state — not because an external force breaks the symmetry, but because the symmetric state is unstable. In physics, classic examples include a liquid crystallizing into a solid (breaking continuous translational symmetry into discrete symmetry) and the Higgs mechanism in quantum field theory.

## Key ideas

- **Explicit vs. spontaneous breaking**: Explicit breaking requires an external perturbation that selects a direction. Spontaneous breaking occurs when the symmetric state is a local maximum — any perturbation causes the system to fall into one of many equivalent asymmetric ground states.
- **Goldstone modes**: When a continuous symmetry is spontaneously broken, the system gains zero-energy excitations called Goldstone modes — oscillations along the "flat" directions of the energy landscape. These waves propagate without dispersion, preserving information over long distances.
- **Higgs modes**: Oscillations perpendicular to the Goldstone direction require energy and exhibit dispersion — information mixes across frequencies and is lost.
- **Phase transitions**: SSB is the mechanism behind phase transitions (liquid → crystal, paramagnet → ferromagnet). The transition point is characterized by a critical temperature or coupling strength.

## In deep learning

Max Welling argues in his [ICLR 2026 invited talk](../../raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/README.md) that SSB may be "at the root of modern AI." His proposal:

1. **Capsule networks with internal symmetries**: Neurons carry internal degrees of freedom (vectors on spheres). The network's equivariance ensures that rotating internal phases in the input layer rotates all downstream phases consistently.
2. **Edge of chaos**: When randomly initialized networks cross a critical variance threshold, the internal sphere representations undergo a phase transition from collapsing to expanding — analogous to the ordered-to-broken phase transition. Networks perform best at this transition point.
3. **Wave-based memory**: In the broken phase, Goldstone modes create traveling waves through network layers that preserve information over long spatiotemporal distances. This provides a natural mechanism for long-term memory without explicit memory modules.
4. **Preliminary results**: RNNs with internal sphere structure outperform standard RNNs and GRUs on memory-intensive tasks (permuted MNIST, copy task, adding task) with fewer parameters.

This connects to neuroscience: multi-electrode recordings show that the brain uses traveling waves for information propagation, and operates at the edge of chaos.

## Sources

- [Max Welling invited talk](../../raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/README.md) — Primary exposition of SSB in neural networks, with live demonstration

## Related concepts

- [Equivariant Networks](equivariant-networks.md) — SSB presupposes a symmetry to break
- [Deep Learning Theory](deep-learning-theory.md) — Edge of chaos and information propagation
