---
title: "Challenges in Inference-Time Scaling with Uncertainty-Aware Tree Search"
url: "https://openreview.net/forum?id=KkornA17a3"
source: "openreview"
author: "Jacopo Minniti, Neil Band, Tim G. J. Rudner"
date: "2026-04-23"
captured: "2026-05-13"
tags:
  - iclr-2026
  - openreview
related:
  - "wiki/papers/uncertainty-tree.md"
---

# Challenges in Inference-Time Scaling with Uncertainty-Aware Tree Search

**OpenReview:** [KkornA17a3](https://openreview.net/forum?id=KkornA17a3)
**Venue:** TTU at ICLR 2026 (Main)

## Abstract

Inference-time search has emerged as a powerful paradigm for scaling large language models' reasoning capabilities. 
Standard approaches like beam search rely on process reward models (PRMs) for dense, step-by-step scoring to identify promising reasoning paths.
However, scaling these methods encounters a known failure mode: as compute budgets increase, search algorithms explore out-of-distribution states spuriously assigned high reward, decoupling proxy reward from actual reasoning ability. 
To address this, we propose Uncertainty-Aware Tree Search (UATS), which uses a process uncertainty model (PUM) to predict when PRM predictions are unreliable.
UATS dynamically allocates computational resources by increasing the branching factor at high-uncertainty nodes to resolve ambiguity through exploration, unlike the fixed branching of standard beam search.
In our evaluation, while PUMs perform well on held-out in-distribution data, this does not translate to improved downstream search. On instruction-tuned models, UATS matches standard beam search, but on RLVR-trained models, it consistently degrades performance as inference-time compute grows.
This negative result suggests that search-induced distribution shift causing poor PRM generalization similarly affects process uncertainty models. Our results suggest that uncertainty-guided inference-time scaling requires robust uncertainty quantification models that remain reliable under search-induced distribution shift.