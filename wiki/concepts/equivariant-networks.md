---
title: "Equivariant Networks"
type: concept
tags:
  - equivariance
  - symmetry
  - graph-neural-networks
  - AI-for-science
related:
  - "wiki/concepts/spontaneous-symmetry-breaking.md"
  - "wiki/concepts/deep-learning-theory.md"
  - "wiki/concepts/ai-for-materials.md"
  - "wiki/articles/welling-physics-ai-materials-talk.md"
sources:
  - "raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/"
---

# Equivariant Networks

Equivariant neural networks are architectures whose outputs transform predictably under symmetry transformations of their inputs. If a transformation $g$ is applied to the input, the network's output transforms by a corresponding (possibly different) representation of $g$, rather than producing an arbitrary change. Convolutional neural networks are the prototypical example: translating the input translates the feature maps by the same amount.

## Key ideas

- **Formal definition**: A function $f$ is equivariant to a group $G$ if $f(g \cdot x) = g \cdot f(x)$ for all $g \in G$. When the output representation is trivial (i.e., $g \cdot f(x) = f(x)$), the function is *invariant*.
- **Group equivariant CNNs**: Taco Cohen and Max Welling (2016) generalized CNNs to be equivariant under discrete groups beyond translations — rotations, reflections, and other symmetries — by using group convolutions.
- **Steerable networks and fiber bundles**: Extensions handle continuous groups (SO(3), SE(3)) using steerable filters and representations from harmonic analysis.
- **Geometric deep learning**: The unifying framework (Bronstein et al., 2021) views equivariance as the central design principle for networks on graphs, meshes, point clouds, and manifolds.

## Applications in AI for science

Equivariance has been especially impactful in scientific applications where physical symmetries are known a priori:

- **Machine learning interatomic potentials (MLIPs)**: Equivariant GNNs learn atomic force fields that respect rotational and translational symmetry, enabling molecular dynamics simulations orders of magnitude faster than quantum mechanical calculations.
- **Molecular generation**: Equivariant generative models (diffusion, flow matching) generate 3D molecular structures that respect SE(3) symmetry.
- **Weather modeling**: Spherical equivariant architectures respect the rotational symmetry of atmospheric data.

## Ten years of symmetries in AI

Max Welling's [ICLR 2026 invited talk](../../raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/README.md) celebrates a decade since group equivariant CNNs, noting the field now has a comprehensive textbook (Maurice Weiler). He argues the next frontier is [spontaneous symmetry breaking](spontaneous-symmetry-breaking.md) — going beyond hardwired equivariance to networks that dynamically break symmetries in service of computation.

## Sources

- [Max Welling invited talk](../../raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/README.md) — Retrospective on 10 years of equivariance and future directions

## Related concepts

- [Spontaneous Symmetry Breaking](spontaneous-symmetry-breaking.md) — The next chapter after equivariance
- [Deep Learning Theory](deep-learning-theory.md) — Theoretical foundations
- [AI for Materials](ai-for-materials.md) — Primary application domain
