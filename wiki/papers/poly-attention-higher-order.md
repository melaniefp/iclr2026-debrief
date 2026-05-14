---
title: "Poly-attention: A general scheme for higher-order self-attention"
authors: "Sayak Chakrabarti, Toniann Pitassi, Josh Alman"
affiliations: "Columbia University"
url: "https://openreview.net/forum?id=amivrmQyvQ"
date: "2026-04-23"
category: "Deep Learning Theory"
raw_source: "raw/poly-attention-openreview.md"
keywords:
  - attention-mechanism
  - higher-order
  - transformers
  - polynomial-attention
---

# Poly-attention: A general scheme for higher-order self-attention

## Summary

TL;DR: This article generalizes higher-order self attention, studies their representational strengths and computational complexities, and characterizes all self-attention mechanisms computable in quadratic time.

- **Problem**: The self-attention mechanism, at the heart of the transformer model, is able to effectively model pairwise interactions between tokens.
- **Approach**: Our mechanisms can incorporate arbitrary higher-order (tensor) computations as well as arbitrary relationship structures between the input tokens, and they include the aforementioned alternatives as special cases.
- **Results**: Our results give interesting tradeoffs between different desiderata for these mechanisms, including a tight relationship between how expressive a mechanism is, and how large the coefficients in the model may be so that the mechanism can be approximated in almost-linear time.

Notably, we give a new attention mechanism which can be computed exactly in quadratic time, and which can perform function composition for any fixed number of functions.
- **Impact**: Prior mechanisms, even for just composing two functions, could only be computed in superquadratic time, and our new lower bounds show that faster algorithms for them are not possible.

**TL;DR:** This article generalizes higher-order self attention, studies their representational strengths and computational complexities, and characterizes all self-attention mechanisms computable in quadratic time..

## Abstract

The self-attention mechanism, at the heart of the transformer model, is able to effectively model pairwise interactions between tokens. However, numerous recent works have shown that it is unable to perform basic tasks involving detecting triples of correlated tokens, or compositional tasks where multiple input tokens need to be referenced to generate a result. Some higher-dimensional alternatives to self-attention have been proposed to address this, including higher-order attention (Sanford et al., 2023) and Strassen attention (Kozachinskiy et al., 2025), which can perform some of these polyadic tasks in exchange for slower, superquadratic running times.

In this work, we define a vast class of generalizations of self-attention, which we call poly-attention mechanisms. Our mechanisms can incorporate arbitrary higher-order (tensor) computations as well as arbitrary relationship structures between the input tokens, and they include the aforementioned alternatives as special cases. We then systematically study their computational complexity and representational strength, including giving new algorithms and matching complexity-theoretic lower bounds on the time complexity of computing the attention matrix exactly as well as approximately, and tightly determining which polyadic tasks they can each perform. Our results give interesting tradeoffs between different desiderata for these mechanisms, including a tight relationship between how expressive a mechanism is, and how large the coefficients in the model may be so that the mechanism can be approximated in almost-linear time.

Notably, we give a new attention mechanism which can be computed exactly in quadratic time, and which can perform function composition for any fixed number of functions. Prior mechanisms, even for just composing two functions, could only be computed in superquadratic time, and our new lower bounds show that faster algorithms for them are not possible.

**TL;DR:** This article generalizes higher-order self attention, studies their representational strengths and computational complexities, and characterizes all self-attention mechanisms computable in quadratic time.

## Review Summary

**Decision:** Accept (Poster)

**Reviewer ratings:**
- Rating: 6
- Rating: 4
- Rating: 4
- Rating: 6

See [OpenReview discussion](https://openreview.net/forum?id=amivrmQyvQ) for full reviews.

## Implementation Notes

- **OpenReview:** [amivrmQyvQ](https://openreview.net/forum?id=amivrmQyvQ)
- **Venue:** ICLR 2026 Poster
