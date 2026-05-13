---
title: "Fantastic Pretraining Optimizers and Where to Find Them 2.1: Hyperball Optimization"
url: "https://psychedelic-sunstone-851.notion.site/Fantastic-Pretraining-Optimizers-and-Where-to-Find-Them-2-1-Hyperball-Optimization-2e924306e6f280e7a5ffee00eb40a0dd"
source: blog
author: "Kaiyue Wen, Xingyu Dang, Kaifeng Lyu, Tengyu Ma, Percy Liang"
date: "2025-12-15"
captured: "2026-04-28"
tags:
  - optimization
  - weight-decay
  - hyperparameter-transfer
  - scaling-laws
  - language-models
aliases:
  - "Hyperball Optimization"
  - "Hyperball optimizer blog"
related:
  - "wiki/concepts/hyperball-optimizer.md"
  - "wiki/papers/hyperp-hypersphere-scaling.md"
  - "wiki/concepts/neural-scaling-laws.md"
  - "wiki/concepts/marin-project.md"
  - "raw/fantastic-pretraining-optimizers-weight-norm-theory.md"
---

# Fantastic Pretraining Optimizers and Where to Find Them 2.1: Hyperball Optimization

**Authors:** [Kaiyue Wen](https://whenwen.github.io/), [Xingyu Dang](https://dangxingyu.github.io/), [Kaifeng Lyu](https://kaifeng.ac/), [Tengyu Ma](https://ai.stanford.edu/~tengyuma/), [Percy Liang](https://cs.stanford.edu/~pliang/)

**Series navigation:**

- **Part 1 (this page):** Hyperball Optimization
- **Part 2 (theory):** [The Hitchhiker's Guide to the Weight Norm Theory](https://whenwen.github.io/wd_blog/public/weight-decay-part-2.html)

## TL;DR

We propose an optimizer wrapper called **Hyperball** that **normalizes the Frobenius norm of both weights and optimizer updates of all matrices in the neural network** throughout training instead of using weight decay. This operation leads to **20-30% speedup** over weight decay and hyperparameter transfer across widths and depths.

## Section 1: Motivation

In our previous paper *[Fantastic Pretraining Optimizers and Where to Find Them](https://arxiv.org/abs/2509.02046)*, we observed that the speedups of matrix-based optimizers including Muon over AdamW shrink from 30% to only 10% as model size and data scale grow. We've been searching for a way to keep those speedups at higher compute since.

It turns out the solution is extremely simple. We introduce a simple **optimizer wrapper that enforces constant weight and update norms**, transforming any base optimizer into its hyperball variant (e.g., Muon → Muon Hyperball). This small change leads to two empirical benefits: (1) It preserves optimizer speedups across scales, and (2) it allows hyperparameters to transfer without retuning.

## Section 2: Hyperball Optimization

Most modern LLM training uses weight decay, which controls the size of the weights implicitly. Let $W_t$ be the weight matrix at step $t$, $u_t$ be the update provided by a base optimizer (e.g., from Adam), $\eta$ be the learning rate, and $\lambda$ be the weight decay coefficient. The standard update rule is:

$$W_{t+1} = (1 - \eta \lambda) W_t - \eta u_t$$

Here $-\eta u_t$ adds the new update information and typically leads to increasing weight norm without weight decay. The term $(1 - \eta\lambda)$ softly controls the norm by shrinking the weights towards zero every step.

Hyperball replaces this soft control on weight norm with an explicit constraint. It decouples the magnitude of the weights from the direction of the update entirely. To define the update, we first introduce the following notation:

1. $R$: The initial Frobenius norm of the weight matrix.
1. $\mathrm{Normalize}(x) = x / \|x\|_F$: A projection operator that maps a matrix to the sphere with Frobenius norm $R$

The Hyperball update rule is defined as:

$$W_{t+1} = R \cdot \text{Normalize}\left(W_t - \eta R \cdot \text{Normalize}(u_t) \right)$$

Geometrically, Hyperball constrains the optimization trajectory to lie strictly on the surface of a hypersphere with radius $R$. The update takes a step of length $\eta R$ in the direction defined by the normalized update $-\mathrm{Normalize}(u_t)$, and the result is immediately projected back onto the sphere. This ensures that the norm of the weights and updates remains constant, while the optimizer purely navigates the direction of the updates.

Here $u_t$ can be the optimizer update from any optimizer. In this blog, we focus on two variants: **Adam-Hyperball (AdamH)** and **Muon-Hyperball (MuonH)**.

**Empirical Tips:**

1. Hyperball is applied to all non-embedding matrices in the neural network. All remaining parameters, including those in RMSNorm and the word embedding layers, are still optimized using Adam. When we use MuonH for the rest of projection, we use AdamH for the LM head.

1. The step size $\eta$ intuitively represents how strongly the current update should influence the next weights. We empirically find that Hyperball optimizers prefer a learning rate between `2.5e-3` to `1e-2`. It also has better hyperparameter transfer property as discussed in Section 3.2.

1. The radius $R$ fixes the weight norm and can be set once. In our experiments, we set it to be the initial norm $R = \lVert W_0\rVert_F$ where we randomly initialize each parameter with a standard deviation of $1 / \sqrt{d_{\mathrm{in}}}$. We expect Hyperball to tolerate a wide range of initialization schemes, since it keeps the relative update size the same across initializations.

## Section 3: Experiments

### Section 3.1: Empirical Speedup

We evaluated Hyperball's training speedup across multiple scales and settings. Unless otherwise specified, we use a Qwen3-like architecture with **QK-Norm** and train on a mixture of DCLM-baseline, StarCoder and ProofPile 2.

**Head-to-head Comparison with Weight Decay.** In the below run where we compare Muon and MuonH on a 1.2B model, we show that MuonH reaches 0.03 lower final loss while maintaining a constant weight norm throughout training. One important thing to note is that Hyperball optimizers typically start with a higher loss but overtake baseline methods once the learning rate decays.

**Quantitative Speedup on 1.2B Models.** We then quantify optimizer **speedup** by training **1.2B-parameter Qwen3** models over 4 Chinchilla ratios: 1× means the token budget is 20x the non-embedding parameters and 2×/4×/8× mean training on 2/4/8 times more tokens than that reference. We then fit a scaling law for AdamW and compute *to reach the same final evaluation loss, how many tokens would AdamW need compared to our new optimizer / Muon?*

This is the same setup as in our [previous paper](https://arxiv.org/abs/2509.02046) except that now we incorporate QK-Norm in the new architecture. The original Muon runs only show 10% speedup at this model scale, similar to the result in our original paper. Meanwhile, our Hyperball optimizers demonstrate **20-30%** speedup and the speedup increases with respect to the training duration. See the original [runs](https://api.wandb.ai/links/marin-community/3zuwbr17) here.

**Validation in [Marin's speedrun](https://marin.community/speedrun/).** We further test both AdamH and MuonH in the setting of Marin's speedrun, where we train on the FineWeb-Edu data for different models in the 1x Chinchilla regime. Both AdamH and MuonH show persistent speedup over their weight decay counterparts with increasing scales and can match models with 10% more parameters in 1x Chinchilla regime.

**Scale up to 8B model.** We further scaled MuonH up to 8B parameter models in [Marin Ferries](https://github.com/marin-community/marin/pull/1839) and compare MuonH with our previous AdamW baseline. We observe a surprising 0.04 loss improvement for the 8B experiments. Note that there is a catch that both MuonH and AdamW adopt manually chosen hyperparameters so likely there are rooms to improve both of them.

**Over-training Stress Test.** Our [previous paper](https://arxiv.org/abs/2509.02046) observed that optimizer's speedup can diminish with increasing training durations. We show here Hyperball maintained its performance advantages for overtrained 130M models even when we pushed training far beyond typical Chinchilla budgets.

### Section 3.2: Hyperparameter Transfer (Depth & Width)

Hyperball's second compelling property is its ability to transfer hyperparameters across different model architectures without retuning. Optimal hyperparameters often change with scales, even when one adopts initialization schemes like MuP (e.g. [Kosson et al.](https://arxiv.org/abs/2510.19093) and [Fan et al.](https://arxiv.org/abs/2510.15262)). This makes it challenging to find suitable hyperparameters for large model training.

Hyperball enables hyperparameter transfer by explicitly controlling the effective step size in the direction space. The key insight is that the ratio between weight norm and update norm is the main factor governing optimization dynamics according to [Spectral Condition](https://arxiv.org/abs/2310.17813). This approach maintains the model in a feature learning "sweet spot" during the optimization process.

We validated this experimentally across two dimensions:

- **Depth scaling:** Fixed hidden dimensions at $d=128$ while varying the number of layers from L=4 to 512 for 10B tokens. The maximal drift of the optimal learning rate window was only **1.4x**.
- **Width scaling:** Fixed the number of layers at L=4 while varying hidden dimensions from $d=128$ to 2048 for 10B tokens. Again, the maximal drift of the optimal learning rate window was just **1.4x** for both AdamH and MuonH (refer to [runs](https://wandb.ai/marin-community/Hyperball) here).

## Section 4: Mechanism Behind Hyperball

### Sec 4.1: RMSNorm's Rescaling Parameter Preserves Representation Power

One might worry that fixing weight norms would limit what the network can learn. Fortunately, this isn't the case for architectures that use RMSNorm with rescaling parameters $\gamma$.

$$\mathrm{RMSNorm}(h; \gamma) = \gamma\odot h / \|h\|_{\mathrm{rms}}$$

For many linear weights in Transformers, the input is preprocessed by RMSNorm before feeding it into the corresponding linear layer. Concretely, with $W$ as the weight matrix:

$$f(h; W, \gamma) = W \times \mathrm{RMSNorm}(h; \gamma) = W (\gamma\odot h / \|h\|_{\mathrm{rms}})$$

The key observation is that $f(h; cW, \gamma/c) = f(h; W, \gamma)$ — scaling the weights and inversely scaling the rescaling parameter produces the same output. This means fixing the norm of $W$ doesn't restrict the function class the network can represent.

### Sec 4.2: Why Hyperball Speeds Up Training

Hyperball achieves faster training by cleanly separating two questions: "how big are the weights?" and "how fast do their *directions* change?"

**Weight decay couples these two factors.** With standard weight decay, there are two forces deciding the weight norm. Due to the existence of gradient noise, the optimizer update has a stable angle with the weight, causing each weight matrix's norm to increase. Meanwhile, the weight decay term shrinks the weight norm towards 0. The two effects eventually balance and each weight matrix's norm drifts toward an equilibrium value determined by hyperparameters including learning rate and weight decay factor. This equilibrium norm then implicitly sets the relative step size $\eta \|u\|_F / \|W\|_F$, which controls how quickly weight *directions* evolve ([Li et al.](https://arxiv.org/abs/2010.02916), [Simon et al.](https://arxiv.org/abs/2006.13382)).

**But neural networks are approximately scale-invariant.** Since features are typically normalized (via LayerNorm or RMSNorm), performance depends much more on the *direction* of weights than their absolute scale. What really matters for learning is the relative step size — how much the weight directions rotate each step.

**Hyperball decouples scale from directional learning speed.** By explicitly fixing the weight norm and normalizing updates, Hyperball gives direct control over the directional update speed. You can schedule this speed independently (e.g., with linear or cosine schedules), allowing the model's features to evolve at the optimal rate throughout training. This decoupling is what enables faster, more efficient learning.

## Section 5: Related Methods

While less common in modern large-scale LLM training, normalization and constraints on weight matrices have a rich history.

**Reparameterization and Standardization:**

- [Weight Normalization (Salimans & Kingma, 2016)](https://arxiv.org/abs/1602.07868): Decouples weight norm from weight direction by reparameterizing each weight matrix as $W = g \cdot \mathrm{Normalize}(V)$, where $g$ is a scalar and $V$ is a matrix with the same shape as $W$.
- [Weight Standardization (Qiao et al., 2019)](https://arxiv.org/abs/1903.10520) / [BiT (Kolesnikov et al., 2020)](https://arxiv.org/abs/1912.11370): Standardizes weights within convolution kernels (zero mean, unit variance).
- [Convolutional Normalization (Liu et al., 2021)](https://arxiv.org/abs/2102.07227): Limits the Frobenius norm of kernels to improve robustness.
- [Decoupled Network (Hyperball Convolution)](https://arxiv.org/abs/1804.08071): Constrains the convolution weight on the hypersphere and performs gradient normalization.

**Constraints in Generative Models:**

- [EDM2 (Karras et al., 2023)](https://arxiv.org/abs/2312.02696): Reparametrizes every column weight to be unit norm before use.
- [Spectral Normalization (Miyato et al., 2018)](https://arxiv.org/abs/1802.05957): Constrains the spectral norm in GANs for Lipschitz continuity.

**Constraints in Update:**

- [AdamP & SGDP](https://sangdooyun.github.io/data/heo2021iclr_adamp.pdf): Propose to keep only the component of update orthogonal to the weight to control the increase of weight norm.
- [Rotation Equilibrium](https://arxiv.org/abs/2305.17212): Proposes RV-Adam which controls the weight norm as constant and keeps only the orthogonal component of update.
- [LionAR](https://arxiv.org/abs/2410.23922): Proposes to keep each neuron's weight vector constant norm and rescale update according to the weight norm.

**Fixed Norms in LLM Pretraining:**

- [nGPT](https://arxiv.org/abs/2410.01131): Uses column-wise weight normalization and replaces all normalization layers with adaptive normalization.
- [Nemotron-Flash](https://arxiv.org/abs/2511.18890): (Concurrent) Uses spherical constraints on each channel of each weight matrix for inference latency and quantization stability, but does not apply normalization on updates.
- [anGPT](https://arxiv.org/abs/2505.22014): Relaxes the column-wise weight normalization in nGPT to the matrix version and constrains the weight to be $\|W\|_{\mathrm{F}} \le 1$ using [Constrained Parameter Regularization](https://arxiv.org/abs/2311.09058v3).
- [Target Variance Rescaling](https://arxiv.org/abs/2503.17500): Rescales the weight to be constant variance and mean zero periodically throughout training.

**Spectral-related Manifold Optimization:**

*[See embedded comparison figure in original Notion page]*

## Acknowledgement

The authors would like to thank Songlin Yang, Zihan Qiu, and Liliang Ren for motivating this blog post into existence. To some extent, this work is a proof of concept to show that it is possible to remove weight decay altogether by designing the optimizer to explicitly control weight norms. The authors would also like to thank William Held, David Hall, Suhas Kotha, Tatsunori Hashimoto, Jason Lee, Zhiyuan Li, Lijie Chen, Huaqing Zhang, Jiacheng You, Jeremy Bernstein, Shu Zhong, and Samuel Schoenholz for helpful discussions. We would like to specially thank Google TRC compute for making all the experiments possible.

## Citations

```bibtex
@online{wen2025hyperball,
  title   = {Fantastic Pretraining Optimizers and Where to Find Them 2.1: Hyperball Optimization},
  author  = {Wen, Kaiyue and Dang, Xingyu and Lyu, Kaifeng and Ma, Tengyu and Liang, Percy},
  year    = {2025},
  month   = {12},
  day     = {15},
  url     = {https://tinyurl.com/muonh},
  urldate = {2025-12-15}
}
```
