---
title: "Rethinking Language Model Scaling under Transferable Hypersphere Optimization"
authors: "Liliang Ren, Yang Liu, Yelong Shen, Weizhu Chen"
affiliations: "Microsoft"
url: "https://arxiv.org/abs/2603.28743"
date: "2026-03-30"
category: "Optimization"
raw_source: "raw/hyperp-hypersphere-parameterization-src/"
keywords:
  - hypersphere-optimization
  - scaling-laws
  - hyperparameter-transfer
  - mixture-of-experts
related:
  - "wiki/papers/hyperp-hypersphere-scaling.md"
  - "wiki/papers/spectral-sphere-optimizer.md"
---

# Rethinking Language Model Scaling under Transferable Hypersphere Optimization

## Summary

TL;DR: HyperP is the first framework for transferring a single optimal learning rate across model width, depth, training tokens, and MoE granularity under Frobenius-sphere optimization, achieving 1.58× compute efficiency over Muon baselines while providing structural stability guarantees.

- **Weight decay elimination**: Proves that weight decay is a first-order no-op under Frobenius-sphere normalization (Theorem 1/Corollary 1), reducing the hyperparameter search from a joint $(\eta, \lambda)$ plane to a single learning rate $\eta$.
- **Universal data-scaling exponent**: The optimal learning rate scales as $\eta^* \propto T^{-0.32}$ with training tokens, matching the "magic exponent" previously found for AdamW by Bjorck et al., suggesting universality across optimizers.
- **Depth-$\mu$P remains necessary**: Disproves the claim from the MuonH paper (Wen et al.) that hypersphere optimization is inherently depth-transferable; cumulative angular drift from residual connections still requires $\eta \propto 1/\sqrt{d}$ scaling.
- **SqrtGate for MoE**: Proposes replacing gating weights $g_i$ with $\sqrt{g_i}$, which preserves output RMS across MoE granularities ($k$-invariant), reducing router Z-value peaks by 5×.
- **Monotonically growing compute advantage**: HyperP's CEL over baseline grows with scale from 1× to 1.58× for dense models and 3.38× for MoE models at $6 \times 10^{21}$ FLOPs.

## Contributions

### 1. Elimination of weight decay ([Section 3.1](https://arxiv.org/html/2603.28743v2#S3.SS1))

The paper proves that on the Frobenius sphere, only the tangent component of an update survives to first order after re-projection. Formally, for weight $W$ with $\|W\|_F = c_W$:

$$
W^+ - W = \Pi_T(\Delta) + O(\|\Delta\|_F^2)
$$

where $\Pi_T(\Delta) = \Delta - \frac{\langle \Delta, W\rangle_F}{\|W\|_F^2} W$ is the tangent-space projection. Since weight decay $\lambda W$ lies in the radial direction, $\Pi_T(\lambda W) = 0$, making it a first-order no-op ([Corollary 1](https://arxiv.org/html/2603.28743v2#S3.SS1)).

Empirically validated: MuonH ($\lambda=0$) achieves slightly better validation loss (2.475) than best-tuned Muon with $\lambda=10^{-3}$ (2.479) on a 208M model at 10.4B tokens ([Table 2](https://arxiv.org/html/2603.28743v2#S3.T2), [Figure 2](https://arxiv.org/html/2603.28743v2#S3.F2)).

### 2. Width scaling ([Section 3.2](https://arxiv.org/html/2603.28743v2#S3.SS2))

Under the Frobenius-sphere constraint with $\|W\|_F = C\sqrt{d_{\text{out}}}$ and approximately isotropic singular values (as induced by Muon), the output RMS is width-stable: $\|Y\|_{\text{rms}} \approx C \|X\|_{\text{rms}}$. This inherits the $\mu$P width transfer without explicit $1/w$ LR scaling ([Theorem 2](https://arxiv.org/html/2603.28743v2#S3.SS2)).

### 3. Depth scaling ([Section 3.3](https://arxiv.org/html/2603.28743v2#S3.SS3))

With both weight and update normalization (as in MuonH), the total first-order function perturbation is $O(L \alpha_L \eta)$. For the standard $\alpha_L = L^{-1/2}$ residual scaler, this requires $\eta = O(L^{-1/2})$ — i.e., Depth-$\mu$P is still necessary ([Theorem 3](https://arxiv.org/html/2603.28743v2#S3.SS3)). The paper explicitly disproves the claim from Wen et al. (2025) that MuonH is inherently depth-transferable, showing the optimal LR drifts from 0.016 ($d=8$) to 0.008 ($d=24$) without Depth-$\mu$P ([Figure 3](https://arxiv.org/html/2603.28743v2#S4.F3)).

### 4. Data scaling ([Section 3.4](https://arxiv.org/html/2603.28743v2#S3.SS4))

Empirical sweeps across 10.4B–166.4B tokens at 208M parameters reveal a power-law:

$$
\eta^* = 24.27 \cdot T^{-0.320}
$$

with leave-one-out cross-validation error of 1.50% ([Figure 1](https://arxiv.org/html/2603.28743v2#S3.F1)). The exponent 0.32 matches the finding of Bjorck et al. for AdamW.

### 5. SqrtGate for MoE ([Section 3.6](https://arxiv.org/html/2603.28743v2#S3.SS6))

Classical softmax gating produces routed-branch RMS $\approx r/\sqrt{k}$ (shrinks with granularity). SqrtGate replaces $g_i$ with $\sqrt{g_i}$:

$$
y_{\text{route}}' = \sum_{i=1}^{k} \sqrt{g_i} E_i(x)
$$

Under weak correlation and equal-RMS assumptions (made natural by hypersphere optimization), $\|y_{\text{route}}'\|_{\text{rms}} \approx r$ regardless of $k$ ([Proposition 3](https://arxiv.org/html/2603.28743v2#S3.SS6)).

### 6. HyperP framework summary ([Table 1](https://arxiv.org/html/2603.28743v2#S3.T1))

The complete HyperP transfer rules for hidden weights under MuonH:
- **LR multiplier**: $\propto 1/(T^{0.32} \sqrt{d})$
- **Init std**: $\propto 1/\sqrt{d_{\text{in}}}$
- **Residual multiplier**: $1/\sqrt{2d}$
- **Weight decay**: 0

## Empirical findings

### MuonH vs. Muon optimality ([Section 4.1](https://arxiv.org/html/2603.28743v2#S4.SS1))

MuonH with no weight decay matches or slightly beats the best Muon configuration across a joint $(\eta, \lambda)$ sweep. Best Muon: loss 2.479 ($\eta^*=0.0222$, $\lambda=10^{-3}$); MuonH: loss 2.475 ($\eta^*=0.0155$, $\lambda=0$) ([Table 2](https://arxiv.org/html/2603.28743v2#S3.T2)).

### Depth transfer verification ([Section 4.2](https://arxiv.org/html/2603.28743v2#S4.SS2))

With Depth-$\mu$P: optimal LR stays at $\approx 0.014$–0.016 from $d=8$ to $d=24$. Without: drifts from 0.016 to 0.008. Both achieve comparable best losses at each depth, confirming Depth-$\mu$P preserves quality while enabling transfer ([Figure 3](https://arxiv.org/html/2603.28743v2#S4.F3), [Table A.4](https://arxiv.org/html/2603.28743v2#A4.T4)).

### Batch size scaling ([Section 4.3](https://arxiv.org/html/2603.28743v2#S4.SS3))

Optimal LR scales as $\eta^* \propto B^{0.558}$, between linear (1.0) and square-root (0.5) rules. All tested batch sizes (256K–2M) are below the critical batch size for this configuration ([Figure 4](https://arxiv.org/html/2603.28743v2#S4.F4)).

### MoE sparsity and granularity scaling ([Section 4.4](https://arxiv.org/html/2603.28743v2#S4.SS4))

- **Sparsity**: Optimal LR varies only 0.012–0.016 across $S \in \{1, \ldots, 32\}$. Moving from $S=1$ to $S=32$ reduces loss by 0.224 nats ([Figure 5](https://arxiv.org/html/2603.28743v2#S4.F5)).
- **Granularity**: Optimal LR varies 0.012–0.014 across $k \in \{2, \ldots, 64\}$. SqrtGate improves loss at every $k$, with best performance at $k=32$ (loss 2.310) vs. baseline saturation at $k=16$ ([Figure 6](https://arxiv.org/html/2603.28743v2#S4.F6)).

### Training FLOPs scaling ([Section 4.5](https://arxiv.org/html/2603.28743v2#S4.SS5))

Four configurations compared across $d \in \{8, 12, 16, 20, 24\}$ with 50 tokens-per-parameter:

| Method | CEL at $6\times10^{21}$ FLOPs | Irreducible floor $C_0$ |
|--------|-------------------------------|-------------------------|
| Muon ($\mu$P++) | 1.00× (baseline) | 1.23 |
| MuonH (vanilla) | 0.70× | 1.62 |
| MuonH + HyperP | 1.58× | 0.85 |
| MuonH + HyperP MoE ($S=8, k=8$) | 3.38× | 0.87 |

CEL grows monotonically with scale for HyperP, suggesting even larger gains at frontier compute ([Figure 7](https://arxiv.org/html/2603.28743v2#S4.F7), [Table A.8](https://arxiv.org/html/2603.28743v2#A4.T8)).

### Transferable stability ([Section 5.1](https://arxiv.org/html/2603.28743v2#S5.SS1))

Six metrics tracked across MoE models (913M–13.3B parameters):
- Attention Z-values plateau at ~200–220 across depths
- Router Z-values *decrease* with depth (56 → 33)
- Output RMS decreases with depth
- Outlier % decreases with depth

All metrics are bounded and non-increasing, demonstrating structural stability guarantees without Z-loss regularization ([Figure 8](https://arxiv.org/html/2603.28743v2#S5.F8)).

### Auxiliary load balancing ([Section 4.4](https://arxiv.org/html/2603.28743v2#S4.SS4))

Under hypersphere optimization, a large auxiliary loss weight $\gamma = 0.1$ achieves *both* the best validation loss (2.332) and lowest MaxVio (0.086), contradicting prior findings that large $\gamma$ hurts quality ([Table 3](https://arxiv.org/html/2603.28743v2#S4.T3)).

### Architecture ablations ([Section 5.3](https://arxiv.org/html/2603.28743v2#S5.SS3))

- **Dense**: GatedAttn+QKNorm outperforms baseline by −0.023 nats at small scale; advantage shrinks at larger scale but provides significant stability benefits (eliminates MLP output RMS spikes) ([Figure 10](https://arxiv.org/html/2603.28743v2#S5.F10), [Figure 12](https://arxiv.org/html/2603.28743v2#S5.F12)).
- **MoE**: SqrtGate reduces router Z-value peaks by 5× (from >190 to <40) compared to SharedExp alone ([Figure 12](https://arxiv.org/html/2603.28743v2#S5.F12)).

## Notes from summaries of related work

The [hyperball optimization paper](hyperp-hypersphere-scaling.md) (Wen et al., 2025) introduced MuonH with Frobenius-sphere constraint and claimed inherent depth transferability. The current paper **disproves** this claim (Section 3.3, Theorem 3) by showing cumulative angular drift requires Depth-$\mu$P. Additionally, the hyperball paper found that hyperball removes the need for weight decay tuning — HyperP provides a rigorous theoretical justification for this (Theorem 1, Corollary 1) and extends it to a full transfer framework covering data scaling and MoE granularity.

The data-scaling exponent 0.32 aligns with findings from Bjorck et al. (2025) for AdamW, suggesting a universal property independent of optimizer choice.

## Implementation notes

- **Architecture**: Transformer-Next family inspired by Qwen3-Next — GQA with 4 KV heads, head dim 128, aspect ratio $\alpha=128$ ($w = 128d$), QK-Norm, headwise gated attention, SwiGLU with $4w$ intermediate size, Pre-Norm.
- **Optimizer**: MuonH for matrix-like parameters, AdamH for unembedding, AdamW for vectors/embeddings. Momentum 0.95 for both Muon and MuonH.
- **LR schedule**: Linear decay to 10% of peak, no warm-up.
- **Initialization**: PyTorch default Kaiming uniform.
- **Training data**: SlimPajama, 4K context length, 2M token batch size.
- **FLOPs accounting**: Chinchilla-style (includes embedding, LM head, and accurate self-attention FLOPs).
- **Code release**: [https://github.com/microsoft/ArchScale](https://github.com/microsoft/ArchScale)
- **Framework**: PyTorch
