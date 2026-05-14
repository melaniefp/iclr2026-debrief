---
title: "Transformers are Inherently Succinct"
authors: "Pascal Bergsträßer, Ryan Cotterell, Anthony W. Lin"
affiliations: "RPTU Kaiserslautern-Landau, ETH Zürich, MPI-SWS"
url: "https://arxiv.org/abs/2510.19315"
date: "2025-10-22"
category: "Deep Learning Theory"
raw_source: "raw/transformers-are-inherently-succinct-src/"
keywords:
  - succinctness
  - unique hard-attention transformers
  - formal language theory
  - EXPSPACE-completeness
---

# Transformers are Inherently Succinct

## Summary

TL;DR: Fixed-precision transformers (UHATs) are exponentially more succinct than LTL and RNNs, and doubly exponentially more succinct than finite automata, at representing formal languages — making verification of transformer properties EXPSPACE-complete.

- **Succinctness as expressivity metric**: The paper proposes *succinctness* — the minimum description size needed to represent a language — as an alternative to raw expressivity for comparing transformers to other formalisms. Even though fixed-precision transformers recognize only star-free regular languages (a subset of regular languages), they can encode the same concepts far more compactly.
- **Exponential gap over LTL/RNN**: UHATs can be exponentially more succinct than Linear Temporal Logic formulas and fixed-precision RNNs (including SSMs like Mamba). The gap is tight: any UHAT can be converted to an exponential-size LTL formula ([Proposition 9](https://arxiv.org/html/2510.19315#S4.Thmtheorem9)).
- **Doubly exponential gap over automata**: UHATs can be doubly exponentially more succinct than finite automata ([Theorem 7](https://arxiv.org/html/2510.19315#S4.Thmtheorem7)). This follows from the ability to encode counters counting up to $2^{2^n}$ in polynomial-size UHATs.
- **Verification is EXPSPACE-complete**: Checking whether a UHAT recognizes the empty language (non-emptiness) is EXPSPACE-complete ([Theorem 3](https://arxiv.org/html/2510.19315#S3.Thmtheorem3)), as is checking equivalence of two UHATs. This is drastically harder than the same problems for DFAs (polynomial time) or LTL (PSPACE-complete).
- **Improved translation**: The paper gives an exponential-time translation from UHATs to LTL ([Proposition 9](https://arxiv.org/html/2510.19315#S4.Thmtheorem9)), improving the doubly exponential translation of Yang et al. (2024). A key insight is that UHAT intermediate values require only polynomially many bits ([Proposition 8](https://arxiv.org/html/2510.19315#S4.Thmtheorem8)).

## Contributions

### 1. Succinctness framework for transformers

The paper introduces succinctness as a formal measure of how compactly different formalisms can represent the same language ([Section 1](https://arxiv.org/html/2510.19315#S1)). A class $\mathcal{C}_1$ is exponentially more succinct than $\mathcal{C}_2$ if for every subexponential function $f \in 2^{o(n)}$, there exists a representation in $\mathcal{C}_1$ of size $n$ such that any equivalent representation in $\mathcal{C}_2$ has size $> f(n)$ ([Section 2.4](https://arxiv.org/html/2510.19315#S2.SS4)). This contrasts with prior work that focused purely on which language classes transformers can recognize.

### 2. EXPSPACE-completeness of non-emptiness (Theorem 3)

The lower bound is proved via reduction from the $2^n$-tiling problem ([Section 3](https://arxiv.org/html/2510.19315#S3)). The key technical construction shows how a B-RASP program (and hence a UHAT) of polynomial size can encode tilings of a $2^n \times m$ grid using:

- **Binary counter with attention**: A B-RASP attention operation $C_{+1}(i)$ checks that consecutive binary counter values are incremented correctly, using strict future masking with rightmost tie-breaking to select the previous counter block ([Example 1](https://arxiv.org/html/2510.19315#S3.Thmtheorem1)).
- **Vertical constraint checking**: Attention selects the most recent occurrence of the same column position (matching counter value) to verify vertical tiling constraints.

The upper bound follows from the new exponential-time UHAT→LTL translation combined with PSPACE decidability of LTL non-emptiness.

### 3. Tight succinctness gaps

| Comparison | Gap | Reference |
|-----------|-----|-----------|
| UHAT vs LTL | Exponential (tight) | [Theorem 5](https://arxiv.org/html/2510.19315#S4.Thmtheorem5), [Proposition 6](https://arxiv.org/html/2510.19315#S4.Thmtheorem6) |
| UHAT vs finite automata | Doubly exponential | [Theorem 7](https://arxiv.org/html/2510.19315#S4.Thmtheorem7) |
| UHAT vs RNN (fixed precision) | Exponential | [Corollary after Theorem 7](https://arxiv.org/html/2510.19315#S4.Thmtheorem7) |

The exponential gap over LTL is proved by constructing UHATs whose smallest accepted word has length $\geq 2^{2^n}$, while any LTL formula accepting a non-empty language must accept a word of length at most exponential in the formula size ([Theorem 5](https://arxiv.org/html/2510.19315#S4.Thmtheorem5)). The converse direction — LTL can be simulated by polynomial-size UHATs ([Proposition 6](https://arxiv.org/html/2510.19315#S4.Thmtheorem6)) — shows the gap is tight.

### 4. Polynomial bit-complexity of UHAT values (Proposition 8)

A crucial technical observation: intermediate values during UHAT computation can be represented with only polynomially many bits ([Proposition 8](https://arxiv.org/html/2510.19315#S4.Thmtheorem8)). This is because:
- Score function results (dot products) are *not* forwarded to subsequent layers
- Only affine transformations of input vectors are forwarded
- Repeated linear operations across $L$ layers produce values at most exponential in $L$, requiring $O(L)$ bits

This enables the improved exponential (vs. doubly exponential) UHAT→LTL translation.

## Empirical findings

This is a purely theoretical paper with no experiments or benchmarks. All results are formal proofs establishing complexity-theoretic lower and upper bounds.

## Notes from summaries of related work

The paper builds on the line of work establishing that fixed-precision transformers recognize exactly star-free regular languages (Yang et al., 2024; Barceló et al., 2024; Chiang et al., 2025; Li & Chiang, 2025). The key prior result is that B-RASP is expressively equivalent to UHATs (Yang et al., 2024).

Compared to Stockhammer, Angluin, and Loughridge (2025), who showed NEXP-hardness of transformer verification (implying single exponential succinctness over automata), this paper achieves:
- *Doubly* exponential succinctness over automata (stronger)
- Exponential succinctness over LTL and RNN (new)
- Uses a simpler model (unique hard attention vs. softmax/hardmax combination)
- Uses positional masking as a simple form of positional encoding

## Implementation notes

- **Model**: Unique Hard-Attention Transformers (UHATs) — the weakest known class of transformers, using hard attention with deterministic tie-breaking (leftmost or rightmost). Languages are in $\text{AC}^0$.
- **Intermediate formalism**: Boolean RASP (B-RASP) used as a stepping stone, known to be expressively equivalent to UHATs.
- **No code or implementation**: Purely theoretical results; no GitHub repository or experimental code.
- **Fixed precision**: Results assume fixed (finite) precision arithmetic, faithful to real hardware. Lower bounds hold even for fixed-precision integers.
- **Conference**: Accepted at ICLR 2026.
