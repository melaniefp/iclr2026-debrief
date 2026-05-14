---
title: "LLMs Get Lost In Multi-Turn Conversation"
authors: "Philippe Laban, Hiroaki Hayashi, Yingbo Zhou, Jennifer Neville"
affiliations: "Microsoft Research, Salesforce Research"
url: "https://arxiv.org/abs/2505.06120"
date: "2025-05-09"
category: "LLM Evaluation"
raw_source: "raw/llms-get-lost-in-multi-turn-conversation-src/"
keywords:
  - multi-turn evaluation
  - LLM reliability
  - underspecification
  - sharded simulation
---

# LLMs Get Lost In Multi-Turn Conversation

## Summary

TL;DR: All 15 tested LLMs (from Llama-8B to Gemini 2.5 Pro) show an average 39% performance drop in multi-turn underspecified conversations versus single-turn, driven primarily by a massive increase in unreliability rather than loss of aptitude — they make early wrong assumptions and never recover.

- **Universal multi-turn degradation**: Every model tested — including frontier models (GPT-4.1, Gemini 2.5 Pro, Claude 3.7 Sonnet) and reasoning models (o3, DeepSeek-R1) — shows 30–40% performance drops when instructions are revealed gradually across conversation turns vs. given all at once ([Table 1](https://arxiv.org/html/2505.06120#S5.T1)).
- **Unreliability, not aptitude, is the main culprit**: Decomposing degradation into aptitude ($A^{90}$, 90th-percentile performance) and unreliability ($U_{10}^{90}$, gap between 10th and 90th percentiles), the authors find aptitude drops only ~16% while unreliability more than doubles (+112%). All models show ~50-point unreliability in multi-turn settings regardless of their single-turn strength ([Figure 3b](https://arxiv.org/html/2505.06120#S5.F3)).
- **Sharded simulation methodology**: The paper introduces "sharded simulation" — splitting single-turn benchmark instructions into ordered shards revealed one per turn — enabling controlled comparison on the same underlying tasks. Five simulation types (Full, Concat, Sharded, Recap, Snowball) isolate the effect of multi-turn underspecification ([Section 2.3](https://arxiv.org/html/2505.06120#S2.SS3)).
- **Root causes identified**: Four behavioral patterns drive degradation: (1) premature answer attempts with incorrect assumptions, (2) answer bloat from over-reliance on prior incorrect solutions (20–300% longer answers), (3) loss-in-middle-turns (analogous to lost-in-the-middle for context), and (4) overly verbose responses that introduce confusing assumptions ([Appendix D](https://arxiv.org/html/2505.06120#A4)).
- **Known mitigations fail**: Lowering temperature to 0.0 is ineffective for multi-turn reliability (unreliability remains ~30% even at T=0). Agent-like recap/snowball strategies recover only 15–20% of the gap. Reasoning tokens (o3, R1) do not help — reasoning models degrade similarly ([Section 6.2](https://arxiv.org/html/2505.06120#S6.SS2), [Table 2](https://arxiv.org/html/2505.06120#S6.T2)).

## Contributions

### 1. Sharded simulation framework

The paper's central methodological contribution is "sharded simulation" — a controlled framework for comparing LLM performance in single-turn vs. multi-turn settings on identical tasks ([Section 2](https://arxiv.org/html/2505.06120#S2)). A fully-specified instruction $q$ is decomposed into atomic content units:

$$
I(q) = [\mathcal{I}, (c_1, \ldots, c_m)]
$$

where $\mathcal{I}$ is the primary intent and $c_i$ are clarifications. These are converted to shards $[s_1, \ldots, s_k]$ satisfying five properties: information preservation, clear initial intent, order insensitivity, maximal sharding, and minimal transformation ([Appendix B](https://arxiv.org/html/2505.06120#A2)). This is contrasted with prior multi-turn benchmarks (MT-bench, BFCL) that use *episodic* tasks where each turn is independently evaluable.

### 2. Aptitude vs. reliability decomposition

The paper introduces a principled decomposition of LLM performance into aptitude and reliability using percentile-based metrics ([Section 3.2](https://arxiv.org/html/2505.06120#S3.SS2)):

$$
A^{90} = \text{percentile}_{90}(S), \quad U_{10}^{90} = \text{percentile}_{90}(S) - \text{percentile}_{10}(S)
$$

where $S = \{S_i\}_{i=1}^N$ are scores from $N=10$ repeated simulations per instruction. In single-turn settings, higher aptitude correlates with higher reliability. In multi-turn settings, this correlation breaks down entirely — all models converge to similar high unreliability.

### 3. Qualitative behavioral analysis

Four root causes of multi-turn degradation are identified through analysis of 200,000+ simulated conversations:

1. **Premature answer attempts** — Models that delay first answer attempts to the last 20% of the conversation score 64.4 avg vs. 30.9 for those answering in the first 20% ([Table 5, Appendix D.1](https://arxiv.org/html/2505.06120#A4.SS1)).
2. **Answer bloat** — Multi-turn answer attempts grow 20–300% longer than single-turn equivalents, with even *correct* solutions being 14–27% longer ([Appendix D.2](https://arxiv.org/html/2505.06120#A4.SS2)).
3. **Loss-in-middle-turns** — Citation analysis in the summary task shows documents from middle turns are cited 50% less than those from first/last turns ([Figure 9, Appendix D.3](https://arxiv.org/html/2505.06120#A4.F9)).
4. **Over-verbosity** — Shortest-response simulations outperform longest-response simulations by 10–50% across 5 of 6 tasks ([Table 6, Appendix D.4](https://arxiv.org/html/2505.06120#A4.SS4)).

## Empirical findings

### Tasks and benchmarks

Six generation tasks across programming and natural language ([Section 3.1](https://arxiv.org/html/2505.06120#S3.SS1), [Figure 2](https://arxiv.org/html/2505.06120#S3.F2)):

| Task | Source benchmark | Metric | # Instructions |
|------|-----------------|--------|----------------|
| Code | HumanEval + LiveCodeBench | Functional accuracy | 145 |
| Database | Spider (text-to-SQL) | Execution accuracy | 107 |
| Actions | BFCL v3 (function calling) | Semantic match | 105 |
| Math | GSM8K | Numerical accuracy | ~100 |
| Data-to-text | ToTTo | BLEU | ~100 |
| Summary | Summary of a Haystack | Joint Score (LLM judge) | ~100 |

### Main results ([Table 1](https://arxiv.org/html/2505.06120#S5.T1))

| Model | Full avg | Sharded avg | Degradation |
|-------|---------|------------|-------------|
| Gemini 2.5 Pro | 78.1 | 47.3 | 64.5% retained |
| GPT-4.1 | 76.2 | 49.0 | 61.8% retained |
| DeepSeek-R1 | 72.9 | 42.4 | 60.8% retained |
| GPT-4o | 73.0 | 44.6 | 57.9% retained |
| Claude 3.7 Sonnet | 71.3 | 43.8 | 65.9% retained |
| Llama 3.1-8B | 43.3 | 24.5 | 62.5% retained |

Key: **Concat** simulations retain ~95% of Full performance, confirming that degradation is specifically from multi-turn underspecification, not from rephrasing during sharding.

### Mitigation experiments ([Table 2](https://arxiv.org/html/2505.06120#S6.T2))

| Mitigation | Recovery |
|-----------|----------|
| Recap (final-turn recapitulation) | Partial (~25% gap recovery) |
| Snowball (turn-level recapitulation) | 15–20% gap recovery |
| Temperature = 0.0 | Ineffective (unreliability remains ~30%) |
| Reasoning models (o3, R1) | No benefit vs. non-reasoning |

### Gradual sharding experiment ([Figure 3c](https://arxiv.org/html/2505.06120#S5.F3))

Any conversation with ≥2 turns triggers the lost-in-conversation phenomenon. Increasing from 2 to 8 shards shows minimal additional degradation — the degradation onset is binary (1 turn = OK, ≥2 turns = degraded).

### Episodic vs. underspecified tasks

A 7th task (Translation) was tested as a control. Translation is episodic (each turn adds independently translatable sentences) and shows **no** degradation in multi-turn settings, confirming that the effect is specific to underspecified, non-decomposable tasks ([Table 3](https://arxiv.org/html/2505.06120#S6.T3)).

## Notes from summaries of related work

No directly related paper summaries exist in the wiki. However, the oral session capture `raw/iclr-2026-oral-session-2d-llms-evaluation.md` lists this paper as one of the orals in Session 2D, noting it received an **Outstanding Paper Award** at ICLR 2026.

## Implementation notes

- **GitHub**: [Microsoft/lost_in_conversation](https://github.com/Microsoft/lost_in_conversation)
- **Dataset**: [HuggingFace: Microsoft/lost_in_conversation](https://huggingface.co/datasets/Microsoft/lost_in_conversation)
- **User simulator**: GPT-4o-mini used as user simulator, strategy classifier, and answer extractor
- **15 models tested**: Llama 3.1-8B, OLMo-2-13B, Claude 3 Haiku, GPT-4o-mini, Llama 3.3-70B, Phi-4, Command-A, Llama 4 Scout, o3, Claude 3.7 Sonnet, DeepSeek-R1, GPT-4o, Gemini 2.5 Flash, GPT-4.1, Gemini 2.5 Pro
- **Scale**: 200,000+ simulated conversations, N=10 simulations per (model, instruction, type) triple, estimated cost ~$5,000
- **Temperature**: Default T=1.0 for main experiments; supplementary experiment with T ∈ {0.0, 0.5, 1.0}
- **Max response length**: 1,000 tokens (10,000 for reasoning models)
- **Simulation error rate**: <5% of conversations affected by simulator errors, <2% disfavoring assistant
- **Conference**: ICLR 2026, Outstanding Paper Award
