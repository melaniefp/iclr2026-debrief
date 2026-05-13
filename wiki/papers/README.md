# Papers

Summaries of research papers, primarily from ICLR 2026. Created using the **`paper-summary`** skill.

## Categories

### Deep Learning Theory

- [There Will Be a Scientific Theory of Deep Learning](there-will-be-a-scientific-theory-of-deep-learning.md) — Manifesto proposing "learning mechanics" as the emerging scientific theory of deep learning, organized around five lines of evidence

### Generative Models

- [ABC: Any-Subset Autoregression via Non-Markovian Diffusion Bridges in Continuous Time and Space](abc-any-subset-autoregression-non-markovian-diffusion-bridges.md) — Continual SDE generative model with data-to-data transitions, time-adaptive volatility, and path-dependent conditioning for continuous-time stochastic processes (video, weather)
- [Beyond Single Tokens: Distilling Discrete Diffusion Models via Discrete MMD](discrete-mmd-distilling-discrete-diffusion.md) — D-MMD generalizes moment matching distillation to discrete diffusion, producing few-step generators that outperform teachers on text and images

### Optimization

- [Fantastic Pretraining Optimizers 2.1: Hyperball Optimization](hyperp-hypersphere-scaling.md) — Hyperball meta-optimizer: norm-constrained updates enabling stable hyperparameter transfer across model scales
- [Rethinking Language Model Scaling under Transferable Hypersphere Optimization](hyperp-hypersphere-parameterization.md) — HyperP framework: first LR transfer laws across width, depth, tokens, and MoE granularity under Frobenius-sphere constraint with Muon
- [Controlled LLM Training on Spectral Sphere](spectral-sphere-optimizer.md) — Spectral Sphere Optimizer (SSO): steepest descent on spectral manifold with full μP alignment, outperforming AdamW and Muon on Dense 1.7B, MoE 8B, and DeepNet 200L
