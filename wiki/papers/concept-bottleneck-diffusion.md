---
title: "Concept Bottleneck Diffusion for Steerable Generation"
authors: "Eric Enouen, Sainyam Galhotra"
affiliations: "Cornell University"
url: "https://openreview.net/forum?id=yP7ReFvRGN"
date: "2026-04-23"
category: "Generative Models"
raw_source: "raw/concept-diffusion-openreview.md"
keywords:
  - concept-bottleneck
  - diffusion-models
  - steerable-generation
  - interpretable-generation
---

# Concept Bottleneck Diffusion for Steerable Generation

## Summary

TL;DR: Recent work has brought the concept bottleneck architecture to the generative modeling space, adding a bottleneck inside of the typical model architecture to force interpretable reasoning. While this approach is flexible and can be applied to a variety of generative models, such architectural bottlenecks are better suited for single-step models like GANs than for diffusion models, which operate across a sequence of timesteps.

- **Problem**: Recent work has brought the concept bottleneck architecture to the generative modeling space, adding a bottleneck inside of the typical model architecture to force interpretable reasoning.
- **Approach**: In contrast, we place the bottleneck directly in the latent space used by a latent diffusion model, performing denoising along concept channels rather than in pixel space.
- **Results**: By reshaping the latent space in which diffusion occurs, we learn a denoising process that is inherently aligned with the concepts we aim to control, enabled by our novel concept masking procedure.
- **Impact**: Our method, CBDiffuse, achieves improved steerability and control compared to prior work across CelebA-HQ and CUB..

## Abstract

Recent work has brought the concept bottleneck architecture to the generative modeling space, adding a bottleneck inside of the typical model architecture to force interpretable reasoning. While this approach is flexible and can be applied to a variety of generative models, such architectural bottlenecks are better suited for single-step models like GANs than for diffusion models, which operate across a sequence of timesteps. This mismatch limits steerability and interpretability over the full generative process. In contrast, we place the bottleneck directly in the latent space used by a latent diffusion model, performing denoising along concept channels rather than in pixel space. By reshaping the latent space in which diffusion occurs, we learn a denoising process that is inherently aligned with the concepts we aim to control, enabled by our novel concept masking procedure. Our method, CBDiffuse, achieves improved steerability and control compared to prior work across CelebA-HQ and CUB.


## Implementation Notes

- **OpenReview:** [yP7ReFvRGN](https://openreview.net/forum?id=yP7ReFvRGN)
- **Venue:** UCRL@ICLR2026 Poster
