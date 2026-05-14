---
title: "Workshop: I Can't Believe It's Not Better — Where LLMs Need to Improve"
url: "https://iclr.cc/virtual/2026/workshop/10000772"
source: "other"
author: "ICLR 2026"
date: "2026-04-27"
captured: "2026-05-13"
tags:
  - iclr-2026
  - workshop
  - llm-evaluation
  - llm-limitations
aliases:
  - "ICLR 2026 ICBINB LLMs Workshop"
related:
  - "raw/iclr-2026-oral-session-2d-llms-evaluation.md"
  - "wiki/articles/icbinb-llms-workshop.md"
---

# Workshop description

* **Date/time:** Mon, Apr 27, 2026 · 9:00 AM–5:00 PM -03
* **Timezone on page:** America/Sao_Paulo
* **Venue:** 201 C
* **SlidesLive presentation IDs:** 39063694

Large language models (LLMs) have advanced rapidly, yet these advances have also highlighted gaps, such as hallucination, brittle reasoning, alignment failures, and hard efficiency/scaling constraints, especially in safety-critical settings. Ideally, evidence of such limitations would immediately lead to improvements to address these gaps, but compute constraints and unfruitful approaches often stall iteration; meanwhile, publication norms still prioritize positive results over informative null or negative findings. This workshop creates a venue for negative results on LLMs including: (i) rigorous studies that demonstrate and analyze limitations (e.g., leak-resistant reasoning probes, alignment stress tests, failure audits in critical applications), and (ii) attempts on well-established ideas that did not deliver expected gains, with analyses that identify failure modes, boundary conditions, and lessons learned. We welcome diagnostics, replications, counterfactual evaluations, and ablations that separate genuine capability from shortcut learning and clarify when methods break, why they break, and how to fix them. By aggregating evidence of negative results and actionable takeaways, the workshop aims to convert setbacks into robust principles and practices for building more reliable LLMs.

# Schedule

| Time | Event | Speakers |
| --- | --- | --- |
| 9:00 AM | Opening Remarks - Welcome & Introduction to ICBINB | Arno Blaas ⋅ Fan Feng ⋅ Jennifer Williams |
| 9:10 AM | Invited Talk by Adam Block: When Best-of-N is Worse: Coverage, Reward Hacking, and Pessimism in Inference-Time Alignment | Adam Block |
| 9:45 AM | Spotlight Talk: Lost in Translation: Why SOTA LLMs Struggle with French NLU Frontiers | — |
| 9:50 AM | Spotlight Talk: Sharpness-Aware Pretraining Mitigates Catastrophic Forgetting | — |
| 9:55 AM | Spotlight Talk: Attention Sinks as Internal Signals for Hallucination Detection in Large Language Models | — |
| 10:00 AM | Coffee Break | — |
| 10:30 AM | Invited Talk by Marta Garnelo: Tree-vial Pursuits: How Humble Decision Trees Still Outsmart the Generative Giants | Marta Garnelo |
| 11:00 AM | Spotlight Talk: Fairness Failure Modes of Multimodal LLMs | — |
| 11:10 AM | Spotlight Talk: I Can’t Believe It’s Not Safer: Preference–Safety Disassociation in Clinical LLM Evaluation | — |
| 11:15 AM | Spotlight Talk: Voice Evaluation of Reasoning Ability: Diagnosing the Modality-Induced Performance Gap | — |
| 11:20 AM | Invited Talk by Aditi Raghunathan: The Creative Limits of Next-token Prediction | Aditi Raghunathan |
| 11:55 AM | Lunch Break | — |
| 1:00 PM | Poster Session | — |
| 2:25 PM | Invited Talk by Preslav Nakov: Towards Truly Open, Language-Specific, Safe, Factual, and Specialized Large Language Models | Preslav Nakov |
| 3:00 PM | Coffee Break | — |
| 3:30 PM | Invited Talk by Sewon Min: Are Mixture-of-Experts Modular? Why It Matters and How to Fix It | Sewon Min |
| 4:05 PM | Panel Discussion: Where Large Language Models Need to Improve | Preslav Nakov ⋅ Marta Garnelo ⋅ Samy Bengio ⋅ Sewon Min |
| 4:55 PM | Closing Remarks - Thanks & Awards | Arno Blaas ⋅ Fan Feng ⋅ Jennifer Williams |

# Invited talks

## When Best-of-N is Worse: Coverage, Reward Hacking, and Pessimism in Inference-Time Alignment

**Speaker:** Adam Block

Inference-time scaling has emerged as a powerful way to improve language models, but its simplest form, Best-of-N (BoN) sampling, has a delicate failure mode. While additional samples can substantially improve outputs, in the presence of imperfect verifiers, BoN can amplify reward-hacking by over-optimizing to the learned reward model. In this talk, we will discuss a perspective on inference-time alignment centered on this tension. I will argue that the performance of BoN is governed by three key ingredients: the coverage of the reference model, the quality of the reward model, and the metric used to measure success. We will see that, under appropriate coverage assumptions, BoN can be optimal for improving expected reward, but that these guarantees do not by themselves rule out sever reward hacking or poor win-rate performance. This helps explain why seemingly contradictory conclusions can all be correct, depending on what objective is being optimized and how inference-time success is measured. Motivated by this, I will then discuss pessimistic alternatives to standard BoN, including methods that use uncertainty estimates at inference time to penalize suspicious high-reward responses. These approaches retain the benefits of additional inference-time compute while mitigating over-optimization to flawed verifiers. Overall, the talk will argue that making language models better at inference time is not just a question of scaling up search, but of understanding when extra compute is pointed in the wrong direction.

## Tree-vial Pursuits: How Humble Decision Trees Still Outsmart the Generative Giants

**Speaker:** Marta Garnelo

Large Language Models have redefined our expectations for what AI can achieve, showing remarkable prowess in natural language, complex reasoning, and code synthesis. Given these leaps, it is tempting to assume that numerical fluency would follow as a natural byproduct of scale. However, the reality is far more humbling: even the most sophisticated LLMs often fail spectacularly at basic tabular prediction tasks. This gap is a significant bottleneck, considering that the vast majority of the world’s enterprise and scientific data remains locked in rows and columns. In this talk we investigate the dissonance between a model's linguistic confidence and its actual predictive performance and we explore where our false perception of the LLMs' numerical mastery could stem from.

## The Creative Limits of Next-token Prediction

**Speaker:** Aditi Raghunathan

Current LLM pipelines rely on a convenient illusion: that scaling next-token prediction and tweaking temperature naturally unlocks diverse, open-ended generation. In reality, standard autoregression is fundamentally myopic. We quantify this using minimal algorithmic tasks that require far-sighted stochastic planning. In these environments, next-token learning fails to plan, whereas multi-token approaches excel. Furthermore, standard output-layer temperature sampling degrades coherence in its attempt to elicit randomness. Surprisingly, simply injecting noise directly at the input layer (seed-conditioning) works as well, if not better. This same diversity collapse plagues test-time compute scaling for math reasoning, where standard decoding merely regurgitates redundant errors. Yet, applying a simple mode-conditioning (ModC) prefix forces the model to explore distinct reasoning paths, instantly yielding a 4x efficiency gain.

## Towards Truly Open, Language-Specific, Safe, Factual, and Specialized Large Language Models

**Speaker:** Preslav Nakov

As large language models increasingly shape knowledge, communication, and creativity, it is imperative that we make them open, language-specific, safe, factual, and specialized. First, we will argue for the need for fully transparent open-source large language models (LLMs), and we will describe the efforts of MBZUAI's Institute on Foundation Models (IFM) towards that based on the LLM360 initiative. Second, we will argue for the need for language-specific LLMs, and we will share our experience from building Jais, the world's leading open Arabic-centric foundation and instruction-tuned large language model, Nanda, our open-weights Hindi LLM, Sherkala, our open-weights Kazakh LLM, and some other models. Third, we will argue for the need for safe LLMs, and we will present Do-Not-Answer, a dataset for evaluating the guardrails of LLMs, which is at the core of the safety mechanisms of our LLMs. Fourth, we will argue for the need for factual LLMs, we will discuss the factuality challenges that LLMs pose. We will then present some recent relevant tools for addressing these challenges developed at MBZUAI: (i) OpenFactCheck, a framework for fact-checking LLM output, for building customized fact-checking systems, and for benchmarking LLMs for factuality, (ii) LM-Polygraph, a tool for predicting an LLM's uncertainty in its output using cheap and fast uncertainty quantification techniques, and (iii) LLM-DetectAIve, a tool for machine-generated text detection. Finally, we will argue for the need for specialized models, and we will present some other LLMs currently being developed at MBZUAI's IFM.

## Are Mixture-of-Experts Modular? Why It Matters and How to Fix It

**Speaker:** Sewon Min

Mixture-of-Experts (MoEs) are designed as modular architectures—but are they functionally modular, i.e., enabling the independent use of expert subsets for downstream domains? We argue they are not, and that this gap matters: as MoEs grow larger, sparser, and more fine-grained, they become increasingly difficult to use, adapt, and fine-tune without heavy infrastructure. We introduce ModMoE, a self-supervised approach that makes modularity a first-class property—without human priors or loss in overall performance. ModMoE induces semantically specialized experts (rather than lexical partitioning) and enables effective selective expert usage across pool sizes, improving efficiency and performance in both zero-shot inference and fine-tuning. These results point toward more accessible and flexible MoEs, and a path to large-scale, sparse, and truly modular expert architectures.

# Contributed talks

- **Lost in Translation: Why SOTA LLMs Struggle with French NLU Frontiers** — David Beauchemin ⋅ Yan Tremblay ⋅ Mohamed Youssef ⋅ Richard Khoury
- **Sharpness-Aware Pretraining Mitigates Catastrophic Forgetting** — Ishaan Watts ⋅ Catherine Li ⋅ Sachin Goyal ⋅ Jacob Springer ⋅ Aditi Raghunathan
- **Attention Sinks as Internal Signals for Hallucination Detection in Large Language Models** — Jakub Binkowski ⋅ Kamil Adamczewski ⋅ Tomasz Kajdanowicz
- **Fairness Failure Modes of Multimodal LLMs** — Canyu Chen ⋅ Anglin Cai ⋅ Joan Nwatu ⋅ Yale Li ⋅ Han Liu ⋅ Jessica Hullman ⋅ Rada Mihalcea ⋅ Kathleen McKeown ⋅ Manling Li
- **I Can’t Believe It’s Not Safer: Preference–Safety Disassociation in Clinical LLM Evaluation** — Fay Elhassan ⋅ David Sasu ⋅ Lars Klein ⋅ Alexandra Kulinkina ⋅ Mary-Anne Hartley
- **Voice Evaluation of Reasoning Ability: Diagnosing the Modality-Induced Performance Gap** — Yueqian Lin ⋅ Zhengmian Hu ⋅ Qinsi Wang ⋅ Yudong Liu ⋅ Hengfan Zhang ⋅ Jayakumar Subramanian ⋅ Nikos Vlassis ⋅ Hai Li ⋅ Yiran Chen

# Poster papers

- **Evaluation-Conditioned Trojan Attack** — Zihan Zhu ⋅ Hanlin Zhang ⋅ Giovanni D'Antonio ⋅ Anton Tsitsulin ⋅ Sham Kakade ⋅ Vahab Mirrokni
- **Can LLMs Perceive Time? An Empirical Investigation** — Aniketh Garikaparthi
- **Language-Dependent Miscalibration in Multilingual LLM Evaluators** — Ej Zhou ⋅ Lucas Resck ⋅ Zheng Hui ⋅ Anna Korhonen
- **WHEN STABILITY FAILS: HIDDEN FAILURE MODES OF LLMS IN DATA-CONSTRAINED SCIENTIFIC DECISION-MAKING** — Nazia Riasat
- **Bigger Is Not Better Under Differential Privacy: Optimization Failure at Eleven-Billion Scale in Vision–Language Model Fine-Tuning** — TZU-EN SU ⋅ Li-Hong Guo ⋅ Yangmi Su ⋅ Cheng-Yen Li
- **Challenges in Inference-Time Scaling with Uncertainty-Aware Tree Search** — Jacopo Minniti ⋅ Neil Band ⋅ Tim G. J. Rudner
- **Does Math Reasoning Improve General LLM Capabilities? Understanding Transferability of LLM Reasoning** — Maggie Huan ⋅ Yuetai Li ⋅ Tianyu Zheng ⋅ Xiaoyu Xu ⋅ Seungone Kim ⋅ Minxin Du ⋅ Radha Poovendran ⋅ Graham Neubig ⋅ Xiang Yue
- **When Lie Detectors Learn Model Identity: Confounds in Black-Box Sandbagging Detection** — Lin Yulong ⋅ Pablo Bernabeu-Perez ⋅ Benjamin Arnav ⋅ Lennie Wells ⋅ Mary Phuong
- **The Low-Frequency Trap: Why Scaling Doesn't Solve Simple Temporal Counting** — Sarvesh Baskar ⋅ Muhammad Islam ⋅ Zikui Cai ⋅ Ankit Nakhawa ⋅ Anirudh Satheesh ⋅ Tom Goldstein ⋅ Furong Huang
- **Spatial Reasoning is Not a Free Lunch: A Controlled Study on LLaVA** — Nahid Alam ⋅ Leema Murali ⋅ Siddhant Bharadwaj ⋅ Patrick Liu ⋅ Timothy Chung ⋅ Drishti Sharma ⋅ Akshata ⋅ Kranthi Kiran GV ⋅ Wesley Tam ⋅ Bala Vegesna
- **I Can't Believe It Can't Count: Vision-Language Models Fail at Basic Enumeration Beyond the Subitizing Range** — Amirhossein Afsharrad ⋅ Seyed Mousavi ⋅ Sanjay Lall
- **Random Is Hard to Beat: Active Selection in Online DPO with Modern LLMs** — Giyeong Oh ⋅ Junghyun Lee ⋅ Jaehyun Park ⋅ Youngjae Yu ⋅ Wonho Bae ⋅ Junhyug Noh
- **Not All Time Is Gregorian: Evaluating LLMs on Cultural Calendar Systems** — Deepon Halder ⋅ Adish Pandya ⋅ Raj Dabre
- **More Than a Quick Glance: Overcoming the Greedy Bias in KV-Cache Compression** — Aryan Sood ⋅ Tanvi Sharma ⋅ Vansh Agrawal
- **The Missing Red Line: How Commercial Pressure Erodes AI Safety Boundaries** — Nora Petrova ⋅ John Burden
- **Evaluating Ill-Defined Tasks in Large Language Models** — Yi Zhou ⋅ Basel Shbita
- **Is Evaluation Awareness Just Format Sensitivity? Limitations of Probe-Based Evidence under Controlled Prompt Structure** — Viliana Devbunova
- **Learning State-Tracking from Code: REPL Traces and Probabilistic Automata** — Julien Siems ⋅ Riccardo Grazzi ⋅ Kirill Kalinin ⋅ Hitesh Ballani ⋅ Babak Rahmani
- **AI-rithmetic** — Alex Bie ⋅ Travis Dick ⋅ Alex Kulesza ⋅ Prabhakar Raghavan ⋅ Vinod Raman ⋅ Sergei Vassilvitskii
- **Retrieval or Representation? Reassessing Benchmark Gaps in Multilingual and Visually Rich RAG** — Martin Asenov ⋅ Kenza Benkirane ⋅ Daniel Goldwater ⋅ Aneiss Ghodsi
- **A Pilot Study on Doubt Robustness of LLMs in Clinical Prediction Explanation** — Juhwan Choi ⋅ Sangchul Hahn ⋅ Eunho Yang
- **The $\Psi$ Paradox in Extreme Superposition: When ETF Alignment Does Not Predict Language Model Generalization** — Hyunjun Kim
- **Can Multi-Modal LLMs Provide Live Step-by-Step Task Guidance?** — Apratim Bhattacharyya ⋅ Bicheng Xu ⋅ Sanjay Haresh ⋅ Reza Pourreza ⋅ Litian Liu ⋅ Sunny Panchal ⋅ Pulkit Madan ⋅ Leonid Sigal ⋅ Roland Memisevic
- **Improving Proxy Transfer via Intermediate Proxy Tuning** — Kevin Kuo ⋅ Ayush Sehgal ⋅ Robert Pare ⋅ Virginia Smith
- **Beyond Continuity: Challenges of Context Switching in Multi-Turn Dialogue with LLMs** — Aditya Sinha ⋅ Harald Steck ⋅ Vito Ostuni ⋅ Matteo Rinaldi
- **Synthetic Error Injection Fails to Elicit Self-Correction In Language Models** — David Wu ⋅ Shreyas Kapur ⋅ Anant Sahai ⋅ Stuart Russell
- **Style over Substance: LLM-as-a-Judge Fails to Evaluate Multi-Party Social Dialogue** — Kunal Samanta ⋅ Faisal Tareque Shohan ⋅ Amine Trabelsi ⋅ Richard Khoury
- **Knowing Is Not Seeing. Limits of Physical Problem Solving in VLMs** — Karim Elmaaroufi ⋅ Kevin Chon ⋅ Justin Svegliato ⋅ Lakshya A Agrawal ⋅ Matei Zaharia ⋅ Sanjit Seshia
- **The Cost of Consistency: Why Cross-Plane Contrastive Learning Fails to Bridge the Gap Between MedSAM-3 and nnU-Net** — Madhu Shree Aravindan ⋅ Aaditi Bajpai ⋅ Ramamoorthy Sriramulu
- **I Can't Believe It's Not Robust: Catastrophic Collapse of Safety Classifiers under Embedding Drift** — Subramanyam Sahoo ⋅ Vinija Jain ⋅ Divya Chaudhary ⋅ Aman Chadha
- **One Step Forward, Two Steps Back: Regression Errors and Cost Inefficiencies in LLM Iterative Refinement for Code Generation** — Lucas T Borges ⋅ RICARDO RIOS
- **Probing and Steering Chain-of-Thought Unfaithfulness in Language Models** — Giovanni Occhipinti ⋅ Alessandro Abate ⋅ Nandi Schoots
- **Query Timing Produces Opposite Positional Biases Between LLMs and Humans** — Jasin Cekinmez ⋅ Addison J. Wu ⋅ Thomas L. Griffiths
- **Beyond Suffixes: Token Position in GCG Adversarial Attacks on Large Language Models** — Hicham Eddoubi ⋅ Umar Abdullahi ⋅ Fadi Hassan
- **NON-MONOTONICITY AND CATASTROPHIC RISK OF PROMPT INTERVENTIONS IN ADVERSARIAL LLM CONTROL** — Koki Inoue ⋅ Naoya Takashima ⋅ Hayato Fujihara ⋅ SHUYA HIGUCHI ⋅ Kota Shimomura ⋅ Ryuta Shimogauchi ⋅ Takayoshi Yamashita
- **FLUFFINJECTOR: DIAGNOSING LOGICAL CONSISTENCY FAILURES IN CHAIN-OF-THOUGHT REWARD MODELS** — Varshith Vijjapu ⋅ Krishiv Ray ⋅ Vaidheeswaran Archana
- **Don't Retrieve, Generate: Prompting LLMs for Synthetic Training Data in Dense Retrieval** — Aarush Sinha
- **The Limits of Long-Context Reasoning in Automated Bug Fixing** — Ravi Raju ⋅ Mengmeng Ji ⋅ Shubhangi Upasani ⋅ Bo Li ⋅ Urmish Thakker
- **Barriers to Pareto Steerability in Preference-Conditioned LLM Alignment** — Fatemeh Nourzad ⋅ Daouda Sow ⋅ Yingbin Liang ⋅ Ming Shi ⋅ Ming Zhang ⋅ Yunxuan Li ⋅ Eylem Ekici ⋅ Ness Shroff
- **QuanBench Plus: A Unified Multi-Framework Benchmark for LLM-Based Quantum Code Generation** — Ali Slim ⋅ Haydar Hamieh ⋅ Jawad Kotaich ⋅ Yehya Ghosn ⋅ Chehimi ⋅ Hasan Hammoud ⋅ Ammar Mohanna ⋅ Bernard Ghanem
- **EoRA: Fine-tuning-free Compensation for Compressed LLM with Eigenspace Low-Rank Approximation** — Shih-Yang Liu ⋅ Maksim Khadkevich ⋅ Nai Chit FUNG ⋅ Charbel Sakr ⋅ Chao-Han Huck Yang ⋅ Chien-Yi Wang ⋅ Saurav Muralidharan ⋅ Hongxu (Danny) Yin ⋅ Kwang-Ting Cheng ⋅ Jan Kautz ⋅ Yu-Chiang Frank Wang ⋅ Pavlo Molchanov ⋅ Min-Hung Chen
- **Why Large Language Models Fail for Hausa Educational Content: Cascading Errors from Translation to Speech to Comprehension** — Honour-Jesus Bezaleel ⋅ Pearse Jim ⋅ Moses Daudu
- **The Continuous Space Gap: Why VLMs Fail in Continuous Geometric Reasoning** — Yikun Zong ⋅ Cheston Tan
- **I Can't Believe LLMs Still Can't Write Drama: Multi-Dimensional Failures in Script Continuation** — Shijian Ma ⋅ Yunqi Huang ⋅ Lin Yan
- **EsoLang-Bench: Evaluating Genuine Reasoning in Large Language Models via Esoteric Programming Languages** — Aman Sharma ⋅ Paras Chopra
- **Limits of Difficulty Scaling: Hard Samples Yield Diminishing Returns in GRPO-Tuned SLMs** — Suraj Yadav ⋅ Siddharth Yadav ⋅ Parth Goyal
- **When can you TRUST Large Language Models?** — Radu Paradovschi ⋅ Darvin Yi ⋅ Andrew Rabinovich ⋅ Zhao Chen
- **The Selective Safety Trap: How LLMs Scaling and Alignment Fail to Generalize Across Minority Demographics** — Iago Brito ⋅ Walcy Rios ⋅ Julia Dollis ⋅ Diogo Costa Silva ⋅ Arlindo Galvão Filho
- **When Rubrics Backfire: Systematic Preference Drift in LLM Judges** — Ruomeng Ding ⋅ Yifei Pang ⋅ He Sun ⋅ Yizhong Wang ⋅ Steven Wu ⋅ Zhun Deng
- **The Anatomy of Uncertainty in LLMs** — Aditya Taparia ⋅ Ransalu Senanayake ⋅ Kowshik Thopalli ⋅ Vivek Narayanaswamy

# Organizers

- Arno Blaas
- Priya DCosta
- Fan Feng
- Zhaoying Pan
- Nikolai Rozanov
- Jennifer Williams
- Yubin Xie
- Rui Yang
