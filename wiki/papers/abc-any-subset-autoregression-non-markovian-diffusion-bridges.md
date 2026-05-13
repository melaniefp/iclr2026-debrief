---
title: "ABC: Any-Subset Autoregression via Non-Markovian Diffusion Bridges in Continuous Time and Space"
authors: "Gabe Guo, Thanawat Sornwanee, Lutong Hao, Elon Litman, Stefano Ermon, Jose Blanchet"
affiliations: "Stanford University"
url: "https://arxiv.org/abs/2604.27443"
date: "2026-04-30"
category: "Generative Models"
raw_source: "raw/abc-any-subset-autoregression-non-markovian-diffusion-bridges-src/"
keywords:
  - non-Markovian diffusion
  - any-subset autoregression
  - Doob h-transform
  - continuous-time generative models
---

# ABC: Any-Subset Autoregression via Non-Markovian Diffusion Bridges in Continuous Time and Space

## Summary

TL;DR: ABC models continuous-time stochastic processes (videos, weather) with a single continual SDE whose time and state track physical reality, using Doob h-transforms to derive data-to-data generative dynamics with time-adaptive volatility and path-dependent conditioning on arbitrary observation subsets.

- **Data-to-data transitions**: Unlike standard diffusion models that start from noise, ABC generates each future state starting from the previous (already-close) state, improving structural coherence and numerical stability.
- **Time-adaptive volatility**: The SDE's noise injection scales with physical time elapsed between states, so short time gaps produce small perturbations and long gaps allow larger changes — matching real process dynamics. Theorem 4 ([§4](https://arxiv.org/html/2604.27443v2#S4)) proves that chained diffusion bridges with a shared volatility schedule *cannot* reproduce the correct path measure.
- **Any-subset conditioning**: Via a non-Markovian, path-dependent score function, ABC conditions on arbitrary (possibly non-causal, irregularly sampled) subsets of observed states, generalizing both autoregressive and infilling tasks to continuous time and space.
- **Scalable training**: A path- and time-dependent extension of denoising score matching (Theorem 2, [§3.2](https://arxiv.org/html/2604.27443v2#S3.SS2)) provides a simulation-free training objective with closed-form Gaussian noising kernels from an OU base process.
- **Strong empirical results**: ABC outperforms conditional diffusion bridges (DDBM) and noise-to-data diffusion (SMLD) on video generation (CelebV-HQ, Sky Timelapse) and weather forecasting (SEVIR), with clear wins in both temporal consistency (FVD) and per-frame quality (FID).

## Contributions

### C1: Continual SDE for continuous-time, continuous-space autoregression ([§3](https://arxiv.org/html/2604.27443v2#S3))

ABC defines a single SDE over physical time $[0, t_L]$:

$$dX_t^{\text{new}} = \left[-a(t)X_t^{\text{new}} + \sigma(t)^2 s(t, X_t^{\text{new}}; \mathbf{X}_{0:i^*})\right]dt + \sigma(t)dB_t$$

where $a(t), \sigma(t)$ are base process coefficients and $s(t, x_t; \mathbf{x}_{0:i^*})$ is a path-dependent score function conditioned on previously generated states $\mathbf{x}_{0:i^*}$ (Theorem 1, [§3.1](https://arxiv.org/html/2604.27443v2#S3.SS1), Eq. 5). The score is derived via Doob h-transform: it changes the base measure $\mathbb{P}$ (an Ornstein-Uhlenbeck process) into $\mathbb{Q}$ such that the finite-dimensional distribution matches $p_{\text{data}}$.

Key distinction from prior work: the SDE time variable *is* the physical time, so transitions between adjacent states naturally start from data (not noise) and the volatility injected scales with the physical time gap. This contrasts with diffusion bridges that use an auxiliary time $\tau \in [0,1]$ with a fixed volatility schedule regardless of physical time elapsed.

### C2: Provably correct inductive biases — time-adaptive volatility ([§4](https://arxiv.org/html/2604.27443v2#S4))

**Theorem 4** ([§4](https://arxiv.org/html/2604.27443v2#S4)) proves that autoregressively chaining conditional diffusion bridges (as in DDBM or PFI) with a shared volatility schedule $\tilde{\sigma}(\tau)$ generally produces a process $Y$ whose path measure differs from ABC's continual SDE $X^{\text{new}}$ — they can be distinguished almost surely via their quadratic variation. Specifically, for generic time grids $0, t_1, \ldots, t_L$, the concatenated process $Y_t := \tilde{X}^{(i^*)}_{(t - t_{i^*})/(t_{i^*+1} - t_{i^*})}$ has mismatched quadratic variation because each bridge shares the same $\tilde{\sigma}$ regardless of the physical time span it covers.

This means chained bridges inject the same total volatility for a 5-second transition and a 5-hour transition, leading to artifacts like flickering frames.

### C3: Path-dependent denoising score matching ([§3.2](https://arxiv.org/html/2604.27443v2#S3.SS2))

**Theorem 2** derives the training objective:

$$\mathcal{L}_{\text{DSM}}(\hat{s}) = \mathbb{E}_{t \sim \mathcal{U}(0, t_{L-1})} \mathbb{E}_{p_{\text{data}}(x_0, \ldots, x_{t_{i^*+1}}), p_{\text{base}}(x_t | x_{t_{i^*+1}}, x_{t_{i^*}})} \left[\left\|\hat{s}(t, x_t; \mathbf{x}_{0:i^*}) - \nabla_{x_t} \log p_{\text{base}}(x_{t_{i^*+1}} | x_t)\right\|^2\right]$$

This generalizes standard denoising score matching to the non-Markovian case: the score network takes the full observed path history $\mathbf{x}_{0:i^*}$ as input, and the noising kernel $p_{\text{base}}(x_t | x_{t_{i^*}}, x_{t_{i^*+1}})$ is a Gaussian bridge kernel from the OU base process with closed-form mean and variance (Lemma 1, [Appendix B](https://arxiv.org/html/2604.27443v2#A1)).

### C4: Any-subset (non-causal) conditioning ([§3.3](https://arxiv.org/html/2604.27443v2#S3.SS3))

For non-causal conditioning (e.g., knowing both first and last frames), the score function is extended to $s(t, x_t; \mathbf{x}_{0:i^*}, \mathcal{O})$ where $\mathcal{O}$ denotes future observations. A residual Brownian bridge parameterization (Eq. 12, [§3.3](https://arxiv.org/html/2604.27443v2#S3.SS3)) ensures the process hits future constraints:

$$\mathbf{f}_{\theta^*}(t, x_t, \ldots) = \mathbf{f}_{\theta^*}^{\text{res}}(t, x_t, \ldots) + \nabla_{x_t} \log p_{\text{base}}(x_{t_{i^{\mathcal{O}_{>t}}}} | x_t)$$

where $t_{i^{\mathcal{O}_{>t}}}$ is the next future constraint time. As $t$ approaches this constraint, the Brownian bridge drift dominates, steering the process to the known future state.

## Empirical findings

### Video generation — non-causal conditioning

**CelebV-HQ** ([Table 2](https://arxiv.org/html/2604.27443v2#S6.T2), 2048 videos): ABC (No BB, $\sigma=0.5$) achieves the best FVD across most settings, e.g., FVD = 40.5 (32 frames, pin every 4, 250 steps) vs. 49.0 for the best conditional bridge ($\sigma=0.09$) and 705.5 for noise-to-data diffusion. Noise-to-data methods are uncompetitive (FVD 434–1206).

**Sky Timelapse** ([Table 1](https://arxiv.org/html/2604.27443v2#S6.T1), 1360 videos): ABC (No BB, $\sigma=0.4$) achieves FVD = 62.1 (32 frames, pin every 4, 250 steps). Conditional bridges with $\sigma=0.3$ are sometimes competitive on FVD alone but produce flickering artifacts visible in FID scores. In overall FVD+FID ranking, ABC clearly prevails.

### Video generation — causal conditioning

ABC achieves Pareto optimality across FVD and FID for strictly causal generation on both datasets ([§D.3](https://arxiv.org/html/2604.27443v2#A4.SS3), [§D.5](https://arxiv.org/html/2604.27443v2#A4.SS5)), despite training primarily on non-causal conditioning. This demonstrates the framework's flexibility.

### Weather forecasting — SEVIR VIL

[Table 3](https://arxiv.org/html/2604.27443v2#S6.T3) (847 test clips): ABC Non-causal achieves the best performance across all metrics:
- MAE: 18.24 (vs. 36.06 noise-to-data, 55.90 conditional bridge)
- RMSE: 34.85 (vs. 63.05, 88.84)
- CSI at all thresholds (e.g., CSI₇₄ = 0.699 vs. 0.436, 0.204)

ABC Causal also outperforms both baselines, ranking second overall.

### Ablation: conditioning depth ([§D.1](https://arxiv.org/html/2604.27443v2#A4.SS1))

Conditioning ablations ([Tables 6–9](https://arxiv.org/html/2604.27443v2#A4.SS1)) show that full autoregressive conditioning on all past waypoints substantially outperforms conditioning on only the most recent state or only the initial frame. This validates the path-dependent (non-Markovian) formulation.

### Ablation: sensitivity to $\sigma$ ([§D.6](https://arxiv.org/html/2604.27443v2#A4.SS6))

ABC is relatively robust across $\sigma \in \{0.3, 0.4, 0.5, 0.6\}$, while conditional diffusion bridges are more sensitive to this hyperparameter choice.

### Toy experiment ([§6](https://arxiv.org/html/2604.27443v2#S6))

[Figure 2](https://arxiv.org/html/2604.27443v2#S6.F2) illustrates Theorem 4 on Brownian motion pinned at $B(4/5)=-1, B(1)=B(0)=+1$: chained diffusion bridges match marginals but have incorrect quadratic variation, while ABC's continual SDE correctly captures dynamics.

## Notes from summaries of related work

No directly related paper summaries exist in the knowledge base. The paper positions itself against:

- **DDBM** (Zhou et al.) — Denoising diffusion bridge models that use auxiliary time $\tau \in [0,1]$ and shared volatility schedules. ABC generalizes these by using physical time directly.
- **PFI** (Chen et al.) — Probabilistic forecasting with stochastic interpolants; ABC shows this is essentially equivalent to chained conditional diffusion bridges.
- **SMLD/DDPM** (Song et al., Ho et al.) — Standard score-based/denoising diffusion models that map noise to data. ABC's data-to-data approach provides better inductive bias for time series.

## Implementation notes

- **Architecture**: Extended DiT (Diffusion Transformer) with cross-attention for image-based conditioning. The noisy latent $x_t$ is patchified and processed with transformer blocks; conditioning frames enter via cross-attention. All compared methods use the same architecture.
- **Training**: Sample $L \sim \mathcal{U}[1, 16]$ conditioning frames per clip; first frame always conditioned on; remaining frames sampled uniformly (irregular times). Random subsets of future frames included for non-causal training.
- **Inference**: Euler-Maruyama discretization with 250 or 500 steps over $[0, 1]$. For non-causal conditioning, frames are pinned every $K \in \{4, 8, 16\}$ frames.
- **Base process**: Ornstein-Uhlenbeck SDE with constant $a(t) = 0$ (pure Brownian motion) and constant $\sigma$.
- **Datasets**: CelebV-HQ (face videos), Sky Timelapse (sky videos), SEVIR VIL (weather radar).
- **Code**: [https://github.com/gabeguo/abc_diffusion](https://github.com/gabeguo/abc_diffusion)
- **Project page**: [https://abc-diffusion.github.io/](https://abc-diffusion.github.io/)
