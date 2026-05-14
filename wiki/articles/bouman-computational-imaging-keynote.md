---
title: "Katherine Bouman on Computational Imaging — Summary"
type: "article"
tags: [iclr-2026, keynote, computational-imaging, inverse-problems, ai-for-science, uncertainty-estimation]
related: []
sources: ["raw/iclr-2026-schedule-day2-fri.md"]
---

# Katherine Bouman on Computational Imaging

## Overview

Katherine Bouman's keynote presents scientific imaging as a canonical example of AI working under uncertainty rather
than in spite of it.

Her schedule abstract for [ICLR day 2](../../raw/iclr-2026-schedule-day2-fri.md) centers on a striking idea: some of the
most iconic scientific images are not direct snapshots.

They are reconstructions inferred from incomplete, indirect, and physically constrained measurements.

The black hole image is the flagship case.

Bouman emphasizes that confidence in that image did not come from a single reconstruction pipeline magically producing
the "right" answer.

It came from consistency across many reconstructions applied to the same sparse data.

That framing makes the talk highly relevant to machine learning.

Computational imaging is an inverse problem, but it is also a model-selection problem, a prior-design problem, and an
uncertainty quantification problem.

Simple assumptions can take us far.

But at some point, those assumptions become the limiting factor in what the data can reveal.

Bouman's proposal is that machine learning helps by enriching the space of admissible priors while preserving respect
for known physics.

Rather than replacing scientific reasoning, ML broadens the set of plausible worlds consistent with the measurements.

That is why the talk naturally connects to interpretability, uncertainty estimation, concept representation learning,
causal inference, and world models for science.

## Key Points

### Scientific images are often inferred, not captured

Bouman begins with a useful demystification.

A scientific image is frequently not what a conventional camera would record.

It is the result of solving an inverse problem from partial, noisy, or fundamentally indirect data.

The Event Horizon Telescope is the emblematic case.

No single telescope can directly image a distant black hole at the required resolution.

Instead, scientists combine sparse interferometric measurements with physical constraints and computational
reconstruction.

This matters because it changes what "seeing" means.

The task is not passive registration.

It is structured inference.

Once framed that way, computational imaging looks much closer to probabilistic modeling than to simple picture taking.

### Confidence comes from consistency across reconstructions

A core sentence in the abstract says that confidence came not from one image, but from the consistency of features
across many reconstructions of the same data.

That is the keynote's strongest uncertainty lesson.

Bouman is pushing back against the temptation to equate one plausible output with epistemic certainty.

The more principled move is to examine what remains stable across different assumptions, algorithms, and priors.

In effect, the talk treats robustness across reconstruction families as evidence about which image features are
trustworthy.

That is highly aligned with modern ML concerns.

When a model output changes sharply under small prior changes, that instability should itself be part of the scientific
result.

### Physics is the scaffold, not the competitor

The talk does not present physics and machine learning as opposing approaches.

Physics provides the forward model, the measurement process, and the structural constraints that keep inference
grounded.

Machine learning becomes useful when simple hand-designed priors stop being expressive enough.

This is an important balance.

Physics prevents the model from hallucinating unconstrained explanations.

Machine learning expands the family of structured hypotheses that can explain the data.

That combination is particularly attractive in scientific settings where pure end-to-end performance is not enough.

Researchers need reconstructions that remain interpretable in terms of known measurement operators and domain
assumptions.

### Simple priors help, but they also hide possibilities

Bouman's abstract explicitly says that simple assumptions can take us far, but also limit what we can learn.

This is a subtle and important claim.

A simple prior regularizes an ill-posed inverse problem.

But it also narrows the hypothesis class.

That means apparent certainty can be purchased by prematurely excluding real possibilities.

The ML translation is direct.

A strong prior can stabilize inference while simultaneously biasing it.

Bouman's keynote appears to advocate a middle path: use richer learned priors to explore a fuller set of possibilities,
while still calibrating them against expected physics.

### ML expands the posterior, not just the point estimate

One of the most useful phrases in the abstract is that learned assumptions let us "explore a full range of
possibilities" consistent with differing strengths of expected physics.

That suggests the keynote is not merely about producing sharper images.

It is about characterizing a space of candidate explanations.

This is a broad lesson for AI for science.

In many scientific applications, we should care less about one polished prediction and more about the structure of the
posterior: which features are inevitable, which are prior-sensitive, and which remain unresolved.

That is where computational imaging meets uncertainty estimation in a deep way.

### Black hole imaging is the motivating case, not the endpoint

Bouman uses black holes because the example is vivid, but the abstract is careful to generalize.

The same logic applies to imaging technologies we rely on every day.

It also extends to other scientific domains, including gravitational lensing for dark matter mapping.

This expansion matters.

The keynote is really about a general recipe for inference from partial data: combine a mechanistic observation model
with flexible learned structure, and then reason carefully about what features are robust.

That is a transferable template for astronomy, microscopy, medical imaging, and remote sensing.

### The talk implicitly argues for scientific world models

Although the abstract does not use the term "world model," the logic is close to it.

A forward physics model tells us how an underlying scene or state would generate observations.

A learned prior represents what kinds of scenes are plausible.

Inference combines the two.

That is essentially a domain-grounded world model: a latent representation of the world constrained by how measurements
arise.

What distinguishes Bouman's framing from generic generative modeling is that the latent world is tied to physical
observables and scientific use-cases.

## Connections to Research Interests

### Interpretability

Bouman's talk is interpretability-friendly because the reconstruction process is explicitly factorized into measurement
model, physics assumptions, and learned priors.

That makes it possible to ask which part of the pipeline is responsible for a particular visual conclusion.

In AI for science, that kind of structured interpretability is often more valuable than a single high-level explanation.

### Human-AI feedback loops

Scientific imaging contains an expert-in-the-loop feedback process.

Researchers choose priors, inspect reconstructions, compare alternative solutions, and refine the modeling assumptions.

The ML system does not terminate human judgment.

It reorganizes it.

Bouman's insistence on consistency across reconstructions can be read as a call for better human-AI scientific feedback
loops rather than one-shot automation.

### Uncertainty estimation

This is the keynote's clearest connection.

Confidence is treated as stability across reconstructions, not mere sharpness of a final image.

That is a strong message for generative modeling generally.

When the data are incomplete, we need representations of uncertainty over latent structure, not just prettier outputs.

### Concept representation learning

Learned priors in computational imaging effectively encode concepts of what natural, physical, or domain-valid
structures look like.

Those concepts may be edges, textures, shapes, or higher-level morphological patterns.

The keynote suggests that richer concept representations enable extraction of signal that simpler regularizers miss.

### Causal inference

Inverse problems are not causal inference in the narrow experimental sense, but they do involve reasoning from
observations back to latent generating states.

In scientific applications, that often supports downstream causal hypotheses.

For example, reconstructing dark matter distributions from lensing observations is a step toward understanding the
underlying structure of the universe, not just predicting pixels.

### Robotics and world models

The robotics connection is indirect but real.

Any embodied system that must infer hidden state from partial sensory data faces an inverse problem.

Bouman's framework suggests how world models should be built when sensors are sparse, noisy, and physically constrained.

### Steering techniques

In this setting, steering means choosing priors, regularizers, and physics strengths in ways that change the solution
set.

Bouman's talk is a reminder that steering in scientific ML should usually be transparent and hypothesis-driven, not
purely reward-driven.

## Takeaways

- Bouman frames computational imaging as structured inference from incomplete measurements rather than straightforward
  picture taking.
- The black hole example highlights a robust notion of confidence: stable features across multiple reconstructions
  matter more than any single iconic image.
- Physics and machine learning play complementary roles. Physics anchors inference; learned priors widen the range of
  admissible explanations.
- The keynote is fundamentally about uncertainty-aware AI for science.
- For research interests in interpretability, world models, and concept learning, computational imaging is a clean and
  consequential case study.
