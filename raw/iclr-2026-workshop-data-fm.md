---
title: "Workshop: Navigating and Addressing Data Problems For Foundation Models (DATA-FM)"
url: "https://iclr.cc/virtual/2026/workshop/10000798"
source: "other"
author: "ICLR 2026"
date: "2026-04-27"
captured: "2026-05-13"
tags:
  - iclr-2026
  - workshop
  - data-quality
  - foundation-models
aliases:
  - "ICLR 2026 DATA-FM Workshop"
related:
  - "wiki/articles/data-fm-workshop.md"
---

## Workshop description

The past year has witnessed remarkable advances in foundation models (FMs): new post-training paradigms such as reinforcement learning with verifiable rewards (RLVR) that strengthen reasoning, increasingly multimodal and agentic systems, and renewed attention to benchmark design and evaluation. Each of these advances depends on distinct data innovations: verifiable reward signals and reasoning traces for RLVR; aligned cross-modal corpora and interaction logs for multimodality and agency; and leak-resistant, representative test sets for evaluation. Taken together, these dependencies underscore the continuing centrality of data as a design variable at the forefront of FM research. Meanwhile, longstanding challenges in data collection, curation, and synthesis remain unresolved, while concerns surrounding copyright, privacy, and fairness have only intensified. Building on the success of the first two DATA-FM workshops at ICLR 2024 and 2025, the third edition will revisit these persistent issues while highlighting emerging ones at the frontiers of post-training, multimodality, and evaluation. By convening researchers and practitioners across diverse research communities, DATA-FM seeks to advance understanding of data’s evolving role in FMs and foster innovative solutions shaping the next generation of models and applications.

## Date and time

- Page display in captured HTML: Sun, Apr 26, 2026 • 9:00 AM – 5:00 PM -03
- Timezone setting on page: America/Sao_Paulo
- SlidesLive presentation IDs: 39063677

## Schedule table

| Time | Event | Notes |
| --- | --- | --- |
| 9:00 AM | Opening Remarks |  |
| 9:10 AM | Invited Talk (Baharan Mirzasoleiman) | Abstract not included in captured HTML. |
| 9:40 AM | Invited Talk (Sewon Min) | Abstract not included in captured HTML. |
| 10:30 AM | Oral Presentation 1 (Mayee Chen) | Data mixing---determining the ratios of data from different domains---is a first-order concern for training la… |
| 10:45 AM | Oral Presentation 2 (Narmeen Fatimah Oozeer) | Existing benchmarks typically report accuracy for a single model on a single run. This systematically understa… |
| 11:00 AM | Oral Presentation 3 (Kunal Talwar) | Large language models (LLMs) can struggle to memorize factual knowledge in their parameters, often leading to… |
| 11:15 AM | Poster Session I | Poster papers are listed separately below. |
| 1:00 PM | Invited Talk (Juan Carlos Niebles) | Abstract not included in captured HTML. |
| 2:00 PM | Oral Presentation 4 (Jacqueline He) | Modern language models (LMs) tend to memorize portions of their training data and reproduce verbatim spans. Wh… |
| 2:15 PM | Oral Presentation 5 (Arshia Afzal) | Vision-Language Models (VLMs) are typically trained on a diverse set of multi-modal domains, yet current pract… |
| 2:30 PM | Oral Presentation 6 (Maximilian Idahl) | Since FineWeb-Edu, data curation for LLM pretraining has predominantly relied on single scalar quality scores… |
| 3:20 PM | Invited Talk: The Art & Science of Benchmarking Agents (Fred Sala) | Our ability to measure AI has been outpaced by our ability to develop it, and this eval gap is one of the most… |
| 3:50 PM | Sponsor Talk (Snorkel AI) |  |
| 4:05 PM | Closing Remarks |  |
| 4:10 PM | Poster Session II | Poster papers are listed separately below. |

## Invited talks

### Baharan Mirzasoleiman

- Time: 9:10 AM
- Title: Invited Talk
- Abstract: Not included in the captured HTML.

### Sewon Min

- Time: 9:40 AM
- Title: Invited Talk
- Abstract: Not included in the captured HTML.

### Juan Carlos Niebles

- Time: 1:00 PM
- Title: Invited Talk
- Abstract: Not included in the captured HTML.

### Fred Sala

- Time: 3:20 PM
- Title: The Art & Science of Benchmarking Agents
- Abstract: Our ability to measure AI has been outpaced by our ability to develop it, and this eval gap is one of the most important problems in AI. We need more enduring benchmarks to close this gap, and consequently advance entire new vectors of capabilities for the field. In this talk, I'll share our insights into evaluating agents, drawing from experience working with nearly all frontier labs and many of our academic collaborators. We'll discuss the science (i.e., mechanics that make benchmarks rigorous and effective) and art (i.e., intangibles driving ambitious and enduring benchmarks) of building great benchmarks. I'll close by sharing some of the learnings from Open Benchmarks Grants— a $3M initiative in partnership with Hugging Face, Together AI, Prime Intellect, Factory, and others— and highlighting some of the projects we're most excited about funding.

## Contributed talks

### Olmix: A Framework for Data Mixing Throughout LM Development

- Time: 10:30 AM
- Presenter: Mayee Chen
- Authors: Mayee Chen ⋅ Tyler Murray ⋅ David Heineman ⋅ Matt Jordan ⋅ Hanna Hajishirzi ⋅ Christopher Re ⋅ Luca Soldaini ⋅ Kyle Lo
- Abstract: Data mixing---determining the ratios of data from different domains---is a first-order concern for training language models (LMs), but existing mixing methods have poorly understood design choices and assume that the set of domains remain fixed throughout development. We present Olmix, a framework that addresses two challenges encountered during LM development. First, the configuration space for developing a mixing method is not well understood---design choices across existing methods lack justification or consensus and overlook practical issues like data constraints. We conduct a comprehensive empirical study of this space, identifying which design choices lead to a strong mixing method. Second, the domain set evolves throughout LM development as datasets are revised and expanded---a problem setting largely unaddressed by existing works. We study how to efficiently recompute the mixture after the domain set is updated, given an existing mix from before the update. We introduce mixture reuse, a mechanism that reuses existing relative ratios and recomputes ratios only for domains affected by an update. Over a sequence of five domain-set updates mirroring real-world LM development, mixture reuse matches the performance of fully recomputing the mix after each update with 74% less compute and improves over training without mixing by 11.6% on downstream tasks.
Link
- OpenReview: https://openreview.net/forum?id=Z46ZBACu1p

### The Capability Frontier: Benchmarks Miss 82% of Model Performance

- Time: 10:45 AM
- Presenter: Narmeen Fatimah Oozeer
- Authors: Bradley Fowler ⋅ Ryan Smith ⋅ Daniel Graviet ⋅ William Myers ⋅ Joshua Greaves ⋅ Narmeen Oozeer ⋅ Antía García ⋅ Philip Quirke ⋅ Fazl Barez ⋅ Amir Abdullah ⋅ Shriyash Upadhyay
- Abstract: Existing benchmarks typically report accuracy for a single model on a single run. This systematically understates real-world LLM capabilities, particularly under heterogeneous data distributions: (i) different models get different questions correct according to their specializations, and (ii) given a budget, multiple generations can be sampled and selectively retained. To quantify this gap, we introduce the Capability Frontier: a Pareto frontier over a set of models that characterizes the best achievable performance at each cost level under optimal selection across models and generations (i.e., via an oracle). Our construction corrects for two opposing biases: underestimation from single-model evaluation and overestimation from taking maxima over noisy samples. We study 21 LLMs across 16 widely used benchmarks spanning coding, reasoning, medicine, factuality, instruction following, and agentic tasks, comparing Capability Frontier performance at matched cost to each benchmark’s top-performing model. Correcting for single-model evaluation yields a 54% error rate reduction; additionally correcting for single runs yields an 82% improvement, with SOTA accuracy matched at 85% cost reduction. Complementing these empirical results, we use controlled probabilistic simulations to show that higher query topic entropy produces a near-monotonic increase in the performance gap between oracle routing and the best single model. Our findings suggest collective LLM capabilities are substantially underestimated, with implications for evaluation and deployment in data-heterogeneous, multi-domain settings.
Link
- OpenReview: https://openreview.net/forum?id=iV1TS1z1up

### Cram Less to Fit More: Training Data Pruning Improves Memorization of Facts

- Time: 11:00 AM
- Presenter: Kunal Talwar
- Authors: Jiayuan Ye ⋅ Vitaly Feldman ⋅ Kunal Talwar
- Abstract: Large language models (LLMs) can struggle to memorize factual knowledge in their parameters, often leading to hallucinations and poor performance on knowledge-intensive tasks. In this paper, we formalize fact memorization from an information-theoretic perspective and study how training data distributions affect fact accuracy. We show that fact accuracy is suboptimal (below the capacity limit) whenever the amount of information contained in the training data facts exceeds model capacity. This is further exacerbated when the fact frequency distribution is skewed (e.g. a power law). We propose data selection schemes based on the training loss alone that aim to limit the number of facts in the training data and flatten their frequency distribution. On semi-synthetic datasets containing high-entropy facts, our selection method effectively boosts fact accuracy to the capacity limit. When pretraining language models from scratch on an annotated Wikipedia corpus, our selection method enables a GPT2-Small model (110m parameters) to memorize 1.3X more entity facts compared to standard training, matching the performance of a 10X larger model (1.3B parameters) pretrained on the full dataset.
Link
- OpenReview: https://openreview.net/forum?id=P0fB2DZlcL

### Anchored Decoding: Provably Reducing Copyright Risk for Any Language Model

- Time: 2:00 PM
- Presenter: Jacqueline He
- Authors: Jacqueline He ⋅ Jonathan Hayase ⋅ Scott Yih ⋅ Sewoong Oh ⋅ Luke Zettlemoyer ⋅ Pang Wei Koh
- Abstract: Modern language models (LMs) tend to memorize portions of their training data and reproduce verbatim spans. When the underlying sources are sensitive or copyright-protected, such reproduction raises issues of consent and compensation for creators and compliance risks for developers. We propose ANCHORED DECODING, a plug-and-play inference-time method for suppressing verbatim reproduction: it enables decoding from any risky LM trained on mixed-license data by keeping generation in bounded proximity to a permissively trained safe LM. ANCHORED DECODING does so by adaptively allocating a user-chosen information budget over the generation trajectory and enforcing per-step constraints that yield a sequence-level guarantee, enabling a tunable risk–utility trade-off. To make ANCHORED DECODING practically useful, we introduce a new permissively trained safe model (TinyComma 1.8B), as well as ANCHORED Byte DECODING, a bytelevel variant of our method that enables cross-vocabulary fusion via the ByteSampler framework (Hayase et al., 2025). We evaluate our methods across six model pairs on long-form evaluations of copyright risk and utility. ANCHORED and ANCHORED Byte DECODING define a new Pareto frontier, preserving near-original fluency and factuality while eliminating up to 75% of the measurable copying gap (averaged over six copying metrics) between the risky baseline and a safe reference, at a modest inference overhead.
Link
- OpenReview: https://openreview.net/forum?id=63Is26x1qu

### Multi-Modal Data Mixtures via Latent Space Coupling for Vision-Language Model Training

- Time: 2:15 PM
- Presenter: Arshia Afzal
- Authors: Wanyun Xie ⋅ Francesco Tonin ⋅ Volkan Cevher
- Abstract: Vision-Language Models (VLMs) are typically trained on a diverse set of multi-modal domains, yet current practices rely on costly manual tuning. We propose MaD-Mix, a principled and computationally efficient framework that derives multi-modal data mixtures for VLM training. MaD-Mix formulates data mixing as modality-aware domain alignment maximization and obtains closed-form multi-modal alignment scores from the Fenchel dual through inter-modal coupling variables. MaD-Mix systematically handles domains with missing modalities, allowing for the integration of language-only domains. Empirical evaluations across 0.5B and 7B models demonstrate that MaD-Mix accelerates VLM training across diverse benchmarks. MaD-Mix matches human-tuned data mixtures using 22% fewer training steps in image-text instruction tuning. In complex tri-modal video-image-text scenarios, where manual tuning becomes impractical, MaD-Mix boosts average accuracy over uniform weights, with negligible mixture computation overhead (<1 GPU-hour), enabling scalable mixture design for modern VLM pipelines.
Link
- OpenReview: https://openreview.net/forum?id=pAbTdXyaLm

### propella-1: Multi-Property Document Annotation for LLM Data Curation at Scale

- Time: 2:30 PM
- Presenter: Maximilian Idahl
- Authors: Maximilian Idahl ⋅ Benedikt Droste ⋅ Björn Plüster ⋅ Jan Harries
- Abstract: Since FineWeb-Edu, data curation for LLM pretraining has predominantly relied on single scalar quality scores produced by small classifiers. A single score conflates multiple quality dimensions, prevents flexible filtering, and offers no interpretability. We introduce propella-1, a family of small multilingual LLMs (0.6B, 1.7B, 4B parameters) that annotate text documents across 18 properties organized into six categories: core content, classification, quality and value, audience and purpose, safety and compliance, and geographic relevance. The models support 57 languages and produce structured JSON annotations conforming to a predefined schema. Evaluated against a frontier commercial LLM as a reference annotator, the 4B model achieves higher agreement than much larger general-purpose models. We release propella-annotations, a dataset of over three billion document annotations covering major pretraining corpora including data from FineWeb-2, FinePDFs, HPLT 3.0, and Nemotron-CC. Using these annotations, we present a multi-dimensional compositional analysis of widely used pretraining datasets, revealing substantial differences in quality, reasoning depth, and content composition that single-score approaches cannot capture. All model weights and annotations are released under permissive, commercial-use licenses.
Link
- OpenReview: https://openreview.net/forum?id=17tLF0kWFH

## Poster papers list

The captured HTML lists 118 additional paper entries beyond the six oral presentations. They are reproduced below as poster papers:

- **Rethinking Data Curation in LLM Training: Online Reweighting Offers Better Generalization than Offline Methods** — Wanru Zhao ⋅ Yihong Chen ⋅ Yuzhi Tang ⋅ Wentao Ma ⋅ Shengchao Hu ⋅ Xu Hu ⋅ Alex Iacob ⋅ Abhinav Mehrotra ⋅ Nic Lane
- **Resource-Adaptive Federated Text Generation with Differential Privacy** — Jiayi Wang ⋅ John Gounley ⋅ Heidi Hanson
- **ESDAE: Evaluating Synthetic Data for Agent Evaluation** — Shuaiqi Wang ⋅ Aadyaa Maddi ⋅ Zinan Lin ⋅ Giulia Fanti
- **Geometry-Preserving Coresets for Quantized Foundation Models in Remote Sensing** — Tushar Shinde
- **MixtureVitae: Open Web-Scale Pretraining Dataset With High Quality Instruction and Reasoning Data Built from Permissive-First Text Sources** — Huu Nguyen ⋅ Victor May ⋅ Harsh Raj ⋅ Marianna Nezhurina ⋅ Yishan Wang ⋅ Yanqi Luo ⋅ Minh Chien Vu ⋅ Taishi Nakamura ⋅ Ken Tsui ⋅ Van Nguyen ⋅ David Salinas ⋅ Aleksandra Krasnodębska ⋅ Christoph Schuhmann ⋅ Mats L. Richter ⋅ Xuan-Son Vu ⋅ Jenia Jitsev
- **AgenticMath: Enhancing LLM Reasoning via Agentic-based Math Data Generation** — Xianyang Liu ⋅ Yilin LIU ⋅ Shuai Wang ⋅ Hao Cheng ⋅ Andrew Estornell ⋅ Yuzhi Zhao ⋅ Jun Shu ⋅ Jiaheng Wei
- **EnterpriseOps-Gym: Environments and Evaluations for Stateful Agentic Planning and Tool Use in Enterprise Settings** — Shiva Malay ⋅ Shravan Nayak ⋅ Aman Tiwari ⋅ Jishnu Nair ⋅ Sathwik Tejaswi Madhusudhan ⋅ Sagar Davasam ⋅ Srinivas Sunkara ⋅ Sai Rajeswar Mudumba
- **Induction Signatures Are Not Enough: A Matched-Compute Study of Load-Bearing Structure in In-Context Learning** — Mohammed Sabry ⋅ Anya Belz
- **AdaProb: Efficient Machine Unlearning via Adaptive Probability** — Zihao Zhao ⋅ Yuchen Yang ⋅ Anjalie Field ⋅ Yinzhi Cao
- **Privileged Information Distillation for Language Models** — Emiliano Penaloza ⋅ Dheeraj Vattikonda ⋅ Nicolas Gontier ⋅ Alexandre Lacoste ⋅ Laurent Charlin ⋅ Massimo Caccia
- **Non-Local Data Attribution for On-policy Reinforcement Learning** — Shixuan Liu ⋅ Yuzheng Hu ⋅ Han Zhao ⋅ Jiaqi Ma
- **[Short] RIFT: A RubrIc Failure Mode Taxonomy and Automated Diagnostics** — Zhengyang Qi ⋅ Charles Dickens ⋅ Derek Pham ⋅ Amanda Dsouza ⋅ Armin Parchami ⋅ Frederic Sala ⋅ Paroma Varma
- **Query-based Model Collaboration Enables Expert-level Clinical Text Augmentation** — Dongkyu Cho ⋅ Miao Zhang ⋅ Gregory D. Lyng ⋅ Rumi Chunara
- **Structured Captions Improve Prompt Adherence in Text-to-Image Models (Re-LAION-Caption 19M)** — Nicholas Merchant ⋅ Haitz Sáez de Ocáriz Borde ⋅ Andrei Popescu ⋅ Carlos Garcia Jurado Suarez
- **Rethinking Data Selection: The Importance of Coverage over Difficulty in Generative Fine-Tuning** — Lalchand Pandia ⋅ Kanishka Misra ⋅ Allyson Ettinger
- **GraphPFN: A Prior-Data Fitted Graph Foundation Model** — Dmitry Eremeev ⋅ Oleg Platonov ⋅ Gleb Bazhenov ⋅ Artem Babenko ⋅ Liudmila Prokhorenkova
- **Overcoming the Scarcity of Verifiable Reasoning Data with Decision Pivots** — Dongkyu Cho ⋅ Amy Zhang ⋅ Bilel Fehri ⋅ Sheng Wang ⋅ Rumi Chunara ⋅ Hengrui Cai ⋅ Rui Song
- **Escaping Model Collapse via Synthetic Data Verification: Near-term Improvements and Long-term Convergence** — Bingji Yi ⋅ Qiyuan Liu ⋅ Yuwei Cheng ⋅ Haifeng Xu
- **Task Scarcity and Label Leakage in Relational Transfer Learning** — Francisco Galuppo Azevedo ⋅ Clarissa Loures ⋅ Denis Oliveira
- **Inference-Time Distillation: Cost-Efficient Agents Without Fine-Tuning or Manual Prompt Engineering** — Vishnu Sarukkai ⋅ Asanshay Gupta ⋅ James Hong ⋅ Michaël Gharbi ⋅ Kayvon Fatahalian
- **Unified Evaluation of Table Embedding Methods Across Multiple Benchmark Scenarios** — Ali Younes ⋅ Saeed Ghoorchian ⋅ Maximilian Schambach ⋅ Johannes Höhne
- **[Short]ACTIVE L EARNING FOR S CALABLE DATA S ELECTION IN I NSTRUCTION T UNING** — Lalchand Pandia
- **RelBench v2: A Large-Scale Benchmark and Relational Data Repository** — Justin Gu ⋅ Rishabh Ranjan ⋅ Charilaos Kanatsoulis ⋅ Haiming Tang ⋅ Martin Jurkovic ⋅ Valter Hudovernik ⋅ Mark Znidar ⋅ Pranshu Chaturvedi ⋅ Parth Shroff ⋅ Fengyu Li ⋅ Jure Leskovec
- **[Short] Exploration into gradient-based coreset methods for targeted subset selection** — Evelyn Zhu ⋅ Neha Hulkund ⋅ Sara Beery
- **DISCO: Diversifying Sample Condensation for Efficient Model Evaluation** — Alexander Rubinstein ⋅ Benjamin Raible ⋅ Martin Gubri ⋅ Seong Joon Oh
- **Optimal Splitting of Language Models from Mixtures to Specialized Domains** — Skyler Seto ⋅ Pierre Ablin ⋅ Anastasiia Filippova ⋅ Jiayuan Ye ⋅ Louis Béthune ⋅ Angelos Katharopoulos ⋅ David Grangier
- **Train Smarter, Not Longer: Memorization-Guided Data Reuse for Efficient LLM Training** — Jingwei Zuo ⋅ Ilyas Chahed ⋅ Maksim Velikanov ⋅ Cong Zeng ⋅ Dhia Rhaiem ⋅ Pasquale Balsebre ⋅ Abhay Kumar ⋅ Younes Belkada ⋅ Hakim Hacid
- **SpreadsheetArena: Decomposing Preference in LLM Generation of Spreadsheet Workbooks** — Srivatsa Kundurthy ⋅ Clara Na ⋅ Michael Handley ⋅ Zach Kirshner ⋅ Chen Bo Calvin Zhang ⋅ Manasi Sharma ⋅ Emma Strubell ⋅ John Ling
- **When do Score-Based Data Valuation Methods Work, and Why?** — Kumar Kshitij Patel ⋅ Sai Karimireddy ⋅ Raul Fernandez ⋅ Manolis Zampetakis
- **Learning from Synthetic Data Improves Multi-hop Reasoning** — Anmol Kabra ⋅ Yilun Yin ⋅ Albert Gong ⋅ Kamilė Stankevičiūtė ⋅ Dongyoung Go ⋅ Johann Lee ⋅ Katie Luo ⋅ Carla Gomes ⋅ Kilian Weinberger
- **PluRel: Synthetic Data unlocks Scaling Laws for Relational Foundation Models** — Vignesh Kothapalli ⋅ Rishabh Ranjan ⋅ Valter Hudovernik ⋅ Vijay Prakash Dwivedi ⋅ Johannes Hoffart ⋅ Carlos Guestrin ⋅ Jure Leskovec
- **Measuring Dataset Diversity from a Geometric Perspective** — Yang Ba ⋅ Mohammad Abolhasani ⋅ Michelle Mancenido ⋅ Rong Pan
- **Visual Compositional Tuning** — Xindi Wu ⋅ Hee Seung Hwang ⋅ Polina Kirichenko ⋅ Esin Tureci ⋅ Olga Russakovsky
- **OR-LLM-Bench: A Pipeline for Scalable and Verifiable Text-to-Optimization Synthesis** — Zhiqi Gao ⋅ Albert Ge ⋅ Alexander Berenbeim ⋅ Nathaniel Bastian ⋅ Frederic Sala
- **TutorBench: A Benchmark To Assess Tutoring Capabilities Of Large Language Models** — Rakshith Sharma Srinivasa ⋅ Zora Che ⋅ Chen Bo Calvin Zhang ⋅ Diego Buendia ⋅ Ernesto Montoya ⋅ Jayeon Park ⋅ Dean Lee ⋅ Guillermo Mangialardi ⋅ Charmaine Ng ⋅ Ed-Yeremai Hernandez-Cardona ⋅ Anisha Gunjal ⋅ Yunzhong He ⋅ Bing Liu ⋅ Chen Xing
- **Are Easier or Harder Examples Better? Rethinking Data Selection for Reward Models and Preference Optimization** — Kevin Christian Wibisono ⋅ Aya Ismail ⋅ Pedro O Pinheiro ⋅ Yixin Wang ⋅ Kyunghyun Cho ⋅ Natasa Tagasovska ⋅ Rajesh Ranganath
- **Rescaled Influence Functions: Accurate Data Attribution in High Dimension** — Ittai Rubinstein ⋅ Samuel Hopkins
- **[Short] Towards Large-Scale Heterogeneous Data Organization for Scientific Foundation Models: A Nuclear Fusion Case Study** — Nathaniel Chen ⋅ Kouroche Bouchiat ⋅ ⋅ Azarakhsh Jalalvand ⋅ ⋅ Egemen Kolemen
- **SynQuE: Estimating Synthetic Dataset Quality Without Annotations** — Arthur Chen ⋅ Victor Zhong
- **Toward Evaluating Model Collapse in LLMs: Insights from Continual Pretraining** — Kristian Minchev ⋅ Anton Alexandrov ⋅ Martin Vechev ⋅ Nikola Konstantinov
- **Adversarial Arena: Crowdsourcing Data Generation through Interactive Competition** — Prasoon Goyal ⋅ Sattvik Sahai ⋅ Michael Johnston ⋅ Hangjie Shi ⋅ Yao Lu ⋅ Shaohua liu ⋅ Anna Rumshisky ⋅ Rahul Gupta ⋅ Anna Gottardi ⋅ Desheng Zhang ⋅ Lavina Vaz ⋅ Leslie Ball ⋅ Lucy Hu ⋅ Luke Dai ⋅ Samyuth Sagi ⋅ Maureen Murray ⋅ Sankaranarayanan Ananthakrishnan
- **A Unified Theory of Random Projection for Influence Functions** — Pingbang Hu ⋅ Yuzheng Hu ⋅ Jiaqi Ma ⋅ Han Zhao
- **MobileKernelBench: Can LLMs Write Efficient Kernels for Mobile Devices?** — Xingze Zou ⋅ Jing Wang ⋅ Yuhua Zheng ⋅ Xueyi Chen ⋅ Haolei Bai ⋅ Lingcheng Kong ⋅ Syed Abu-Bakar ⋅ Zhaode Wang ⋅ chengfei lv ⋅ Haoji Hu ⋅ Huan Wang
- **Federated Agent Reinforcement Learning** — Canyu Chen ⋅ Kangyu Zhu ⋅ Zhaorun Chen ⋅ Zhanhui Zhou ⋅ Shizhe Diao ⋅ Yiping Lu ⋅ Tian Li ⋅ Manling Li ⋅ Dawn Song
- **[SHORT] Less is More: On Data Redundancy in VLA Training** — Kevin Yang ⋅ Tony Yang
- **Toward Cross-Lingual Quality Classifiers for Multilingual Pretraining Data Selection** — Yassine Turki ⋅ Vinko Sabolčec ⋅ Bettina Messmer ⋅ Martin Jaggi
- **[Short] Few-Shot Cross-Table Data Mixture in Tabular In-Context Learning: Benefits, Failure Modes, and Alignment** — Jia-Wei Liao ⋅ Kuan-Yu Chen ⋅ Yu-Chen Den ⋅ Tien-Hao Chang
- **Configuration-to-Performance Scaling Law with Neural Ansatz** — Huaqing Zhang ⋅ Kaiyue Wen ⋅ Tengyu Ma
- **jina-vlm: Small Multilingual Vision Language Model** — Andreas Koukounas ⋅ Georgios Mastrapas ⋅ Florian Hönicke ⋅ Sedigheh Eslami ⋅ ⋅ Scott Martens ⋅ Han Xiao
- **Less is More: Adaptive Coverage Sampling for Synthetic Training Data** — Sasan Tavakkol ⋅ Max Springer ⋅ MohammadHossein Bateni ⋅ Vincent Cohen-Addad ⋅ Neslihan Bulut ⋅ MohammadTaghi Hajiaghayi
- **Open LLM Projects Should Allocate More Compute for Data Than Training** — Maximilian Idahl
- **[Short] Beyond Data Size: Exploring the Impact of Dataset Diversity and Density in Self-Distillation Learning** — Alvard Barseghyan ⋅ Ani Vanyan ⋅ Hakob Tamazyan ⋅ Hrant Khachatrian
- **LEGALMIDM: Use-Case-Driven Legal Domain Specialization for Korean Large Language Model** — Youngjoon Jang ⋅ Chanhee Park ⋅ Hyeonseok Moon ⋅ Young-kyoung Ham ⋅ jiwon moon ⋅ Jinhyeon Kim ⋅ JuKyung Jung ⋅ Heuiseok Lim
- **Mix Early, Forget Less: Data Mixing During Pretraining Builds Resistance to Forgetting** — Lawrence Feng ⋅ Gaurav Ghosal ⋅ Jacob Springer ⋅ Ziqian Zhong ⋅ Aditi Raghunathan
- **Motion Capture is Not the Target Domain: Scaling Synthetic Data for Learning Motion Representations** — Firas Darwish ⋅ George Nicholson ⋅ Aiden Doherty ⋅ Hang Yuan
- **[Short] DSL-Monkeys: Self-Generated In-Context Examples for Low-Resource GPU DSL Kernels** — Nathan Paek ⋅ Simon Guo ⋅ Vishnu Sarukkai ⋅ Willy Chan ⋅ William Hu ⋅ Ethan Boneh ⋅ Simran Arora ⋅ Ludwig Schmidt ⋅ Kayvon Fatahalian ⋅ Azalia Mirhoseini
- **ROSER: Few-Shot Robotic Sequence Retrieval for Scalable Robot Learning** — Zillur Rahman ⋅ Eddison Pham ⋅ Alejandro Daniel Noel ⋅ Cristian Meo
- **Bridging the Sim-to-real Gap in RF Localization with Large-Scale Synthetic Pretraining** — Armen Manukyan ⋅ Rafayel Mkrtchyan ⋅ Ararat Saribekyan ⋅ Theofanis Raptis ⋅ Hrant Khachatrian
- **Private Linear Regression via a Down-Sensitivity to Privacy Reduction** — Ittai Rubinstein ⋅ Chris Ge ⋅ Samuel Hopkins
- **The Silent Brush: Artistic Style Leakage in AI Art Generation** — Ninad Joshi ⋅ Ashutosh Ranjan ⋅ Vivek Srivastava ⋅ Shirish Karande
- **OASIS: Online Sample Selection for Continual Instruction Tuning** — Minjae Lee ⋅ Minhyuk Seo ⋅ Tingyu Qu ⋅ Tinne Tuytelaars ⋅ Jonghyun Choi
- **Understanding the Impact of Differentially Private Training on Memorization of Long-Tailed Data** — Jiaming Zhang ⋅ Huanyi Xie ⋅ Meng Ding ⋅ Shaopeng Fu ⋅ Jinyan Liu ⋅ Di Wang
- **[Short] Motion Attribution for Video Generation** — Xindi Wu ⋅ Despoina Paschalidou ⋅ Jun Gao ⋅ Antonio Torralba ⋅ Laura Leal-Taixé ⋅ Olga Russakovsky ⋅ Sanja Fidler ⋅ Jonathan Lorraine
- **Shape of Thought: When Distribution Matters More than Correctness in Reasoning Tasks** — Abhranil Chandra ⋅ Ayush Agrawal ⋅ Arian Hosseini ⋅ Sebastian Fischmeister ⋅ Rishabh Agarwal ⋅ Navin Goyal ⋅ Aaron Courville
- **Infusion: Shaping Model Behavior by Editing Training Data via Influence Functions** — J Rosser ⋅ Robert Kirk ⋅ Edward Grefenstette ⋅ Jakob Foerster ⋅ Laura Ruis
- **Evaluating Language Models in Realistic Conversational Contexts** — Ilija Subasic ⋅ Andrew Rabinovich ⋅ Zhao Chen
- **In-Run Data Shapley for Adam Optimizer** — Meng Ding ⋅ ZEQING ZHANG ⋅ Di Wang ⋅ Lijie Hu
- **Context-Aware Criteria Generation with VLMs for Advertisement Ranking under Data Scarcity** — Kyungho Kim ⋅ Yeonje Choi ⋅ Gyurim Hwang ⋅ Sejin Chung ⋅ Hongseok Lee ⋅ Myeong Song ⋅ Yeongho Kim ⋅ Sunwoo Kim ⋅ Jongha Lee ⋅ Juyeon Kim ⋅ Kijung Shin
- **Multimodal Data Curation Through Ranked Retrieval** — Pratyush Muthukumar ⋅ Harshil Kotamreddy ⋅ Sarah Amiraslani ⋅ Tomo Kanazawa ⋅ Ramani Akkati ⋅ Shaan Jain ⋅ Andrew Mathau
- **Guess the unified model: Domain and Linguistic Effects in Generated Images** — Jasin Cekinmez ⋅ Ryo Mitsuhashi ⋅ Yida Yin
- **AI Scientist Via Synthetic Task Scaling** — Ziyang Cai ⋅ Harkirat Behl
- **On the Strengths and Weaknesses of Data for Open-Set Embodied Assistance** — Pradyumna Tambwekar ⋅ Andrew Silva ⋅ Deepak Edakkattil Gopinath ⋅ Jonathan DeCastro ⋅ Xiongyi Cui ⋅ Guy Rosman
- **ATLAS: Adaptive Transfer Scaling Laws for Multilingual Pretraining, Finetuning, and Decoding the Curse of Multilinguality** — Shayne Longpre ⋅ Sneha Kudugunta ⋅ Niklas Muennighoff ⋅ I-Hung Hsu ⋅ Isaac Caswell ⋅ Alex Pentland ⋅ Sercan Arik ⋅ Chen-Yu Lee ⋅ Sayna Ebrahimi
- **Why Diffusion Language Models Struggle with Truly Parallel (Non-Autoregressive) Decoding?** — Pengxiang Li ⋅ Dilxat Muhtar ⋅ Tianlong Chen ⋅ Lu Yin ⋅ Shiwei Liu
- **The Viability Boundary of Differential Privacy** — Arinbjörn Kolbeinsson ⋅ Benedikt Kolbeinsson
- **Conv-to-Bench: Evaluating Language Models Via User–Assistant Dialogues In Code Tasks** — Victor dos Santos ⋅ André Castro ⋅ Samuel de Souza Toledo ⋅ Bruno Calura ⋅ Lisandra de Moura Menezes ⋅ Raul Mata ⋅ Telma de Lima Soares ⋅ Bryan Lincoln Marques de Oliveira
- **The Era of Real-World Human Interaction: RL from User Conversations** — Chuanyang Jin ⋅ Jing Xu ⋅ Bo Liu ⋅ Leitian Tao ⋅ Olga Golovneva ⋅ Tianmin Shu ⋅ Wenting Zhao ⋅ Xian Li ⋅ Jason E Weston
- **Positive Mining from LLM Seeds: A Semi-Supervised Graph Based Approach to Train Rare Event Classifiers** — Sasan Tavakkol ⋅ Lin Chen ⋅ Max Springer ⋅ Abby Schantz ⋅ Blaž Bratanič ⋅ Vincent Cohen-Addad ⋅ MohammadHossein Bateni
- **GUIrilla: A Scalable Framework for Automated Desktop UI Exploration** — Sofiya Garkot ⋅ Maksym Shamrai ⋅ Ivan Synytsia ⋅ Mariya Hirna
- **[Short] Downstream Effects of Translation Scale with Language Difficulty** — Aditya Vikas Kulkarni ⋅ ⋅ Ammar Ahmed Pallikonda Latheef ⋅ Pritam Mukherjee ⋅ Jacob Luber ⋅ Paul Yi
- **Is More Data Worth the Cost? Dataset Scaling Laws in a Tiny Attention-Only Decoder** — Wiegand ⋅ Lorena Raichle ⋅ Rico Staedeli ⋅ Tomas Hrycej ⋅ Bernhard Bermeitinger ⋅ Siegfried Handschuh
- **Privacy Collapse: Benign Fine-Tuning Can Break Contextual Privacy in Language Models** — Anmol Goel ⋅ Cornelius Emde ⋅ Sangdoo Yun ⋅ Seong Joon Oh ⋅ Martin Gubri
- **Greedy Information Projection for LLM Data Selection** — Victor Ye Dong ⋅ Kuan-Yun Lee ⋅ Jiamei Shuai ⋅ Shengfei Liu ⋅ Yi Liu ⋅ Jian Jiao
- **Do RDB Foundation Models Even Need Data?** — Linjie Xu ⋅ Yanlin Zhang ⋅ Quan Gan ⋅ Minjie Wang ⋅ David Wipf
- **Actor-curator: A Principled Approach to Online Data Selection for RL Post-training** — Zhengyao Gu ⋅ Jonathan Li ⋅ Raul Astudillo ⋅ Ziyu Ye ⋅ Langzhou He ⋅ Wei Cheng ⋅ Santiago Paternain ⋅ Philip Yu ⋅ Yisong Yue
- **COMBATING DATA LAUNDERING IN LLM TRAINING** — Muxing Li ⋅ Zesheng Ye ⋅ Sharon Li ⋅ Feng Liu
- **DUMP: Distribution-Level Curriculum Learning for RL-based LLM Post-training** — Zhenting Wang ⋅ Guofeng Cui ⋅ Yu-Jhe Li ⋅ Kun Wan ⋅ Wentian Zhao
- **VULCAN: Where Agents Learn by Living in Simulated Tool Environments** — Amir Saeidi ⋅ Chitta Baral ⋅ Ahmed H Awadallah ⋅ Harkirat Behl
- **[Short] Studying Memorization Dynamics in Large Language Models Across Pre-Training** — Kaustubh Ponkshe ⋅ Raghav Singhal ⋅ Daniele Affinita ⋅ Martin Jaggi
- **Matched Data, Better Models: Target Aligned Data Filtering with Sparse Autoencoders** — Arnav Das ⋅ Gantavya Bhatt ⋅ Sahil Verma ⋅ Yiping Wang ⋅ Viswa Virinchi Muppirala ⋅ Jeff Bilmes
- **[Short] STRIDE: Training data attribution can be estimated in activation space** — Abir Harrasse ⋅ Rishit Dagli ⋅ Amir Abdullah ⋅ Zhijing Jin
- **OPUS: Towards Principled and Scalable Data Selection for Large Language Model Pre-training in Every Iteration** — Shaobo Wang ⋅ Xuan Ouyang ⋅ Tianyi Xu ⋅ Yuzheng Hu ⋅ Jialin Liu ⋅ Guo Chen ⋅ Tianyu Zhang ⋅ Junhao Zheng ⋅ Kexin Yang ⋅ Xingzhang Ren ⋅ Dayiheng Liu ⋅ Linfeng Zhang
- **Adaptive Structured Transformation: Mitigating Distribution Shift in Dense Retrieval Through Training-Time Preprocessing** — Xinyan Yu ⋅ Harsh Jhamtani ⋅ Soham Dan ⋅ Ben Van Durme ⋅ Patrick Xia
- **Hubble: a Model Suite to Advance the Study of LLM Memorization** — Johnny Wei ⋅ Ameya Godbole ⋅ Mohammad Aflah Khan ⋅ Ryan Wang ⋅ Xiaoyuan Zhu ⋅ James Flemings ⋅ Nitya Kashyap ⋅ Krishna Gummadi ⋅ Willie Neiswanger ⋅ Robin Jia
- **[Short] Where Does Olmo Get Its Values?** — Xiaoqing (Lily) Sun ⋅ Arthur Conmy ⋅ Josh Engels
- **[Short] Max It or Miss It: Benchmarking LLM On Solving Extremal Problems** — Binxin Gao ⋅ Jingjun Han
- **Language Self-Play For Data-Free Training** — Jakub Kuba ⋅ Mengting Gu ⋅ Qi Ma ⋅ Yuandong Tian ⋅ Vijai Mohan ⋅ Chun-cheng Chen
- **Test-Time Meta-Adaptation with Self-Synthesis** — Zeyneb Kaya ⋅ Nick Rui
- **Verifying the Verifiers: Failure Attribution for Benchmark Diagnostics and Training Data Curation** — Jesse Hu ⋅ Pratyush Shukla ⋅ Ke Huang ⋅ Meji Abidoye
- **Benign Overfitting in Adversarial Training for Vision Transformers** — Jiaming Zhang ⋅ Meng Ding ⋅ Shaopeng Fu ⋅ Jingfeng Zhang ⋅ Di Wang
- **Auditing Preference-Based Post-Training of LLMs via Strong Membership Inference Attacks** — Lorenzo Rossi ⋅ Kaif A Shaikh ⋅ Franziska Boenisch ⋅ Adam Dziedzic
- **ImageNet-Think-250K: A Large-Scale Synthetic Dataset for Multimodal Reasoning for Vision Language Models** — Krishna Teja Chitty-Venkata ⋅ Murali Emani
- **An Empirical Study on Noisy Data and LLM Pretraining Loss Divergence** — Qizhen (Irene) Zhang ⋅ Ankush Garg ⋅ Jakob Foerster ⋅ Niladri Chatterji ⋅ Kshitiz Malik ⋅ Mike Lewis
- **Evaluating Frontier Agents on End-to-End Investment Banking Workflows** — Elaine Lau ⋅ Rosemary Wei ⋅ Guram Gogia ⋅ Ronak Chaudhary ⋅ Yi Liu ⋅ Saed Qunbar ⋅ Hui Wen Goh ⋅ Scott Millslagle ⋅ Samuel Danquah ⋅ Punit Arani ⋅ Ray Epps ⋅ Markus Dücker ⋅ Abdullah Arif ⋅ Asrith Devalaraju ⋅ Varsha Sandadi ⋅ Haemi Nam ⋅ Sahil Bhaiwala ⋅ Skyler Wang ⋅ Anish Athalye ⋅ Jonas Mueller ⋅ Francisco Guzmán
- **MixAtlas: Uncertainty-aware Data Mixture for Multimodal LLM Midtraining** — Bingbing Wen ⋅ Sirajul Salekin ⋅ Feiyang Kang ⋅ Bill Howe ⋅ Lucy Lu Wang ⋅ Javier Movellan ⋅ Manjot Bilkhu
- **DSGym: A Standardized and Holistic Framework for Advancing Data Science Agents** — Fan Nie ⋅ Junlin Wang ⋅ Harper Hua ⋅ Federico Bianchi ⋅ Yongchan Kwon ⋅ Zhenting Qi ⋅ Owen Queen ⋅ Shang Zhu ⋅ James Y Zou
- **TRIM: TOKEN-BUDGETED DATA MINING FOR INSTRUCTION TUNING** — Md Muntaqim Meherab ⋅ SALMAN ⋅ Naimur Rahman ⋅ Maruf Billah ⋅ Tanvirul Islam ⋅ Fernaz Nur ⋅ Md. Hasanuzzman Dipu
- **Beyond Training for Cultural Awareness: The Role of Dataset Linguistic Structure in Large Language Models** — Reem Masoud ⋅ Chen Feng ⋅ Shunta Asano ⋅ Saied Alshahrani ⋅ Philip Treleaven ⋅ Miguel Rodrigues
- **[Short] A Formal Language Benchmark for LLMs** — Bishwamittra Ghosh ⋅ Krishna Gummadi ⋅ Evimaria Terzi
- **EPSVec: Efficient and Private Synthetic Data Generation via Dataset Vectors** — Mohammadamin Banayeeanzade ⋅ Qingchuan Yang ⋅ Deqing Fu ⋅ Spencer Hong ⋅ Erin Babinsky ⋅ Alfy Samuel ⋅ Anoop Kumar ⋅ Robin Jia ⋅ Sai Karimireddy
- **The Chicken and Egg Dilemma: Co-optimizing Data and Model Configurations for LLMs** — Zhiliang Chen ⋅ Alfred Leong ⋅ Shao Yong Ong ⋅ Apivich Hemachandra ⋅ Gregory Kang Ruey Lau ⋅ Chuan Sheng Foo ⋅ Zhengyuan Liu ⋅ Nancy Chen ⋅ Bryan Kian Hsiang Low
- **Unmasking LAION-5B: Age, Gender, Race, and Emotion Biases in Large-Scale Image Datasets** — Iris Dominguez-Catena ⋅ Mikel Galar ⋅ Daniel Paternain
- **Hierarchical Agenda Reasoning for Strategic Multi-Turn Dialogue Agents** — Marwa Abdulhai ⋅ Ryan Cheng ⋅ Aryansh Shrivastava ⋅ Aviral Kumar ⋅ Sergey Levine
- **RubricRobustness: Evaluating the Sensitivity of Rubrics-Based Benchmarks to Simple Perturbations** — Manasi Sharma ⋅ Bradley Kenstler ⋅ Bing Liu
- **Winning the Pruning Gamble: A Unified Approach to Joint Sample and Token Pruning for Efficient Supervised Fine-Tuning** — Shaobo Wang ⋅ Jiaming Wang ⋅ Jiajun Zhang ⋅ Cong Wang ⋅ Yue Min ⋅ Zichen Wen ⋅ Xingzhang Ren ⋅ Fei Huang ⋅ Huiqiang Jiang ⋅ Junyang Lin ⋅ Dayiheng Liu ⋅ Linfeng Zhang
- **gen2seg: Generative Models Enable Generalizable Instance Segmentation** — Om Khangaonkar ⋅ Hamed Pirsiavash
- **Data Selection for Fine-tuning Vision Language Models via Cross Modal Alignment Trajectories** — Dang Nguyen ⋅ Nilay Naharas ⋅ Neslihan Bulut ⋅ MohammadHossein Bateni ⋅ Vahab Mirrokni ⋅ Baharan Mirzasoleiman
- **Data Provenance for Image Auto-Regressive Generation** — Bihe Zhao ⋅ Louis Kerner ⋅ Michel Meintz ⋅ Tameem Bakr ⋅ Franziska Boenisch ⋅ Adam Dziedzic

## Organizers

- Zheng Xu
- Ruoxi Jia
- Martin Jaggi
- Mónica Ribero
- Pratyush Maini
- Jiachen (Tianhao) Wang
- Luxi He
- Yuzheng Hu
