---
title: "Controlled LLM Training on Spectral Sphere"
authors: "Tian Xie, Haoming Luo, Haoyu Tang, Yiwen Hu, Jason Klein Liu, Qingnan Ren, Yang Wang, Wayne Xin Zhao, Rui Yan, Bing Su, Chong Luo, Baining Guo"
affiliations: "Microsoft Research Asia, Renmin University, Wuhan University, IQuest Research"
url: "https://arxiv.org/abs/2601.08393"
date: "2026-01-13"
category: "Optimization"
raw_source: "raw/spectral-sphere-optimizer-src/"
keywords:
  - spectral-sphere-optimizer
  - muP
  - manifold-optimization
  - LLM-training-stability
---

# Controlled LLM Training on Spectral Sphere

## Summary

**TL;DR:** The Spectral Sphere Optimizer (SSO) constrains both weight matrices and their updates to lie on a spectral sphere, unifying steepest descent under the spectral norm with strict μP alignment — yielding faster convergence and fundamentally stable activations compared to AdamW and Muon.

- **SSO enforces full μP compliance** by constraining both the spectral norm of weights ($\|\mathbf{W}\|_2 = R$) and of the update direction ($\|\Phi\|_2 = 1$), unlike Muon which only constrains updates. This eliminates weight drift and removes the need for weight decay on hidden 2D parameters.
- **The optimizer derives the steepest descent direction on the spectral sphere** via a tangent-space constraint and Lagrange multiplier search (bisection), yielding a mathematically unique update direction that combines maximal convergence speed with manifold stability.
- **Practical stability benefits emerge naturally**: bounded activations ($\Theta(1)$ RMS throughout training), improved MoE router load balancing, suppressed outliers in deep networks, and stable μP learning rate transfer across 25× width scaling.
- **SSO consistently outperforms baselines** on Dense 1.7B (19% fewer steps to match AdamW loss), MoE 8B-A1B, and 200-layer DeepNet models, at ~11.5% overhead relative to Muon on NVIDIA B200.
- **MuonSphere** (SSO with λ=0, i.e., no tangent projection) is offered as a cheaper variant that still provides spectral weight constraint with minimal overhead (~1% over Muon).

## Contributions

### 1. Spectral Sphere formulation unifying convergence and stability

The core insight is that Muon is "half-aligned" with μP: it constrains updates via the matrix sign function ($\operatorname{msign}$) but leaves weights unconstrained, causing activation drift over long training runs. SSO adds the constraint $\|\mathbf{W}\|_2 = R$ where $R = \Theta(\sqrt{d_{\text{out}}/d_{\text{in}}})$ ([Section 3.1, Eq. 1](https://arxiv.org/html/2601.08393#S3.E1)).

The optimization problem is ([Eq. 2](https://arxiv.org/html/2601.08393#S3.E2)):

$$\max_{\Phi} \langle \mathbf{G}, \Phi \rangle \quad \text{s.t.} \quad \|\Phi\|_2 = 1, \quad \|\mathbf{W} - \eta R \Phi\|_2 = R$$

### 2. Tangent-space projection via Lagrange multiplier search

A first-order Taylor expansion of the spectral norm yields the tangent constraint $\langle \Theta, \Phi \rangle = 0$ where $\Theta = \mathbf{u}_1 \mathbf{v}_1^\top$ is the gradient of the spectral norm ([Section 3.2, Eq. 4](https://arxiv.org/html/2601.08393#S3.E4)). The analytical solution is:

$$\Phi^*(\lambda) = \operatorname{msign}(\mathbf{G} + \lambda \Theta)$$

where $\lambda^*$ is the unique root of the monotonic function $h(\lambda) = \langle \Theta, \operatorname{msign}(\mathbf{G} + \lambda \Theta) \rangle$, found by bracket-and-bisect ([Eq. 5](https://arxiv.org/html/2601.08393#S3.E5)). The root is bounded in $[-2\|\mathbf{G}\|_*, 2\|\mathbf{G}\|_*]$ ([Appendix A.2](https://arxiv.org/html/2601.08393#A1.SS2)).

### 3. Retraction step eliminates weight decay

After the tangent-space update, a retraction $\mathbf{W} \gets \mathbf{W} \cdot R / \|\mathbf{W}\|_2$ projects back onto the spectral sphere ([Eq. 7](https://arxiv.org/html/2601.08393#S3.E7)). Since this strictly constrains $\|\mathbf{W}\|_2 = R$, weight decay becomes redundant for 2D hidden weights ([Section 3.3](https://arxiv.org/html/2601.08393#S3.SS3)).

### 4. Spectral μP learning rate scaler

The paper proposes $R = c\sqrt{d_{\text{out}}/d_{\text{in}}}$ as the LR scaler derived from the RMS-to-RMS operator norm invariance condition. Ablations show this outperforms the Align-Adam-RMS scaler used in Kimi Moonlight (uniform 0.2 RMS alignment) and the Spectral Kaiming scaler ([Section 4.2, Fig. 6](https://arxiv.org/html/2601.08393#S4.F6)).

### 5. Atomic module granularity

Fused QKV and gate/up matrices are split into independent spectral units (per-head for attention). Splitting QKV per-head yields the most significant gain ([Section 4.3, Fig. 7](https://arxiv.org/html/2601.08393#S4.F7)).

### 6. Efficient Megatron implementation

The paper provides a full systems recipe: atomic module sharding, ping-pong load balancing, adaptive kernel dispatch (JIT PyTorch for <512, Triton SYRK for ≥512), multi-stream parallelism, BF16 power iteration with FP32 msign, and singular vector caching. Total optimization reduces naive SSO overhead by 29.9% ([Section 5, Table 3](https://arxiv.org/html/2601.08393#S5.T3)).

## Empirical findings

### Dense 1.7B (Qwen3-1.7B architecture, 100B tokens OLMo-Mix-1124)

| Optimizer | Val Loss | LAMBADA PPL | Avg Acc (8 tasks) |
|-----------|----------|-------------|-------------------|
| AdamW | 2.588 | 5.40 | 54.75 |
| Muon | — | 5.05 | 55.26 |
| MuonSphere | — | **4.87** | 56.19 |
| Spectral Sphere | — | 5.00 | **56.35** |

Spectral Sphere reaches AdamW's final val loss in **19% fewer steps**; Muon in 12% fewer steps ([Figure 3](https://arxiv.org/html/2601.08393#S6.F3), [Table 1](https://arxiv.org/html/2601.08393#S6.T1)). Notably, the LR was tuned for AdamW (5e-3), not the spectral optimizers which prefer higher rates (1e-2).

### MoE 8B-A1B (DeepSeek-V3 style, 64 experts top-4 + 1 shared)

Spectral Sphere achieves the lowest validation loss and best expert load balance (lowest MaxVio). AdamW shows substantially larger MaxVio with frequent spikes, indicating unstable routing ([Figure 4](https://arxiv.org/html/2601.08393#S6.F4)).

### DeepNet 200-Layer (stress test)

Under extreme depth (200 layers), AdamW shows pronounced instability with frequent loss spikes. Spectral Sphere attains both the lowest loss and highest stability ([Figure 5](https://arxiv.org/html/2601.08393#S6.F5)).

### μP Width Transfer (70M → 1.8B, 25× scaling)

Muon shows notable optimal LR drift across widths despite μP, while Spectral Sphere achieves stable LR transfer and lower optimal loss at all scales ([Figure 2](https://arxiv.org/html/2601.08393#S2.F2)).

### Activation stability

AdamW attention AbsMax and FFN RMS reach ~100× magnitude compared to spectral optimizers. Spectral Sphere maintains constant activation magnitudes throughout training ([Figure 1](https://arxiv.org/html/2601.08393#S1.F1)).

### Overhead

On NVIDIA B200 with 4M tokens/step, SSO adds 11.45% latency over Muon (7666ms vs 6879ms). MuonSphere adds only 1.03% ([Table 4](https://arxiv.org/html/2601.08393#S5.T4)).

### Ablations

- **Radius scale** $c$: $c=2.0$ is optimal; AbsMax follows radius monotonically, RMS follows power-law scaling ([Figure 5, Section 4.1](https://arxiv.org/html/2601.08393#S4.F5))
- **LR scaler**: Spectral μP > Align-Adam-RMS > Spectral Kaiming ([Figure 6](https://arxiv.org/html/2601.08393#S4.F6))
- **Module granularity**: Per-head QKV split most impactful ([Figure 7](https://arxiv.org/html/2601.08393#S4.F7))
- **Weight decay**: Retraction makes WD redundant; ablations on 1.7B suggest disabling WD may be slightly better

## Notes from summaries of related work

The closely related [Hyperball Optimizer](hyperp-hypersphere-scaling.md) paper by Wen et al. (Stanford) constrains weight Frobenius norm rather than spectral norm. Both papers share the insight that explicit norm control eliminates weight decay and enables hyperparameter transfer. Key differences:
- **Norm choice**: Hyperball uses Frobenius norm (all singular values contribute equally); SSO uses spectral norm (only the top singular value is constrained, allowing internal spectrum to evolve freely).
- **μP alignment**: SSO explicitly derives from the spectral μP condition ($\|\mathbf{W}\|_2 = \Theta(\sqrt{d_{\text{out}}/d_{\text{in}}})$); Hyperball uses Frobenius normalization which doesn't directly control the operator norm.
- **Update direction**: SSO uses tangent-space projected msign; Hyperball applies Muon/msign followed by norm projection.

The [HyperP paper](hyperp-hypersphere-parameterization.md) (Renmin University — overlapping authors with SSO) provides the first LR transfer laws across width, depth, tokens, and MoE granularity under Frobenius-sphere constraint. SSO extends this to spectral-sphere constraint with a steepest-descent derivation.

Both Hyperball and SSO confirm that **manifold-constrained optimization enables hyperparameter transfer** — a convergent finding across independent groups.

## Implementation notes

- **Code**: [github.com/Unakar/Spectral-Sphere-Optimizer](https://github.com/Unakar/Spectral-Sphere-Optimizer)
- **Framework**: Implemented in Megatron-LM
- **Hardware**: Experiments on NVIDIA B200 GPUs
- **Training**: BF16 mixed precision, 4M tokens/step global batch, cosine LR decay to 10% peak, 500 warmup steps
- **msign**: Polar Express method with 8 Newton-Schulz iterations in FP32
- **λ-solver**: Max 20 iterations, tolerance 2e-4, bracket-and-bisect
- **Data**: OLMo-Mix-1124 dataset, 100B tokens training, 1B validation
- **Key hyperparameters**: Nesterov momentum, spectral radius $c=2.0$, no weight decay on 2D hidden weights
- **MuonSphere variant**: For practitioners wanting weight constraint without solver overhead — just normalize weights onto spectral sphere before each update (λ=0)
