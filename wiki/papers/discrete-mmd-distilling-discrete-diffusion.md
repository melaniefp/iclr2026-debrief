---
title: "Beyond Single Tokens: Distilling Discrete Diffusion Models via Discrete MMD"
authors: "Emiel Hoogeboom, David Ruhe, Jonathan Heek, Thomas Mensink, Tim Salimans"
affiliations: "Google DeepMind Amsterdam"
url: "https://arxiv.org/abs/2603.20155"
date: "2026-03-20"
category: "Generative Models"
raw_source: "raw/discrete-mmd-distilling-discrete-diffusion-src/"
keywords:
  - discrete diffusion distillation
  - moment matching distillation
  - few-step generation
  - gradient moment metric
---

# Beyond Single Tokens: Distilling Discrete Diffusion Models via Discrete MMD

## Summary

TL;DR: D-MMD generalizes continuous moment matching distillation to discrete diffusion, producing few-step generators that outperform their teachers on both text (Open Web Text) and image (CIFAR-10) generation, while also introducing a new gradient-based evaluation metric for discrete diffusion samples.

- **D-MMD reformulates continuous MMD as a general min-max objective** over arbitrary loss functions, enabling application to discrete diffusion processes (masked and uniform) without requiring an ODE or continuous score.
- **Distilled generators consistently outperform their teachers** — on CIFAR-10, a 32-step uniform D-MMD achieves FID 3.7 vs. the 1024-step teacher's 7.5; on text, a 16-step masked D-MMD achieves GPT-2 Gradient Moment 0.236 vs. the 512-step teacher's 0.275.
- **A new evaluation metric (GPT-2 Gradient Moment)** uses the squared norm of the centered loss gradient of a reference LM to measure distributional distance, addressing failure modes of generative perplexity.
- **Factorized generators learn correlated outputs** by collapsing their soft output distributions — input noise conditioning helps masked diffusion generators achieve this collapse more effectively.
- **Students can outperform teachers** because D-MMD's adversarial component induces mild mode-seeking behavior (akin to reverse-KL), concentrating density near modes without full collapse.

## Contributions

### 1. Generalized min-max formulation of MMD (D-MMD)

The core contribution is rewriting the alternating MMD optimization into a general min-max loss ([Section 3](https://arxiv.org/html/2603.20155#S3)):

$$
\mathcal{L}_{\text{D-MMD}}(\eta) = \min_\eta \max_\phi \mathbb{E}_{g_\eta(z_t, x, s, z_s)}\left[L_s(x, \hat{x}_\theta(z_s), z_s) - L_s(x, \hat{x}_\phi(z_s), z_s) - L_s(\hat{x}_\theta(z_s), \hat{x}_\phi(z_s), z_s)\right]
$$

The generator minimizes loss under the teacher while maximizing loss under the auxiliary model. This formulation is **equivalent to continuous MMD** when $L_s$ is the squared error ([Section 3](https://arxiv.org/html/2603.20155#S3)), but generalizes to the cross-entropy loss used in discrete diffusion.

For discrete diffusion specifically, since there is no gradient through the categorical sample, soft probability vectors $\hat{x}_\eta(z_t)$ are used instead of hard samples. The generator loss simplifies to ([Section 3](https://arxiv.org/html/2603.20155#S3)):

$$
\mathcal{L}_{\text{GEN}}(\eta) = \text{CE}(\hat{x}_\eta | \hat{x}_\theta(z_s)) - \text{CE}(\hat{x}_\eta | \hat{x}_\phi(z_s)) = -\sum_c (\hat{x}_\eta)_c (\log \hat{x}_\theta(z_s) - \log \hat{x}_\phi(z_s))_c
$$

Previous discrete distillation methods like SDTT use progressive distillation which fundamentally cannot represent correlated distributions (e.g., perfectly correlated coin tosses). Di4C addresses this with mixture outputs but scales exponentially. D-MMD avoids both issues by using the generator itself as the mixture, while keeping factorized outputs.

### 2. Gradient Moment evaluation metric

The paper proposes measuring sample quality via the squared norm of the centered gradient of a reference LM ([Section 5](https://arxiv.org/html/2603.20155#S5)):

$$
\lVert \mathbb{E}_g[\nabla_\theta \log p_\theta^{\text{LLM}}(x)] - \mathbb{E}_q[\nabla_\theta \log p_\theta^{\text{LLM}}(x)] \rVert^2
$$

If an AR model trained to convergence has zero gradient on its training data, then a nonzero gradient on generated samples indicates distributional mismatch. The metric is estimated via an unbiased inner-product estimator on independent minibatch pairs ([Equation in Section 5](https://arxiv.org/html/2603.20155#S5.E2)). This addresses the known failure of generative perplexity, which can assign good scores to collapsed/repetitive text.

### 3. Correlated outputs from factorized generators

The paper explains ([Section 3.1](https://arxiv.org/html/2603.20155#S3.SS1)) how a factorized model learns correlations: the generator is a composition of (1) a stochastic function producing soft samples $\hat{x}_\eta(z_t)$, and (2) a factorized categorical sampling step. Only the second step is factorized — the soft samples can encode correlations. To minimize the MMD loss, the generator must reduce its output entropy, concentrating probability on correlated configurations.

### 4. Temperature and top-p distillation

D-MMD incorporates mode-seeking teacher modifications during distillation ([Section 3.4](https://arxiv.org/html/2603.20155#S3.SS4)). For top-p, a key practical contribution is avoiding gradient explosion: instead of masking logits to $-10^{20}$, they dynamically lower logits by a constant $\Delta = 2$, preventing divergence while maintaining the top-p effect.

## Empirical findings

### CIFAR-10 (unconditional image generation, 3072 tokens at 256 vocab)

Results from [Table 1](https://arxiv.org/html/2603.20155#S5.T1):

| Model | Steps | FID ↓ |
|-------|-------|-------|
| Uniform Teacher | 1024 | 7.5 |
| Uniform D-MMD | 32 | **3.7** |
| Masked Teacher | 1024 | 6.4 |
| Masked D-MMD | 64 | **3.5** |

D-MMD achieves roughly **2× better FID at 16–64× fewer steps**. Note that continuous diffusion models achieve FID ~3 on CIFAR-10, so discrete D-MMD is approaching parity.

### Open Web Text (unconditional text generation, 1024 tokens)

Results from [Table 2](https://arxiv.org/html/2603.20155#S5.T2):

| Model | Steps | GPT-2 GM ↓ |
|-------|-------|-------------|
| Masked Teacher (p=0.85) | 512 | 0.275 |
| Masked D-MMD (p=0.85) | 16 | 0.236 |
| Masked D-MMD (p=0.85) | 32 | **0.225** |
| AR Baseline | — | 0.061 |

The 16-step D-MMD already outperforms the 512-step teacher. A gap to AR models remains (0.225 vs 0.061).

### Block autoregressive diffusion

From [Table 3](https://arxiv.org/html/2603.20155#S5.T3): a 16-step D-MMD matches the 256-step teacher (GPT-2 GM 0.225) in a block-AR setup with block size 256.

### Comparison with prior discrete distillation methods

From [Table 5](https://arxiv.org/html/2603.20155#S5.T5):
- CIFAR-10: D-MMD (8 steps, FID 5.0) outperforms Di4C (10 steps, FID 20.6; 20 steps hybrid, FID 9.5).
- Text: SDTT shows degradation over distillation rounds (GPT-2 GM 0.293–0.340 at 32–64 steps), while D-MMD achieves 0.225–0.236 at 16–32 steps.

### Ablation: noise conditioning ([Table 6](https://arxiv.org/html/2603.20155#S5.T6))

For masked diffusion, input noise conditioning is critical: without it, FID at 4 steps is 151 vs. 22.3 with noise. The noise source allows the generator to collapse its output entropy further (1.01 vs. 1.26 at 4 steps), enabling stronger correlations. Uniform diffusion does not benefit, likely because $z_t$ already provides sufficient randomness.

### Why students outperform teachers

The paper explains ([Section 5.6](https://arxiv.org/html/2603.20155#S5.SS6)) that teacher models are trained with maximum likelihood (mode-covering). D-MMD's adversarial component induces mode-seeking behavior, concentrating density near modes without full collapse. A paradoxical consequence: student performance eventually degrades at very high step counts, converging back to teacher performance.

## Notes from summaries of related work

The ABC paper summary in this knowledge base covers non-Markovian diffusion bridges for continuous generative modeling — a different approach to improving diffusion sampling. D-MMD is complementary, focusing on distillation of existing discrete diffusion models rather than novel architectures.

The [flow maps](../concepts/flow-maps.md) concept page covers the broader landscape of diffusion distillation methods, noting that discrete diffusion distillation (including D-MMD) faces fundamental limitations from token independence assumptions that continuous flow maps avoid.

No prior summaries of SDTT, Di4C, DiMO, or MDLM are available in the knowledge base for direct comparison.

## Implementation notes

- **Framework**: Google DeepMind internal infrastructure (JAX/Flax likely, based on authors' prior work)
- **Teacher architectures**: Not fully specified but use transformer-based discrete diffusion models
- **Training**: Alternating optimization between generator and auxiliary model (even/odd steps)
- **Key hyperparameters**: top-p for temperature distillation ($\Delta = 2$ for safe top-p masking), noise pyramid for masked diffusion conditioning
- **Reference metric model**: GPT-2 (publicly available)
- **Datasets**: CIFAR-10 (images, 32×32×3, 256-class vocabulary), Open Web Text (text, 1024 tokens)
- **Concurrent work**: IDLM proposes a similar framework but generates full $x$ and diffuses back to $z_t$, whereas D-MMD samples from the posterior $q(z_s | z_t, x)$
- **No public code repository** mentioned in the paper
