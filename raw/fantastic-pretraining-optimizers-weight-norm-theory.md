---
title: "Fantastic Pretraining Optimizers and Where to Find Them 2.2: The Hitchhiker's Guide to the Weight Norm Theory"
url: "https://whenwen.github.io/wd_blog/public/weight-decay-part-2.html"
source: blog
author: "Kaiyue Wen, Xingyu Dang, Kaifeng Lyu, Tengyu Ma, Percy Liang"
date: "2025-01-03"
captured: "2026-04-28"
tags:
  - optimization
  - weight-decay
  - hyperparameter-transfer
  - scaling-laws
  - deep-learning-theory
aliases:
  - "Weight Norm Theory"
  - "Hyperball theory blog"
related:
  - "wiki/concepts/hyperball-optimizer.md"
  - "wiki/papers/hyperp-hypersphere-scaling.md"
  - "wiki/concepts/neural-scaling-laws.md"
  - "wiki/concepts/deep-learning-theory.md"
---

# Fantastic Pretraining Optimizers and Where to Find Them 2.2: The Hitchhiker's Guide to the Weight Norm Theory

**Series navigation:**

- **Part 1 (optimizer):** [Hyperball Optimization](https://psychedelic-sunstone-851.notion.site/Fantastic-Pretraining-Optimizers-and-Where-to-Find-Them-2-1-Hyperball-Optimization-2e924306e6f280e7a5ffee00eb40a0dd)
- **Part 2 (this page):** The Hitchhiker's Guide to the Weight Norm Theory

Weight decay is a standard component of training, yet its role in modern deep learning is often misunderstood. In this post, we will show how recent deep learning research reveals that for scale-invariant models (like Transformers), weight decay does not control capacity. Instead, it controls the **effective step size** [1][2][3][4][5]. This theory is what motivates the design of the **Hyperball** optimizer in Part 1 of this series.

**Key takeaways:**

1. **Debunk** the classical "capacity control" view.
2. **Derive** the modern view: weight decay regulates weight norm, which then controls the effective update size. This can lead to unexpected phenomena. For example, gradient norms may increase as loss decreases [6]!

---

## 1. The Paradox of Weight Decay

Standard weight decay updates parameters $W$ by:

$$W_{t+1} = (1 - \eta_t \lambda) W_t - \eta_t u_t$$

where $\eta_t$ is the learning rate, $\lambda$ is the decay coefficient, and $u_t$ is the update direction given by the base optimizer. This is equivalent to minimizing $L(W) + \frac{\lambda}{2}\|W\|_F^2$ for SGD.

> **Classical View:** This penalty keeps weights small, limiting model capacity and preventing overfitting.
>
> **Modern Reality:** Most weight matrices in modern architectures (Transformers, ResNets with BatchNorm/LayerNorm) are **scale-invariant** [1][3]. Multiplying weights by a constant $c$ does not change the output or the loss:
>
> $$L(cW) = L(W), \quad \forall c > 0$$

If the neural network function and hence the loss is unchanged by the scale of $W$, penalizing $\|W\|_F$ cannot constrain capacity. Yet, people continue to use weight decay. Why?

## 2. The Mechanism: How Weight Decay Sets the Effective Step Size

For scale-invariant losses $L(cW)=L(W)$, optimization depends only on the **direction** of the weights:

$$\hat{W} = W / \|W\|_F.$$

This direction-only view follows the intrinsic learning-rate analysis of [4].

Define the **effective step size** $\eta_{\text{eff}}$ as the magnitude of the change in the weight direction:

$$\eta_{\text{eff}} := \|\hat{W}_{t+1} - \hat{W}_t\|.$$

The key mechanism is:

1. The **weight norm** $\|W\|_F$ determines how large a step we take in direction space.
2. The **weight decay** coefficient $\lambda$ determines the equilibrium value of $\|W\|_F$.

Together these imply that $\lambda$ directly sets the effective step size. This calculation has been explored in detail in [4][8].

### Summary of steady-state behavior

| Quantity | AdamW / Moonlight | Muon |
|----------|-------------------|------|
| $\|W_t\|_F$ | $\eta \sqrt{\frac{1-\beta_1}{1+\beta_1}}\sqrt{d_{\mathrm{in}}d_{\mathrm{out}}}\sqrt{\frac{1+\alpha\beta_1}{(1-\alpha^2)(1-\alpha\beta_1)}}$ | $\eta \sqrt{d_{\mathrm{out}}}\sqrt{\frac{1+\alpha\beta_1}{(1-\alpha^2)(1-\alpha\beta_1)}}$ |
| $\|u_t\|_F$ | $\sqrt{\frac{1-\beta_1}{1+\beta_1}}\sqrt{d_{\mathrm{in}}d_{\mathrm{out}}}$ | $\sqrt{d_{\mathrm{out}}}$ |
| $\cos(W_t,u_t)$ | $-\beta_1 \sqrt{\frac{1-\alpha^2}{(1+\alpha\beta_1)(1-\alpha\beta_1)}}$ | (same) |
| Effective step size $\eta_{\mathrm{eff}}$ | $\frac{1}{1+\alpha\beta_1}\sqrt{(1-\alpha^2)(1-\beta_1^2)} \approx \sqrt{2\eta\lambda \frac{1 - \beta_1}{1+\beta_1}}$ | (same) |

Here $\alpha = 1 - \eta\lambda$ and $d_{\mathrm{in}}, d_{\mathrm{out}}$ are the layer dimensions; Muon and Moonlight share the same correlation structure as AdamW, so only the update norm $U$ differs.

### 2.1 Basic Assumption: Noise-Dominated Training

Throughout this section we work in the **noise-dominated regime**: the stochasticity of the gradients is much larger than the signal. Concretely, for a single scalar gradient entry we assume:

$$g_t \in \mathbb{R},\quad g_t \sim \mathcal N(0,\sigma^2)\ \text{i.i.d. over } t,$$

and for a whole layer we treat the gradient as:

$$g_t \in \mathbb{R}^d,\quad g_t \sim \mathcal N(0,\sigma^2 I_d).$$

This assumption may look outrageous at first glance, because it ignores any structure in the loss and assumes there is "no signal." However, **for the specific quantities we care about** (stationary update norms, angles, equilibrium weight norms, effective step size), this is a good approximation when the noise level is much larger than the signal. A similar assumption has been used in [12] to study how batch size affects the effective step size.

### 2.2 Predicting Optimizer Update Norm

Let $u_t$ be the **base optimizer update** *before* adding weight decay (e.g. the Adam part of AdamW). Under the noise-dominated model, the update norm is approximately **constant over time**, depending only on the optimizer hyperparameters and the layer dimension.

For **Muon**, this is already guaranteed by design, as all of the singular values of Muon's update before scaling are $1$. In the speedrun implementation [13], the update is scaled by $\max(\sqrt{\frac{d_{\mathrm{out}}}{d_{\mathrm{in}}}}, 1)$, giving:

$$\|u_t\|_F = \sqrt{d_{\mathrm{out}}}.$$

For **Moonlight** [14], the update is scaled by $0.2\sqrt{\max(d_{\mathrm{out}}, d_{\mathrm{in}})}$, giving:

$$\|u_t\|_F = 0.2\sqrt{d_{\mathrm{out}} d_{\mathrm{in}}}.$$

For **AdamW**, focusing on a single scalar coordinate, the (bias-corrected) update in the "infinite history" limit is:

$$\bar u_{t} = \frac{m_t}{\sqrt{v_t}}, \quad m_t = (1 - \beta_1)\sum_{i=0}^{\infty} \beta_1^i \bar g_{t-i}, \quad v_t = (1 - \beta_2)\sum_{i=0}^{\infty} \beta_2^i \bar g_{t-i}^2$$

Under the noise-dominated assumption, the denominator converges to the variance of the gradient, and for a matrix $W_t$ with $d = d_{\mathrm{in}} d_{\mathrm{out}}$ parameters:

$$\mathbb{E}[\bar u_t^2] \approx d\frac{1-\beta_1}{1+\beta_1}.$$

> **Property 1 (Approximately Constant Update Norm):** In the Gaussian noise model, common base optimizers have a **time-independent RMS**, so we can treat $\|u_t\|_F \approx U$ as a **constant per layer**.

| Optimizer | Update Norm $\|u_t\|_F$ |
|-----------|------------------------|
| AdamW | $\sqrt{\frac{1-\beta_1}{1+\beta_1}} \sqrt{d_{\mathrm{in}} \times d_{\mathrm{out}}}$ |
| Muon | $\sqrt{d_{\mathrm{out}}}$ |
| Moonlight | $0.2\sqrt{d_{\mathrm{out}} d_{\mathrm{in}}}$ |

### 2.3 Predicting the Correlation Between Update and Weight

We now turn to the relationship between the update vector $u_t$ and the weight vector $W_t$. A crucial observation is that they exhibit a **stable correlation**.

We quantify this via the projection coefficient $\gamma_t$:

$$\gamma_t := \frac{\langle u_t, W_t \rangle}{\|u_t\|_F^2} \approx \text{const}.$$

**Intuition:** Why are they correlated?

1. **Weights accumulate history:** The weight vector $W_t$ is an exponentially weighted sum of **past updates** ($u_{t-1}, u_{t-2}, \dots$).
2. **Momentum creates memory:** Due to momentum, the current update $u_t$ is not independent of the past; it is strongly correlated with **recent past updates**.
3. **Correlation is inevitable:** Since $W_t$ is built from vectors that $u_t$ is correlated with, the projection of $W_t$ onto $u_t$ is non-zero and stable.

Mathematically, with decoupled weight decay $W_{t+1} = \alpha W_t - \eta u_t$ (where $\alpha = 1-\eta\lambda$), we can write:

$$W_t = -\eta\sum_{k=1}^{t} \alpha^{k-1} u_{t-k}.$$

In the same noise-dominated regime, the correlation converges to:

$$\gamma_t \approx -\frac{\eta\beta_1}{1-\alpha\beta_1}.$$

> Because $W_t$ accumulates past updates and momentum ensures $u_t$ correlates with those same past updates, the **projection of $W_t$ onto $u_t$** stabilizes:
>
> $$\langle W_t, u_t \rangle \approx -\frac{\eta\beta_1}{1-\alpha\beta_1} \|u_t\|_F^2.$$
>
> This projection term is the same across AdamW and Muon.

### 2.4 Solving the Equilibrium Weight Norm

The dynamics of the weight norm are driven by a tension between two forces: **weight decay**, which shrinks the weights, and **optimizer updates**, which drive the weights away from zero.

With decoupled weight decay, the weight evolves as $W_{t+1} = \alpha W_t - \eta u_t$. Squaring gives:

$$r_{t+1}^2 = \alpha^2 r_t^2 + \underbrace{(\eta^2 - 2\alpha\eta \gamma) U^2}_{\text{effective norm increase}} \quad (\star)$$

At equilibrium ($r_{t+1} \approx r_t \approx r_\star$):

$$r_\star \approx U \sqrt{\frac{\eta^2 - 2\alpha\eta\gamma}{1-\alpha^2}}.$$

Plugging in $\gamma \approx -\frac{\eta\beta_1}{1-\alpha\beta_1}$:

$$\boxed{\|W_\infty\|_F \approx \eta U \sqrt{\frac{1+\alpha\beta_1}{(1-\alpha^2)(1-\alpha\beta_1)}}}$$

This formula depends *only* on the hyperparameters ($\eta, \lambda, \beta_1$) and the layer geometry (through $U$). It requires no empirical fitting.

### 2.5 Solving the Effective Step Size

We finally translate the norm dynamics into an **effective step size**, defined as the magnitude of the change in the *direction* of the weights:

$$\eta_{\mathrm{eff},t} := \|\hat{W}_{t+1} - \hat{W}_t\|_F.$$

The step size is determined by the projection of the update onto the tangent space of the unit sphere. After substitution:

$$\boxed{\eta_{\mathrm{eff},t} \approx \frac{1}{1 + \alpha \beta_1} \sqrt{(1 - \alpha^2)(1 - \beta_1^2)} \approx \sqrt{2\eta\lambda \frac{1 - \beta_1}{1 + \beta_1}}}$$

> Weight decay $\lambda$ and learning rate $\eta$ together define a **hidden effective step size**: tuning $\eta\lambda$ directly controls how aggressively the model moves in direction space [4][8].

### 2.6 One Last Thing: How Gradient Norms Scale

We explain why **gradient norms tend to grow** toward the end of training when the learning rate decays, even as the loss keeps decreasing.

From §2.4, in the steady-state regime:

$$\|W_t\|_F \approx C(\alpha,\beta)\sqrt{\frac{\eta_t}{\lambda}}.$$

For a **scale-invariant** layer, the loss satisfies $L(cW) = L(W)$ for all $c > 0$, which implies the gradient rescales inversely:

$$\nabla_W L(cW) = \frac{1}{c} \nabla_W L(W).$$

Therefore:

$$\|G_t\|_F := \|\nabla_W L(W_t)\|_F \propto \frac{1}{\|W_t\|_F} \propto \sqrt{\frac{\lambda}{\eta_t}}.$$

> **Key point:** In scale-invariant layers with weight decay, the steady-state weight norm scales like $\|W_t\|_F \propto \sqrt{\eta_t/\lambda}$, so the gradient norm scales like $\|G_t\|_F \propto \sqrt{\lambda/\eta_t}$.
>
> When the learning rate decays, the **equilibrium radius shrinks and the gradient norm rises**, explaining the empirically observed increase in gradient norms late in training.

## 3. Explaining Empirical Phenomena

The classic saying goes "all models are wrong, but some are useful". In deep learning theory, whether a theory is useful should be judged by two perspectives:

1. Can it predict empirical phenomena? (This section)
2. Can it motivate algorithms that work better? (Part 1)

Most of the empirical figures in this section are from the optimizer sweeps from the previous study of pretraining optimizers [15].

### Phenomenon 1: Weight norm tracks learning rate warmup and decay throughout training

**Explanation:** The equilibrium weight norm is determined by learning rate $\eta$ and weight decay $\lambda$, as $\|W_{\infty}\|_F \propto \sqrt{\frac{\eta}{2\lambda}} U$.

### Phenomenon 2: Gradient norm increases through training

**Explanation:** The gradient norm is determined by the weight norm, as $\|G_t\|_F \propto \frac{1}{\|W_t\|_F} \propto \sqrt{\lambda/\eta}$. Naturally, as the weight norm decreases, the gradient norm increases.

### Phenomenon 3: When $\eta \lambda$ is fixed, AdamW converges to the same loss; weight norms are proportional to learning rate

**Explanation:** The effective step size is $\eta_{\mathrm{eff}} \propto \sqrt{\eta\lambda}$. The equilibrium weight norm $\|W_{\infty}\|_F \propto \sqrt{\frac{\eta}{\lambda}} U$ is proportional to the learning rate when $\eta \lambda$ is fixed [13].

### Phenomenon 4: Weight decay starts with higher loss but converges to lower loss

**Explanation:** Although runs use the same nominal learning-rate schedule, weight decay changes weight norms and therefore induces a different effective step size. Training with weight decay yields a larger effective step size throughout training. In the *river valley landscape* picture [16], a larger effective step size amplifies hill-direction oscillations (raising early loss), but accelerates motion along the river. When the learning rate decays, oscillations shrink and the additional river progress is revealed.

### Phenomenon 5: Hyperparameter transfer is not sensitive to weight scale at initialization but is sensitive to how weight decay is scaled

**Explanation:** Weight decay has emerged as the key driver of hyperparameter transfer in recent work [17][18][19][20], overshadowing MuP initialization [21]. The weight norm rapidly settles into the equilibrium predicted by theory, a value set solely by the learning rate and weight decay that does **not** depend on the initial scale.

## Acknowledgments

The authors thank Songlin Yang, Zihan Qiu, and Liliang Ren for motivating this blog post into existence. To some extent, this work is a proof to show that it is possible to remove weight decay altogether by designing the optimizer to explicitly control weight norms. The authors also thank William Held, David Hall, Suhas Kotha, Tatsunori Hashimoto, Jason Lee, Zhiyuan Li, Lijie Chen, Huaqing Zhang, Jiacheng You, Jeremy Bernstein, and Samuel Schoenholz for helpful discussions.

## Citation

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

## References

1. **Twan van Laarhoven**. "L2 Regularization versus Batch and Weight Normalization." arXiv (2017). [arXiv:1706.05350](https://arxiv.org/abs/1706.05350)
2. **Guodong Zhang, Chaoqi Wang, Bowen Xu, Roger Grosse**. "Three Mechanisms of Weight Decay Regularization." ICLR (2019). [OpenReview](https://openreview.net/forum?id=B1lz-3Rct7)
3. **Elad Hoffer, Ron Banner, Itay Golan, Daniel Soudry**. "Norm matters: efficient and accurate normalization schemes in deep networks." (2018). [arXiv:1803.01814](https://arxiv.org/abs/1803.01814)
4. **Zhiyuan Li, Kaifeng Lyu, Sanjeev Arora**. "Reconciling Modern Deep Learning with Traditional Optimization Analyses: The Intrinsic Learning Rate." NeurIPS (2020). [arXiv:2010.02916](https://arxiv.org/abs/2010.02916)
5. **Francesco D'Angelo, Maksym Andriushchenko, Aditya Varre, Nicolas Flammarion**. "Why Do We Need Weight Decay in Modern Deep Learning?" (2023). [arXiv:2310.04415](https://arxiv.org/abs/2310.04415)
6. **Aaron Defazio**. "Why Gradients Rapidly Increase Near the End of Training." (2025). [arXiv:2506.02285](https://arxiv.org/abs/2506.02285)
7. **Ilya Loshchilov, Frank Hutter**. "Decoupled Weight Decay Regularization (AdamW)." (2019). [arXiv:1711.05101](https://arxiv.org/abs/1711.05101)
8. **Atli Kosson, Bettina Messmer, Martin Jaggi**. "Rotational Equilibrium: How Weight Decay Balances Learning Across Neural Networks." (2024). [arXiv:2305.17212](https://arxiv.org/abs/2305.17212)
9. **Jianlin Su**. "AdamW Weight RMS Asymptotics (Part I)." (2025). [kexue.fm/archives/11307](https://kexue.fm/archives/11307)
10. **Jianlin Su**. "Why Adam's Update RMS Is 0.2?" (2025). [kexue.fm/archives/11267](https://kexue.fm/archives/11267)
11. **Jianlin Su**. "AdamW Weight RMS Asymptotics (Part II)." (2025). [kexue.fm/archives/11404](https://kexue.fm/archives/11404)
12. **Sadhika Malladi, Kaifeng Lyu, Abhishek Panigrahi, Sanjeev Arora**. "On the SDEs and Scaling Rules for Adaptive Gradient Algorithms." (2022). [arXiv:2205.10287](https://arxiv.org/abs/2205.10287)
13. **Keller Jordan**. "Muon: An optimizer for hidden layers in neural networks." (2023). [kellerjordan.github.io/posts/muon/](https://kellerjordan.github.io/posts/muon/)
14. **Jingyuan Liu et al.** "Muon is Scalable for LLM Training." (2025). [arXiv:2502.16982](https://arxiv.org/abs/2502.16982)
15. **Kaiyue Wen, David Hall, Tengyu Ma, Percy Liang**. "Fantastic Pretraining Optimizers and Where to Find Them." (2025). [arXiv:2509.02046](https://arxiv.org/abs/2509.02046)
16. **Kaiyue Wen, Zhiyuan Li, Jason Wang, David Hall, Percy Liang, Tengyu Ma**. "Understanding Warmup-Stable-Decay Learning Rates: A River Valley Loss Landscape Perspective." (2024). [arXiv:2410.05192](https://arxiv.org/abs/2410.05192)
17. **Atli Kosson, Jeremy Welborn, Yang Liu, Martin Jaggi, Xi Chen**. "Weight Decay may matter more than μP for Learning Rate Transfer in Practice." (2025). [arXiv:2510.19093](https://arxiv.org/abs/2510.19093)
18. **Charlie Blake et al.** "u-μP: The Unit-Scaled Maximal Update Parametrization." (2024). [arXiv:2407.17465](https://arxiv.org/abs/2407.17465)
19. **Zhiyuan Fan, Yifeng Liu, Qingyue Zhao, Angela Yuan, Quanquan Gu**. "Robust Layerwise Scaling Rules by Proper Weight Decay Tuning." (2025). [arXiv:2510.15262](https://arxiv.org/abs/2510.15262)
20. **Xi Wang, Laurence Aitchison**. "How to set AdamW's weight decay as you scale model and dataset size." (2024). [arXiv:2405.13698](https://arxiv.org/abs/2405.13698)
21. **Greg Yang et al.** "Tensor Programs V: Tuning Large Neural Networks via Zero-Shot Hyperparameter Transfer." (2021). [arXiv:2203.03466](https://arxiv.org/abs/2203.03466)
22. **Tim Salimans, Diederik P. Kingma**. "Weight Normalization: A Simple Reparameterization to Accelerate Training of Deep Neural Networks." (2016). [arXiv:1602.07868](https://arxiv.org/abs/1602.07868)
23. **Tero Karras et al.** "Analyzing and Improving the Training Dynamics of Diffusion Models." (2023). [arXiv:2312.02696](https://arxiv.org/abs/2312.02696)
24. **Yonggan Fu et al.** "Nemotron-Flash: Towards Latency-Optimal Hybrid Small Language Models." (2025). [arXiv:2511.18890](https://arxiv.org/abs/2511.18890)
25. **Greg Yang, James B. Simon, Jeremy Bernstein**. "A Spectral Condition for Feature Learning." (2023). [arXiv:2310.17813](https://arxiv.org/abs/2310.17813)
26. **Jeremy Bernstein**. "Modular Manifolds." Thinking Machines Lab (2025). [thinkingmachines.ai/blog/modular-manifolds/](https://thinkingmachines.ai/blog/modular-manifolds/)
27. **Jianlin Su**. "Muon + Stiefel." Scientific Spaces (2025). [kexue.fm/archives/11221](https://kexue.fm/archives/11221)
28. **Jeremy Bernstein**. "Orthogonal manifold." Modula Systems Docs (2025). [docs.modula.systems](https://docs.modula.systems/algorithms/manifold/orthogonal/#open-problem-extending-to-the-stiefel-manifold)
29. **Franz Louis Cesista**. "Heuristic Solutions for Steepest Descent on the Stiefel Manifold." (2025). [leloykun.github.io](https://leloykun.github.io/ponder/steepest-descent-stiefel/)
30. **Jianlin Su**. "Thinking about Spectral Norm Gradient and Spectral Weight Decay." Scientific Spaces (2024). [kexue.fm/archives/10648](https://kexue.fm/archives/10648)
31. **Lizhang Chen, Jonathan Li, Qiang Liu**. "Muon Optimizes Under Spectral Norm Constraints." (2025). [arXiv:2506.15054](https://arxiv.org/abs/2506.15054)
32. **Shikai Qiu et al.** "Hyperparameter Transfer Enables Consistent Gains of Matrix-Preconditioned Optimizers Across Scale." (2025). [arXiv:2512.05620](https://arxiv.org/abs/2512.05620)
