---
title: "There Will Be a Scientific Theory of Deep Learning"
authors: "Jamie Simon, Daniel Kunin, Alexander Atanasov, Enric Boix-Adserà, Blake Bordelon, Jeremy Cohen, Nikhil Ghosh, Florentin Guth, Arthur Jacot, Mason Kamb, Dhruva Karkada, Eric J. Michaud, Berkan Ottlik, Joseph Turnbull"
affiliations: "UC Berkeley, Stanford, MIT, Harvard, Meta FAIR, CMU, NYU, EPFL"
url: "https://arxiv.org/abs/2604.21691"
date: "2026-04-23"
category: "Deep Learning Theory"
raw_source: "raw/there-will-be-a-scientific-theory-of-deep-learning-src/"
keywords:
  - learning mechanics
  - deep learning theory
  - neural scaling laws
  - edge of stability
---

# There Will Be a Scientific Theory of Deep Learning

## Summary

TL;DR: A manifesto-style paper arguing that a scientific theory of deep learning — termed "learning mechanics" — is emerging, organized around five lines of evidence: solvable models, tractable limits, empirical laws, hyperparameter theories, and universal behaviors.

Key takeaways:

- The paper proposes the name **learning mechanics** for the emerging scientific theory of deep learning, drawing explicit parallels to classical, statistical, and continuum mechanics in physics.
- Five lines of evidence are presented that such a theory is coalescing: (a) analytically solvable settings, (b) insightful infinite-width/depth limits, (c) simple empirical laws like scaling laws and edge-of-stability, (d) hyperparameter theories (μP, curvature-penalized flows), and (e) universal behaviors across architectures.
- The paper articulates seven desiderata for learning mechanics: fundamental, mathematical, predictive, comprehensive, intuitive, useful, and humble.
- A symbiotic relationship between learning mechanics and mechanistic interpretability is proposed: learning mechanics as the "physics" and mech interp as the "biology" of deep learning.
- Ten open directions are identified as tractable targets for the next decade of research.

## Contributions

This is a position/survey paper rather than a technical contribution. Its main contributions are:

### 1. Framing: "Learning Mechanics" as a field name and research program ([Section 1](https://arxiv.org/html/2604.21691v1#S1))

The paper argues that the emerging theory of deep learning shares deep structural similarities with branches of mechanics in physics:
- Forces → gradients; movement through physical space → movement through parameter space
- Equilibria → convergence to loss minima; system parameters → hyperparameters
- Solvable toy models, tractable limits, macroscopic laws, and universality classes all have direct analogues

Seven desiderata are articulated ([Section 1](https://arxiv.org/html/2604.21691v1#S1)): the theory should be fundamental, mathematical, predictive, comprehensive, intuitive, useful, and humble.

### 2. Five lines of evidence ([Section 2](https://arxiv.org/html/2604.21691v1#S2))

#### (a) Analytically solvable settings ([Section 2.1](https://arxiv.org/html/2604.21691v1#S2.SS1))

- **Deep linear networks**: linearization in the data yields exactly solvable nonlinear dynamics; the learning dynamics decouple into independent Bernoulli ODEs showing sequential singular value learning (Saxe et al., 2013). The model captures greedy low-rank bias, saddle-dominated landscapes, and stepwise learning.
- **Neural tangent kernel (NTK)**: linearization in the parameters reduces training to kernel ridge regression, connecting architecture to inductive bias through the NTK eigenstructure (Jacot et al., 2018).

#### (b) Insightful limits ([Section 2.2](https://arxiv.org/html/2604.21691v1#S2.SS2))

- The infinite-width limit yields two qualitatively different regimes depending on initialization scaling:
  - **Lazy/kernel regime** ($\text{width}^{-1/2}$ scaling): linearized, no feature learning, NTK description
  - **Rich/feature-learning regime** ($\text{width}^{-1}$ output scaling): features evolve, representations adapt to data structure
- The "Discretization Hypothesis": finite networks are discretized approximations to infinite-width/depth limits, with model size reducing discretization error.

#### (c) Simple empirical laws ([Section 2.3](https://arxiv.org/html/2604.21691v1#S2.SS3))

- **Neural scaling laws**: test loss follows power laws in compute, data, and model size (Kaplan et al., 2020). Origin of exponents remains unexplained.
- **Edge of stability**: sharpness (top Hessian eigenvalue) rises to $2/\eta$ and equilibrates there during full-batch gradient descent ([Figure 4](https://arxiv.org/html/2604.21691v1#S2.F4); Cohen et al., 2021). Progressive sharpening followed by plateau is universal across architectures.

#### (d) Hyperparameter theories ([Section 2.4](https://arxiv.org/html/2604.21691v1#S2.SS4))

- **Optimization hyperparameters**: Linear scaling rule (learning rate × batch size invariance) explained via SDE interpretation. Critical batch size concept. Curvature-penalized gradient flows (central flows) explain the role of learning rate.
- **Architecture hyperparameters (μP)**: Maximal Update Parameterization enables learning rate transfer across widths by ensuring order-one feature updates at any width. Validated on GPT-3 scale.

#### (e) Universal phenomena ([Section 2.5](https://arxiv.org/html/2604.21691v1#S2.SS5))

- Different architectures converge to similar learned distributions (e.g., diffusion models with UNet vs. ViT produce identical images from same seed)
- Large models across modalities develop increasingly similar internal representations ("Platonic Representation Hypothesis")
- Data itself exhibits universal structure (Zipf's law, power-law spectra)

### 3. Relationship to other perspectives ([Section 3](https://arxiv.org/html/2604.21691v1#S3))

The paper positions learning mechanics relative to:
- **Statistical perspective**: implicit bias + overparameterization → easy optimization, but needs mechanics to explain *how*
- **Information-theoretic perspective**: learning as compression, but needs mechanics to explain *implementation*
- **Physics of deep learning**: essentially the same community/goal
- **Neuroscience**: analogies to systems neuroscience and circuit-level analysis
- **Developmental interpretability/singular learning theory**: same goal, different toolkit
- **Mechanistic interpretability**: proposed symbiosis — mechanics provides the "physics" (quantitative laws of aggregate behavior), mech interp provides the "biology" (semantic decomposition into interpretable parts)

### 4. Responses to skepticism ([Section 4](https://arxiv.org/html/2604.21691v1#S4))

Addresses counterarguments: "decades of failure", "too primitive compared to LLMs", "too microscopic", "need theory of data not models", "AI will understand itself first". Key response: local theories of pieces of the stack are already useful (scaling laws, μP, data attribution), and identifying the right basic objects enables applied science even without complete theory.

### 5. Ten open directions ([Section 5](https://arxiv.org/html/2604.21691v1#S5))

1. Solvable models of genuinely deep, nonlinear learning
2. Theory capable of capturing natural data
3. Does deep learning minimize some notion of functional complexity?
4. Formal definition of "features" learned by neural networks
5. Are finite networks approximations to infinite limits? (Discretization Hypothesis)
6. Can we eliminate all hyperparameters?
7. Predict scaling law exponents *a priori*
8. How does loss curvature interplay with architecture, features, generalization?
9. What makes a good optimizer?
10. In what sense do large models learn similar representations?

## Empirical findings

This is primarily a position/survey paper and does not present new empirical results. However, it extensively cites and reproduces key empirical findings from the literature:

- [Figure 1](https://arxiv.org/html/2604.21691v1#S2.F1): Deep linear network dynamics showing sequential singular value learning (reproduced from Saxe et al., 2013) and NTK learning curves (from Simon et al., 2023)
- [Figure 2](https://arxiv.org/html/2604.21691v1#S2.F2): Lazy vs. rich training dynamics showing weight trajectories (reproduced from Chizat et al., 2019)
- [Figure 3](https://arxiv.org/html/2604.21691v1#S2.F3): Neural scaling laws as power laws in compute, data, and parameters (reproduced from Kaplan et al., 2020)
- [Figure 4](https://arxiv.org/html/2604.21691v1#S2.F4): Edge of stability — sharpness equilibrating at $2/\eta$ across architectures (reproduced from Cohen et al., 2021)
- [Figure 5](https://arxiv.org/html/2604.21691v1#S2.F5): μP enabling learning rate transfer across widths (reproduced from Yang et al., 2022)
- [Figure 6](https://arxiv.org/html/2604.21691v1#S2.F6): Universality across architectures (diffusion models) and data modalities (Platonic Representation Hypothesis)

## Notes from summaries of related work

This paper has strong connections to existing wiki content:

- **Edge of stability** ([wiki/concepts/edge-of-stability.md](../concepts/edge-of-stability.md)): The paper discusses edge of stability as one of the key "simple empirical laws" (Section 2.3) and connects it to the curvature regularization framework. Jeremy Cohen (co-author) presented this work at the [Sci4DL workshop](../articles/edge-of-stability-cohen-talk.md).
- **Neural scaling laws** ([wiki/concepts/neural-scaling-laws.md](../concepts/neural-scaling-laws.md)): Scaling laws are highlighted as the single most important empirical law in deep learning, with predicting their exponents identified as a key open problem.
- **Mechanistic interpretability** ([wiki/concepts/mechanistic-interpretability.md](../concepts/mechanistic-interpretability.md)): The paper proposes a detailed framework for symbiosis between learning mechanics and mech interp.
- **Learning Mechanics blog** ([raw/learningmechanics-pub.md](../../raw/learningmechanics-pub.md)): The companion website announced in this paper, hosting introductory blog posts on deep linear networks, quanta hypothesis, and perspectives essays.

## Implementation notes

- This is a position/survey paper; no code or algorithms to implement.
- Companion website: [learningmechanics.pub](https://learningmechanics.pub/) — hosts introductory materials, perspectives, and open questions.
- Open questions catalog: [learningmechanics.pub/openquestions](https://learningmechanics.pub/openquestions)
- Many co-authors maintain relevant codebases:
  - Central flows (Cohen et al.): [centralflows.github.io](http://centralflows.github.io)
  - μP (Yang et al.): referenced in Section 2.4
  - Quantization model (Michaud et al.): [arxiv.org/abs/2303.13506](https://arxiv.org/abs/2303.13506)
