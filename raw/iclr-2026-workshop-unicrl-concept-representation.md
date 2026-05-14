---
title: "Unifying Concept Representation Learning (UniCRL Workshop)"
url: "https://iclr.cc/virtual/2026/workshop/10000775"
source: "other"
author: "ICLR 2026"
date: "2026-04-26"
captured: "2026-05-13"
tags:
  - iclr-2026
  - workshop
  - concept-learning
  - neuro-symbolic
  - explainability
  - causal-representation-learning
aliases:
  - "UniCRL Workshop"
  - "Unifying Concept Representation Learning"
related:
  - "wiki/concepts/mechanistic-interpretability.md"
---

# Unifying Concept Representation Learning

**ICLR 2026 Workshop** — Sun, Apr 26, 2026 · 9:00 AM – 5:00 PM (BRT, UTC-3)

## Abstract

Several areas at the forefront of AI research are currently witnessing a convergence of interests around the problem of learning high-quality concepts from data. Concepts have become a central topic of study in neuro-symbolic integration (NeSy). NeSy approaches integrate perception — usually implemented by a neural backbone — and symbolic reasoning by employing concepts to glue together these two steps: the latter relies on the concepts detected by the former to produce suitable outputs.

Concepts are also used in Explainable AI (XAI) by recent post-hoc explainers and self-explainable architectures as a building block for constructing high-level justifications of model behavior. Compared to saliency maps, these can portray a more abstract and understandable picture of the machine's reasoning process, potentially improving understandability, interactivity, and trustworthiness — to the point that concepts have been called the *lingua franca* of human-AI interaction.

Both areas hinge on learned concepts being "high-quality". Causal Representation Learning (CRL) aims to identify latent causal variables and causal relations from high-dimensional observations (e.g., images or text) with theoretical guarantees. CRL is a generalization of disentangled representation learning when latent variables depend on each other due to causal relations.

This workshop brings together researchers from NeSy, XAI, and CRL — from both industry and academia — who are interested in learning robust, semantically meaningful concepts. It aims to tie together these currently independent strands of research and promote cross-fertilization.

## Schedule

### Morning Session

| Time | Event | Speaker |
|------|-------|---------|
| 9:00 AM | Introduction | — |
| 9:10 AM | **Invited talk**: Causal effects in the eyes of the beholder | Francesco Locatello |
| 9:40 AM | **Invited talk**: Learning Programming Abstractions for Automating Formal Verification | Jocelyn Qiaochu Chen |
| 10:10 AM | Coffee break | — |
| 10:30 AM | **Contributed talk**: Navigating the Concept Space of Language Models | Wilson Marcilio Jr |
| 10:45 AM | **Contributed talk**: Diagnosing and Fixing Latent Recovery in Sparse Autoencoders | Marco Fumero |
| 11:00 AM | **Poster session 1** | — |
| 12:00 PM | Lunch | — |

### Afternoon Session

| Time | Event | Speaker |
|------|-------|---------|
| 1:00 PM | **Invited talk**: Learning Causal Systems in the Latent Space | Biwei Huang |
| 1:30 PM | **Invited talk**: In Defense of Concept Leakage | Mateo Espinosa Zarlenga |
| 2:00 PM | **Contributed talk**: Automated Concept Discovery for LLM-as-a-Judge Preference Analysis | James Wedgwood |
| 2:15 PM | **Invited talk**: Humans & LLMs: Two Great Systems Separated by a Common Language | Subbarao Kambhampati |
| 2:45 PM | **Invited talk**: Expanding our concepts with help of agents | Been Kim |
| 3:15 PM | Coffee break | — |
| 3:30 PM | **Contributed talk**: Dynamics Reveals Structure: Challenging the Linear Propagation Assumption | Hoyeon Chang |
| 3:45 PM | **Contributed talk**: Automatic Interpretation of Visual Concepts | Felix Meissen |
| 4:00 PM | **Poster session 2** | — |

## Poster Session Papers

### Poster Session 1 (11:00 AM)

- Concept Bottleneck Diffusion for Steerable Generation — Eric Enouen, Sainyam Galhotra
- Multi-shot AutoInterp: Agents Can Explain Complex Features By Refining Explanations — Kamal Maher, Simon Elias Schrader, Kola Ayonrinde
- Causality Guided Representation Learning for Cross-Style Hate Speech Detection — Chengshuai Zhao et al.
- SSCD: Sparse Semantic Concept Defense Against Semantic Adversarial Attacks — Nghia Nguyen et al.
- Decomposing Representation Drift via Interventions — Thomas Chen, Daniel Xu
- Continual Learning and Refinement of Causal Models through Dynamic Predicate Invention — Enrique Crespo Fernandez et al.
- An Information-Theoretic Approach to Benign Leakage in Static Concept Embedding Models — Tianchao Li et al.
- Do Monolingual Language Models Learn Cross-Lingual Universal Conceptual Representations? — Suchir Salhan et al.
- Gluing Local Contexts into Global Meaning: A Sheaf-Theoretic Decomposition of Transformer Representations — Bryce Grant, Peng Wang
- One Language, Two Scripts: Probing Script-Invariance in LLM Concept Representations — Sripad Karne
- Post-hoc Self-explanation of CNNs — Ahcene Boubekki, Line Clemmensen
- Simulating Concept Bottlenecks with Vision-Language Models — Karim Galliamov et al.
- Self-Interpretable Concept Representations: Training Lightweight Adapters on Vector-Label Pairs — Keenan Pepper et al.
- Identifiable Estimation of Causal Concept Effects under Visual Latent Confounding — Thomas Melistas et al.
- Automated Concept Discovery for LLM-as-a-Judge Preference Analysis — James Wedgwood et al.
- Syntax-Preserving Hyperbolic Visual-Semantic Embeddings — Genji Ohara et al.
- Dynamics Reveals Structure: Challenging the Linear Propagation Assumption — Hoyeon Chang et al.
- NEUROLOGIC: From Neural Representations to Interpretable Logic Rules — Chuqin Geng et al.
- Navigating the Concept Space of Language Models — Wilson Marcilio Jr, Danilo Eler
- Extracting Representations in LLMs Robust to Distribution Shifts — Sweta Karlekar et al.
- VLC Fusion: Vision-Language Conditioned Sensor Fusion for Robust Object Detection — Aditya Taparia et al.
- Diagnosing and Fixing Latent Recovery in Sparse Autoencoders — Zhenyu Zhu et al.
- Digging Deeper: Learning Multi-Level Concept Hierarchies — Oscar Hill et al.
- Automatic Interpretation of Visual Concepts — Felix Meissen et al.
- Post-hoc Stochastic Concept Bottleneck Models — Wiktor Hoffmann et al.
- On the Existence and Behavior of Secondary Attention Sinks — Jeffrey T. H. Wong et al.

## Key Themes

- **Neuro-symbolic integration (NeSy)** — Using concepts to bridge neural perception and symbolic reasoning
- **Concept bottleneck models** — Architectures that force predictions through interpretable concept layers
- **Causal representation learning (CRL)** — Identifying latent causal variables from high-dimensional observations
- **Concept leakage** — When unintended information flows through concept representations
- **Sparse autoencoders** — Techniques for discovering interpretable features in neural networks
- **LLM concept representations** — How language models organize and represent conceptual knowledge
