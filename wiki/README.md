# Wiki

Curated knowledge base for ICLR 2026 research. Contains paper summaries, concept definitions, short summaries of raw captures, and longer-form synthesis articles — all cross-linked into a unified knowledge graph with references back to source material in [`raw/`](../raw/).

## Structure

```
wiki/
  papers/      # Paper summaries with contributions, findings, and notes
  concepts/    # Concept articles defining key ideas, methods, and topics
  summaries/   # Short summaries of individual raw/ entries
  articles/    # Longer-form articles synthesizing multiple sources into topic overviews
```

## Conventions

- Use standard markdown links (`[text](path)`) for all cross-references
- Every file **must** have YAML frontmatter (see schema below)
- Backlinks should be bidirectional: if A links to B, B should link back to A
- Concept pages are the backbone — they connect papers, raw captures, and articles

## Frontmatter schema

```yaml
---
title: "Concept or article title"
type: "concept | summary | article"
tags:
  - tag1
  - tag2
related:
  - "wiki/concepts/linked-concept.md"
sources:
  - "raw/slug.md"
  - "wiki/papers/paper-title.md"
---
```

### Field reference

| Field     | Required | Description                                        |
|-----------|----------|----------------------------------------------------|
| `title`   | ✅       | Title of the wiki page                              |
| `type`    | ✅       | One of: `concept`, `summary`, `article`             |
| `tags`    | ✅       | List of topic tags for indexing                     |
| `related` |          | Links to related wiki pages                         |
| `sources` |          | Links to source material in `raw/` or `wiki/papers/`  |

## Index

### Papers

- [AdAEM: An Adaptively and Automated Extensible Measurement of LLMs' Value Difference](papers/adaem-llm-value-measurement.md) — This paper proposes aa novel dynamic and automated evaluation framework to probe LLMs' value orientations and value differences
- [An Information-Theoretic Approach to Benign Leakage in Static Concept Embedding Models](papers/info-theoretic-benign-leakage.md) — Self-explanatory Concept Bottleneck Models (CBMs) integrate human-defined concepts into their internal representations to achieve interpretability,
- [Beyond Prompt-Induced Lies: Investigating LLM Deception on Benign Prompts](papers/beyond-prompt-induced-lies.md) — We detected the widespread deception of LLM under benign prompts and found its tendency increases with task difficulty.
- [Challenges in Inference-Time Scaling with Uncertainty-Aware Tree Search](papers/uncertainty-aware-tree-search.md) — Inference-time search has emerged as a powerful paradigm for scaling large language models' reasoning capabilities.
- [CoDeC: Detecting Data Contamination in LLMs via In-Context Learning](papers/codec-data-contamination-detection.md) — We propose Contamination Detection via Context (CoDeC), a simple, efficient, and model-agnostic method that detects training data contamination in LLMs by
- [Concept Bottleneck Diffusion for Steerable Generation](papers/concept-bottleneck-diffusion.md) — Recent work has brought the concept bottleneck architecture to the generative modeling space, adding a bottleneck inside of the typical model architecture to
- [Digging Deeper: Learning Multi-Level Concept Hierarchies](papers/digging-deeper-concept-hierarchies.md) — Concept-based models explain predictions using human-understandable concepts, but they typically rely on exhaustive annotations and treat concepts as flat and
- [EigenBench: A Comparative Behavioral Measure of Value Alignment](papers/eigenbench-value-alignment.md) — Aligning AI with human values is a pressing unsolved problem.
- [Extracting Representations in LLMs Robust to Distribution Shifts](papers/extracting-representations-llms-distribution-shifts.md) — CARE extracts true behavior representations from LLMs by separating them from dataset artifacts and context effects, enabling more robust behavior prediction,
- [How LR Decay Wastes Your Best Data in Curriculum-Based LLM Pretraining](papers/lr-decay-curriculum-pretraining.md) — Use model weight average to enhance curriculum learning in LLM pretraining.
- [How Reliable is Language Model Micro-Benchmarking?](papers/language-model-micro-benchmarking.md) — Micro-benchmarking offers a solution to the often prohibitive time and cost of language model development: evaluate on a very small subset of existing
- [Is it Thinking or Cheating? Detecting Implicit Reward Hacking by Measuring Reasoning Effort](papers/trace-reward-hacking-detection.md) — TRACE detects implicit reward hacking by measuring how quickly truncated reasoning suffices to pass verification, outperforming CoT monitoring and enabling
- [LLMs Get Lost In Multi-Turn Conversation](papers/llms-get-lost-in-multi-turn-conversation.md) — All 15 tested LLMs (from Llama-8B to Gemini 2.5 Pro) show an average 39% performance drop in multi-turn underspecified conversations versus single-turn, driven
- [Model Collapse Is Not a Bug but a Feature in Machine Unlearning for LLMs](papers/model-collapse-machine-unlearning.md) — We show that model collapse can be intentionally triggered to make LLMs unlearn specific information, turning it into a practical method for machine unlearning.
- [Poly-attention: A general scheme for higher-order self-attention](papers/poly-attention-higher-order.md) — This article generalizes higher-order self attention, studies their representational strengths and computational complexities, and characterizes all
- [Query Timing Produces Opposite Positional Biases Between LLMs and Humans](papers/query-timing-positional-biases.md) — Positional biases such as recency and primacy effects have been documented in large language models (LLMs), yet the underlying mechanism by which these models
- [Retain and Adapt: Auto-Balanced Model Editing for Open-Vocabulary Object Detection under Domain Shifts](papers/retain-and-adapt-model-editing.md) — We propose a hyperparameter-free auto-balanced model editing method that flexibly injects and learns new task knowledge into open-vocabulary detectors while
- [Sharpness-Aware Pretraining Mitigates Catastrophic Forgetting](papers/sharpness-aware-pretraining.md) — Downstream stability in language models depends on both pre-training loss and loss-landscape sharpness, with increased sharpness leading to greater
- [Simulating Concept Bottlenecks with Vision-Language Models](papers/simulating-concept-bottlenecks-vlm.md) — The paper shows how to turn a vision-language model into a concept bottleneck model by fine-tuning it to describe an image's concepts in natural language.
- [The Anatomy of Uncertainty in LLMs](papers/anatomy-of-uncertainty-llms.md) — A framework for decomposing uncertainty in LLMs.
- [The Missing Red Line: How Commercial Pressure Erodes AI Safety Boundaries](papers/missing-red-line-ai-safety.md) — Commercial system prompts can override AI safety training, causing models to recommend dangerous products and dismiss health risks, and most models show no
- [There Was Never a Bottleneck in Concept Bottleneck Models](papers/no-bottleneck-concept-bottleneck-models.md) — Deep learning representations are often difficult to interpret, which can hinder their deployment in sensitive applications.
- [Transformers are Inherently Succinct](papers/transformers-are-inherently-succinct.md) — Fixed-precision transformers (UHATs) are exponentially more succinct than LTL and RNNs, and doubly exponentially more succinct than finite automata, at
- [What's In My Human Feedback? Learning Interpretable Descriptions of Preference Data](papers/whats-in-my-human-feedback.md) — We present WIMHF, a method to describe the preferences encoded by human feedback; produce insights from seven widely-used datasets; and show that the method
- [When Can You TRUST Large Language Models?](papers/when-can-you-trust-llms.md) — Quantifying neural network model uncertainty is a difficult problem that has far-reaching implications on our ability to improve model reliability.
- [WRING Out the Bias: A Rotation-Based Alternative to Projection Debiasing](papers/wring-out-the-bias.md) — Vision-Language models (VLMs), including CLIP, are known to encode biases such as learning spurious correlations that falsely associate background attributes

### Concepts

- [Affective Computing](concepts/affective-computing.md) — Affective computing is the study and development of systems that can recognize, interpret, process, and simulate human affects (emotions, moods, personality).
- [Concept Bottleneck Models](concepts/concept-bottleneck-models.md) — Concept bottleneck models (CBMs) are architectures that route prediction through an intermediate layer of human-interpretable concepts before producing a
- [Concept Representation Learning](concepts/concept-representation-learning.md) — Concept representation learning is the problem of discovering or constructing latent variables that correspond to semantically meaningful, reusable, and often
- [Data Contamination](concepts/data-contamination.md) — Data contamination is the leakage of benchmark or evaluation content into a model's training data, post-training data, or cached synthetic data pipeline.
- [Edge of Stability](concepts/edge-of-stability.md) — The edge of stability is a phenomenon in neural network training where the largest eigenvalue of the Hessian hovers near the stability threshold 2/η (where η
- [Human-Robot Interaction](concepts/human-robot-interaction.md) — Human-robot interaction (HRI) studies how people perceive, relate to, and collaborate with physically embodied robotic agents.
- [Inference-Time Scaling](concepts/inference-time-scaling.md) — Inference-time scaling is the strategy of spending extra computation at test time — through sampling, search, tool use, verification, or deliberation — to
- [LLM Evaluation](concepts/llm-evaluation.md) — LLM evaluation is the study of how to measure model capability, reliability, alignment, and deployment risk in ways that survive contact with real use.
- [Marin Project](concepts/marin-project.md) — Marin is an openly-developed language model project led by Percy Liang at Stanford and OpenAthena.
- [Mechanistic Interpretability](concepts/mechanistic-interpretability.md) — Mechanistic interpretability aims to reverse-engineer the internal computations of neural networks by identifying interpretable features, circuits, and
- [Model Collapse](concepts/model-collapse.md) — Model collapse is the progressive narrowing or corruption of a model's learned distribution when training data are increasingly generated by models themselves
- [Multi-Turn Conversation](concepts/multi-turn-conversation.md) — Multi-turn conversation is the interactive setting where a user reveals intent, constraints, and corrections across several exchanges rather than in one fully
- [Neural Scaling Laws](concepts/neural-scaling-laws.md) — Neural scaling laws describe the empirical power-law relationships between model performance and factors such as model size, dataset size, and compute budget.
- [Open-Source AI](concepts/open-source-ai.md) — Open-source AI refers to the practice of making the full stack of an AI system — model weights, training code, data recipes, and development process — publicly
- [Reward Hacking](concepts/reward-hacking.md) — Reward hacking occurs when a model finds outputs that score well under a proxy reward, judge, or verifier while failing the task a human actually intended.
- [Self-Consuming AI](concepts/self-consuming-ai.md) — Self-consuming AI describes a feedback regime in which models are increasingly trained, adapted, or evaluated on content produced by earlier models.
- [Socially Assistive Robotics](concepts/socially-assistive-robotics.md) — Socially assistive robotics (SAR) is a subfield of robotics focused on creating robots that provide assistance through social interaction rather than physical
- [Uncertainty in LLMs](concepts/uncertainty-in-llms.md) — Uncertainty in LLMs is the problem of representing when a model's answer should be treated as ambiguous, undersupported, unstable, or otherwise unreliable.
- [Value Alignment](concepts/value-alignment.md) — Value alignment is the problem of getting AI systems to behave in ways that are consistent with human values, norms, and constraints.
- [World Models](concepts/world-models.md) — World models are learned internal models of environment dynamics that support prediction, planning, and control.

### Summaries

#### Conference schedules
- [Summary: ICLR 2026 Conference Schedule](summaries/iclr-2026-conference-schedule.md) — Source: [raw/iclr-2026-conference-schedule.md](../raw/iclr-2026-conference-schedule.md)

#### Workshop and session pages
- [Summary: DATA-FM Workshop](summaries/iclr-2026-workshop-data-fm.md) — Source: [raw/iclr-2026-workshop-data-fm.md](../raw/iclr-2026-workshop-data-fm.md)
- [Summary: ICBINB LLMs Workshop](summaries/iclr-2026-workshop-icbinb-llms.md) — Source: [raw/iclr-2026-workshop-icbinb-llms.md](../raw/iclr-2026-workshop-icbinb-llms.md)
- [Summary: Lifelong Agents Workshop](summaries/iclr-2026-workshop-lifelong-agents.md) — Source: [raw/iclr-2026-workshop-lifelong-agents.md](../raw/iclr-2026-workshop-lifelong-agents.md)
- [Summary: Oral Session 2D — LLMs and Evaluation](summaries/iclr-2026-oral-session-2d-llms-evaluation.md) — Source: [raw/iclr-2026-oral-session-2d-llms-evaluation.md](../raw/iclr-2026-oral-session-2d-llms-evaluation.md)
- [Summary: Scientific Methods for Understanding Deep Learning (Sci4DL)](summaries/iclr-2026-workshop-sci4dl.md) — Source: [raw/iclr-2026-workshop-sci4dl/README.md](../raw/iclr-2026-workshop-sci4dl/README.md)
- [Summary: Trustworthy AI Workshop](summaries/iclr-2026-workshop-trustworthy-ai.md) — Source: [raw/iclr-2026-workshop-trustworthy-ai.md](../raw/iclr-2026-workshop-trustworthy-ai.md)
- [Summary: UniCRL Workshop](summaries/iclr-2026-workshop-unicrl-concept-representation.md) — Source: [raw/iclr-2026-workshop-unicrl-concept-representation.md](../raw/iclr-2026-workshop-unicrl-concept-representation.md)
- [Summary: World Models Workshop](summaries/iclr-2026-workshop-world-models.md) — Source: [raw/iclr-2026-workshop-world-models.md](../raw/iclr-2026-workshop-world-models.md)

#### Talks and expo talks
- [Summary: From Physics to AI to Materials — Max Welling (ICLR 2026)](summaries/iclr-2026-invited-talk-welling.md) — Source: [raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/](../raw/iclr-2026-invited-talk-from-physics-to-ai-to-materials-talk/)
- [Summary: Marin — Open Development of Frontier AI (ICLR 2026 Invited Talk)](summaries/iclr-2026-invited-talk-marin.md) — Source: [raw/iclr-2026-invited-talk-marin-open-development-frontier-ai-talk/](../raw/iclr-2026-invited-talk-marin-open-development-frontier-ai-talk/)
- [Summary: Prolific on Evaluation Infrastructure](summaries/prolific-evaluation-infrastructure-expo-talk.md) — Source: [raw/prolific-evaluation-infrastructure-expo-talk.md](../raw/prolific-evaluation-infrastructure-expo-talk.md)
- [Summary: Scale AI on Evaluation and RL Frontiers](summaries/scale-ai-new-frontier-eval-rl-expo-talk.md) — Source: [raw/scale-ai-new-frontier-eval-rl-expo-talk.md](../raw/scale-ai-new-frontier-eval-rl-expo-talk.md)
- [Summary: The Challenges of Human-Centered AI and Robotics](summaries/challenges-human-centered-ai-robotics.md) — Source: [raw/challenges-human-centered-ai-robotics-talk](../raw/challenges-human-centered-ai-robotics-talk)

#### Blogs and websites
- [Summary: Learning Mechanics](summaries/learningmechanics-pub.md) — Source: [raw/learningmechanics-pub.md](../raw/learningmechanics-pub.md)

### Articles

- [From Physics to AI to Materials: Max Welling on Waves, Thermodynamics, and the Responsibility of Building Powerful Tools](articles/welling-physics-ai-materials-talk.md) — In his ICLR 2026 keynote, Max Welling argues that physics offers deep structural insights that can shift paradigms in AI — not just incremental improvements.
- [How Does Gradient Descent Actually Work? Jeremy Cohen on the Edge of Stability](articles/edge-of-stability-cohen-talk.md) — In his invited talk at the Sci4DL workshop (ICLR 2026), Jeremy Cohen presented a compelling case that gradient descent in deep learning does *not* work the way
- [Karen Adolph on Infant Learning — Summary](articles/adolph-infant-learning-keynote.md) — Karen Adolph's keynote is one of the clearest reminders at ICLR 2026 that intelligence is not best understood as a static capability.
- [Katherine Bouman on Computational Imaging — Summary](articles/bouman-computational-imaging-keynote.md) — Katherine Bouman's keynote presents scientific imaging as a canonical example of AI working under uncertainty rather than in spite of it.
- [LLMs Get Lost in Multi-Turn Conversation — Summary](articles/llms-get-lost-multi-turn-talk.md) — The oral talk for LLMs Get Lost in Multi-Turn Conversation explains a deceptively simple failure mode: large language models perform substantially worse when
- [Maja Matarić on Human-Centered Robotics — Summary](articles/materic-robotics-keynote.md) — Maja Matarić's keynote argues that the next phase of AI will not be won by adding mobility to existing models alone.
- [Marin: How Open Development and Scaling Recipes Are Changing Frontier AI](articles/marin-open-development-frontier-ai.md) — Percy Liang's ICLR 2026 invited talk presents Marin, a frontier language model project built entirely in the open on GitHub.
- [Pablo Arbeláez on AI for Open Science — Summary](articles/arbelaez-ai-open-science-keynote.md) — Pablo Arbeláez's keynote is programmatic rather than narrowly technical, and that is part of its value.
- [Percy Liang on Open Development — Summary](articles/liang-percy-keynote.md) — Percy Liang's keynote, listed on ICLR's day-3 schedule as "Marin: Open Development of Frontier AI," argues that the central scarcity in frontier AI is no
- [Prolific on Evaluation Infrastructure — Summary](articles/prolific-ai-leaderboard-talk.md) — Prolific's expo talk, captured in the raw summary page, starts from a now-familiar complaint about frontier AI: models are improving faster than our
- [Richard Baraniuk on Self-Consuming Loops — Summary](articles/baraniuk-self-consuming-loops-talk.md) — Richard Baraniuk's Sci4DL talk asks what happens when generative models begin to train on their own outputs.
- [Scale AI on Evaluation and RL Frontiers — Summary](articles/scale-ai-eval-rl-talk.md) — Scale AI's expo talk, captured here, argues that the next capability bottleneck for large language models is not raw scale but verification.
- [Some Insights into LLM Reasoning: Julia Kempe on Why RL Unlocks Chain-of-Thought](articles/kempe-llm-reasoning-insights.md) — In her Sci4DL invited talk, Julia Kempe presents a clean mechanistic explanation for why reinforcement learning with verifiable rewards (RLVF) dramatically
- [What's In My Human Feedback? — Summary](articles/wimhf-human-feedback-talk.md) — The WIMHF talk asks a question that much of post-training still leaves oddly underspecified: what exactly is encoded in human preference data?
- [Workshop: I Can't Believe It's Not Better — Where LLMs Need to Improve — Key Takeaways](articles/icbinb-llms-workshop.md) — The ICBINB LLMs workshop is organized around a simple scientific norm: negative results should be treated as signal, not embarrassment.
- [Workshop: Lifelong Agents: Learning, Aligning, Evolving — Key Takeaways](articles/lifelong-agents-workshop.md) — The Lifelong Agents workshop framed a clear agenda: agents should not be trained once and then frozen, but should instead keep learning, stay aligned with
- [Workshop: Navigating and Addressing Data Problems For Foundation Models (DATA-FM) — Key Takeaways](articles/data-fm-workshop.md) — The DATA-FM workshop makes a strong claim that data remains the decisive design variable in foundation-model development.
- [Workshop: Principled Design for Trustworthy AI — Key Takeaways](articles/trustworthy-ai-workshop.md) — The Trustworthy AI workshop is unusually broad without becoming vague.
- [Workshop: World Models — Understanding, Modelling and Scaling — Key Takeaways](articles/world-models-workshop.md) — The World Models workshop is one of the clearest places in the repo where “world model” means more than generative prediction.

## Maintaining the wiki

- **`wiki-update`** skill — Scans for new content and updates summaries, concepts, and backlinks
- **`wiki-article`** skill — Synthesizes multiple sources into a longer-form article
