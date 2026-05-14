# Papers

Summaries of research papers, primarily from ICLR 2026. Created using the **`paper-summary`** skill.

## Categories

### Deep Learning Theory

- [There Will Be a Scientific Theory of Deep Learning](there-will-be-a-scientific-theory-of-deep-learning.md) — Manifesto proposing "learning mechanics" as the emerging scientific theory of deep learning, organized around five lines of evidence
- [Transformers are Inherently Succinct](transformers-are-inherently-succinct.md) — Fixed-precision transformers are exponentially more succinct than LTL/RNNs and doubly exponentially more succinct than finite automata; verification is EXPSPACE-complete
- [Poly-attention: A general scheme for higher-order self-attention](poly-attention-higher-order.md)

### LLM Evaluation

- [LLMs Get Lost In Multi-Turn Conversation](llms-get-lost-in-multi-turn-conversation.md) — All 15 tested LLMs show ~39% performance drop in multi-turn underspecified conversations, driven by unreliability doubling (+112%) rather than aptitude loss; Outstanding Paper Award at ICLR 2026
- [What's In My Human Feedback? Learning Interpretable Descriptions of Preference Data](whats-in-my-human-feedback.md)
- [Query Timing Produces Opposite Positional Biases Between LLMs and Humans](query-timing-positional-biases.md)
- [When Can You TRUST Large Language Models?](when-can-you-trust-llms.md)
- [CoDeC: Detecting Data Contamination in LLMs via In-Context Learning](codec-data-contamination-detection.md)
- [Challenges in Inference-Time Scaling with Uncertainty-Aware Tree Search](uncertainty-aware-tree-search.md)
- [The Anatomy of Uncertainty in LLMs](anatomy-of-uncertainty-llms.md)
- [How Reliable is Language Model Micro-Benchmarking?](language-model-micro-benchmarking.md)
- [AdAEM: An Adaptively and Automated Extensible Measurement of LLMs' Value Difference](adaem-llm-value-measurement.md)
- [EigenBench: A Comparative Behavioral Measure of Value Alignment](eigenbench-value-alignment.md)

### Generative Models

- [ABC: Any-Subset Autoregression via Non-Markovian Diffusion Bridges in Continuous Time and Space](abc-any-subset-autoregression-non-markovian-diffusion-bridges.md) — Continual SDE generative model with data-to-data transitions, time-adaptive volatility, and path-dependent conditioning for continuous-time stochastic processes (video, weather)
- [Beyond Single Tokens: Distilling Discrete Diffusion Models via Discrete MMD](discrete-mmd-distilling-discrete-diffusion.md) — D-MMD generalizes moment matching distillation to discrete diffusion, producing few-step generators that outperform teachers on text and images
- [Concept Bottleneck Diffusion for Steerable Generation](concept-bottleneck-diffusion.md)

### Optimization

- [Fantastic Pretraining Optimizers 2.1: Hyperball Optimization](hyperp-hypersphere-scaling.md) — Hyperball meta-optimizer: norm-constrained updates enabling stable hyperparameter transfer across model scales
- [Rethinking Language Model Scaling under Transferable Hypersphere Optimization](hyperp-hypersphere-parameterization.md) — HyperP framework: first LR transfer laws across width, depth, tokens, and MoE granularity under Frobenius-sphere constraint with Muon
- [Controlled LLM Training on Spectral Sphere](spectral-sphere-optimizer.md) — Spectral Sphere Optimizer (SSO): steepest descent on spectral manifold with full μP alignment, outperforming AdamW and Muon on Dense 1.7B, MoE 8B, and DeepNet 200L
- [How LR Decay Wastes Your Best Data in Curriculum-Based LLM Pretraining](lr-decay-curriculum-pretraining.md)
- [Sharpness-Aware Pretraining Mitigates Catastrophic Forgetting](sharpness-aware-pretraining.md)

### Computer Vision

- [Retain and Adapt: Auto-Balanced Model Editing for Open-Vocabulary Object Detection under Domain Shifts](retain-and-adapt-model-editing.md)

### Fairness & Bias

- [WRING Out the Bias: A Rotation-Based Alternative to Projection Debiasing](wring-out-the-bias.md)

### Interpretability

- [There Was Never a Bottleneck in Concept Bottleneck Models](no-bottleneck-concept-bottleneck-models.md)
- [Simulating Concept Bottlenecks with Vision-Language Models](simulating-concept-bottlenecks-vlm.md)
- [An Information-Theoretic Approach to Benign Leakage in Static Concept Embedding Models](info-theoretic-benign-leakage.md)
- [Digging Deeper: Learning Multi-Level Concept Hierarchies](digging-deeper-concept-hierarchies.md)

### LLM Safety & Alignment

- [Model Collapse Is Not a Bug but a Feature in Machine Unlearning for LLMs](model-collapse-machine-unlearning.md)
- [The Missing Red Line: How Commercial Pressure Erodes AI Safety Boundaries](missing-red-line-ai-safety.md)
- [Beyond Prompt-Induced Lies: Investigating LLM Deception on Benign Prompts](beyond-prompt-induced-lies.md)
- [Is it Thinking or Cheating? Detecting Implicit Reward Hacking by Measuring Reasoning Effort](trace-reward-hacking-detection.md)

### Representation Learning

- [Extracting Representations in LLMs Robust to Distribution Shifts](extracting-representations-llms-distribution-shifts.md)
