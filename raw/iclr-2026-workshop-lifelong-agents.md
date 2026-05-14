---
title: "Workshop: Lifelong Agents: Learning, Aligning, Evolving"
url: "https://iclr.cc/virtual/2026/workshop/10000805"
source: "other"
author: "ICLR 2026"
date: "2026-04-27"
captured: "2026-05-13"
tags:
  - iclr-2026
  - workshop
  - lifelong-learning
  - agent-alignment
aliases:
  - "ICLR 2026 Lifelong Agents Workshop"
related:
  - "wiki/articles/lifelong-agents-workshop.md"
---

# Workshop: Lifelong Agents: Learning, Aligning, Evolving

**ICLR virtual page timing:** Sun, Apr 26, 2026 · 5:00 AM – 1:00 PM PDT  
**Location:** 101 C  
**Timezone link on page:** America/Los_Angeles

## Workshop description

Artificial intelligence has reached a pivotal stage: while current agentic systems excel in static benchmarks, they struggle to adapt to dynamic, real-world environments. This workshop introduces the concept of lifelong agents, AI systems that continuously learn, align, and evolve across their operational lifespan. Such agents must integrate continual learning, long-term alignment with human values, and self-improvement under resource constraints to remain robust, trustworthy, and sustainable. By uniting research from reinforcement learning, large language models, alignment, embodied AI and more, the workshop seeks to establish shared principles, frameworks, and evaluation methods for creating AI that grows intelligently and responsibly over time.

## Schedule

| Time | Event | Speaker |
|------|-------|---------|
| 9:00 – 9:10 | Morning Opening Remarks | Cheng Qian |
| 9:10 – 9:30 | Introduction to Lifelong Agents | Cheng Qian |
| 9:30 – 10:00 | Invited Talk 1: Robotic Learning with Autonomous Data | Sergey Levine |
| 10:00 – 11:00 | Coffee Break & Poster | — |
| 11:00 – 11:30 | Invited Talk 2: LLM Safety is a Multi-agent Problem | Natasha Jaques |
| 11:30 – 12:00 | Oral Presentations | — |
| 12:00 – 12:30 | Invited Talk 3 | Jun Wang |
| 12:30 – 13:20 | Lunch Break | — |
| 13:20 – 13:30 | Afternoon Opening Remarks | Zhenfei Yin |
| 13:30 – 14:00 | Sponsor Talk Session: Empowering LLMs with More Agency: From Context Engineering to Self-Engineering Architectures | Yan Wang |
| 14:00 – 14:30 | Invited Talk 4 | Asli Celikyilmaz |
| 14:30 – 15:00 | Invited Talk 5: Lifelong Agents from Small Language Models | Siva Reddy |
| 15:00 – 16:00 | Coffee & Posters II | — |
| 16:00 – 16:30 | Invited Talk 6 | Azalia Mirhoseini |
| 16:30 – 17:00 | Student Panel Discussion | Zhenfei Yin |
| 17:00 – 17:15 | Awards and Closing | Zhenfei Yin, Cheng Qian |

## Invited talks

### Robotic Learning with Autonomous Data
**Speaker:** Sergey Levine (UC Berkeley)

**Abstract:** Not found in the ICLR workshop HTML or the public workshop website.

### LLM Safety is a Multi-agent Problem
**Speaker:** Natasha Jaques (University of Washington / Google DeepMind)

**Abstract:** Not found in the ICLR workshop HTML or the public workshop website.

### Invited Talk 3 (title not listed on source page)
**Speaker:** Jun Wang (University College London)

**Abstract:** Not found in the ICLR workshop HTML or the public workshop website.

### Invited Talk 4 (title not listed on source page)
**Speaker:** Asli Celikyilmaz (Microsoft Research)

**Abstract:** Not found in the ICLR workshop HTML or the public workshop website.

### Lifelong Agents from Small Language Models
**Speaker:** Siva Reddy (McGill University / Mila)

**Abstract:** Not found in the ICLR workshop HTML or the public workshop website.

### Invited Talk 6 (title not listed on source page)
**Speaker:** Azalia Mirhoseini (Stanford University / Google DeepMind)

**Abstract:** Not found in the ICLR workshop HTML or the public workshop website.

## Contributed talks

The public OpenReview group lists four papers under `LLA 2026 top5Oral`, which likely correspond to the workshop oral presentation block:

### Agentic Context Engineering: Evolving Contexts for Self-Improving Language Models
**Authors:** Qizheng Zhang, Changran Hu, Shubhangi Upasani, Boyuan Ma, Fenglu Hong, Vamsidhar Kamanuru, Jay Rainton, Chen Wu, Mengmeng Ji, Hanchen Li, Urmish Thakker, James Zou, Kunle Olukotun

**Abstract:** Large language model (LLM) applications such as agents and domain-specific reasoning increasingly rely on *context adaptation*—modifying inputs with instructions, strategies, or evidence, rather than weight updates.  Prior approaches improve usability but often suffer from brevity bias, which drops domain insights for concise summaries, and from context collapse, where iterative rewriting erodes details over time.  Building on the adaptive memory introduced by Dynamic Cheatsheet, we introduce ACE (**A**gentic **C**ontext **E**ngineering), a framework that treats contexts as evolving playbooks that accumulate, refine, and organize strategies through a modular process of generation, reflection, and curation.  ACE prevents collapse with structured, incremental updates that preserve detailed knowledge and scale with long-context models. Across agent and domain-specific benchmarks, ACE optimizes contexts both offline (e.g. system prompts) and online (e.g. agent memory), consistently outperforming strong baselines: +10.6\% on agents and +8.6\% on finance, while significantly reducing adaptation latency and rollout cost.  Notably, ACE could adapt effectively without labeled supervision and instead by leveraging natural execution feedback.  On the AppWorld leaderboard, ACE matches the top-ranked production-level agent on the overall average and surpasses it on the harder test-challenge split, despite using a smaller open-source model. These results show that comprehensive, evolving contexts enable scalable, efficient, and self-improving LLM systems with low overhead.

### ENACT: Evaluating Embodied Cognition with World Modeling of Egocentric Interaction
**Authors:** Qineng Wang, Wenlong Huang, Yu Zhou, Hang Yin, Tianwei Bao, Jianwen Lyu, Weiyu Liu, Ruohan Zhang, Jiajun Wu, Li Fei-Fei, Manling Li

**Abstract:** Embodied cognition argues that intelligence arises from continuous sensorimotor interaction with the world. It raises an intriguing question: do modern vision-language models (VLMs), trained largely in a disembodied manner, exhibit signs of embodied cognition? To investigate this, we introduce ENACT, a benchmark that probes this question through world modeling from egocentric interaction. Grounded in a partially observable Markov decision process (POMDP) framework, ENACT comprises two complementary sequence reordering tasks: forward world modeling (predicting an ordered sequence of future states from actions) and inverse world modeling (inferring an ordered sequence of actions from state changes). Correctly solving these tasks indicates that the model has a solid understanding of how the environment will evolve given one's actions. Our scalable dataset contains 8,972 QA pairs derived from diverse, long-horizon household activities in the BEHAVIOR simulator. Experiments reveal a significant performance gap between state-of-the-art VLMs and humans, which widens dramatically as interaction horizons lengthen. We find that models consistently solve the inverse problem better than the forward one and exhibit strong embodied biases, showing a preference for right-handed actions and performance degradation with camera perspectives that deviate from those of human vision. *This paper has been accepted to ICLR 2026*

### Expanding the Capabilities of Reinforcement Learning via Text Feedback
**Authors:** Yuda Song, Lili Chen, Fahim Tajwar, Rémi Munos, Deepak Pathak, Drew Bagnell, Aarti Singh, Andrea Zanette

**Abstract:** The success of RL for LLM post-training stems from an unreasonably uninformative source: a single bit of information per rollout as binary reward or preference label. At the other extreme, distillation offers dense supervision but requires demonstrations, which are costly and difficult to scale. We study text feedback as an intermediate signal: richer than scalar rewards, yet cheaper than complete demonstrations. Textual feedback is a natural mode of human interaction and is already abundant in many real-world settings, where users, annotators, and automated judges routinely critique LLM outputs. Towards leveraging text feedback at scale, we formalize a multi-turn RL setup, RL from Text Feedback (RLTF), where text feedback is available during training but not at inference. Therefore, models must learn to internalize the feedback in order to improve their test-time single-turn performance. To do this, we propose two methods: Self Distillation (RLTF-SD), which trains the single-turn policy to match its own feedback-conditioned second-turn generations; and Feedback Modeling (RLTF-FM), which predicts the feedback as an auxiliary objective. We provide theoretical analysis on both methods, and empirically evaluate on reasoning puzzles, competition math, and creative writing tasks. Our results show that both methods consistently outperform strong baselines across benchmarks, highlighting the potential of RL with an additional source of rich supervision at scale.

### Self-Distillation Enables Continual Learning
**Authors:** Idan Shenfeld, Mehul Damani, Jonas Hübotter, Pulkit Agrawal

**Abstract:** Continual learning, enabling models to acquire new skills and knowledge without degrading existing capabilities, remains a fundamental challenge for foundation models. While on-policy reinforcement learning can reduce forgetting, it requires explicit reward functions that are often unavailable. Learning from expert demonstrations, the primary alternative, is dominated by supervised fine-tuning (SFT), which is inherently off-policy. We introduce On-Policy Self-Distillation Fine-Tuning (SDFT), a simple method that enables on-policy learning directly from demonstrations. SDFT leverages in-context learning by using a demonstration-conditioned model as its own teacher, generating on-policy training signals that preserve prior capabilities while acquiring new skills. Across skill learning and knowledge acquisition tasks, SDFT consistently outperforms SFT, achieving higher new-task accuracy while substantially reducing catastrophic forgetting. In sequential learning experiments, SDFT enables a single model to accumulate multiple skills over time without performance regression, establishing on-policy distillation as a practical path to continual learning from demonstrations.

## Poster papers

The public OpenReview API lists 100 accepted poster papers under `LLA 2026 Poster`:

- **AccelOpt: A Self-Improving LLM Agentic System for AI Accelerator Kernel Optimization** — Genghan Zhang, Shaowei Zhu, Anjiang Wei, Zhenyu Song, Allen Nie, Zhen Jia, Nandita Vijaykumar, Yida Wang, Kunle Olukotun
- **ACON: Optimizing Context Compression for Long-horizon LLM Agents** — Minki Kang, Wei-Ning Chen, Dongge Han, Huseyin A Inan, Lukas Wutschitz, Yanzhi Chen, Robert Sim, Saravan Rajmohan
- **Actor-Curator: A Scalable RL Post-training Framework with Co-adaptive Curricula** — Zhengyao Gu, Jonathan Light, Raul Astudillo, Ziyu Ye, Langzhou He, Wei Cheng, Santiago Paternain, Philip S. Yu, Yisong Yue
- **Agent0-VL: Exploring Self-Evolving Agent for Tool-Integrated Vision-Language Reasoning** — Jiaqi Liu, Kaiwen Xiong, Peng Xia, Yiyang Zhou, Haonian Ji, Lu Feng, Siwei Han, Mingyu Ding, Huaxiu Yao
- **Agent0: Unleashing Self-Evolving Agents from Zero Data via Tool-Integrated Reasoning** — Peng Xia, Kaide Zeng, Jiaqi Liu, Can Qin, Fang Wu, Yiyang Zhou, Caiming Xiong, Huaxiu Yao
- **AgentGym-RL: An Open-Source Framework to Train LLM Agents for Long-Horizon Decision Making via Multi-Turn RL** — Zhiheng Xi, Jixuan Huang, Chenyang Liao, Baodai Huang, Jiaqi Liu, Honglin Guo, yajie yang, Rui Zheng, Junjie Ye, Jiazheng Zhang, Wenxiang Chen, Wei He, Yiwen Ding, Guanyu Li, Zehui Chen, Zhengyin Du, Xuesong Yao, Yufei Xu, Jiecao Chen, Tao Gui, Zuxuan Wu, Qi Zhang, Xuanjing Huang, Yu-Gang Jiang
- **Agentic Cognitive Profiling: Realigning Automated Alzheimer’s Disease Detection with Clinical Construct Validity** — Jiawen Kang, Kun LI, Dongrui Han, Jinchao Li, Junan Li, Lingwei Meng, Xixin Wu, Helen M. Meng
- **AIF-GEN: Open-Source Platform and Synthetic Dataset Suite for Reinforcement Learning on Large Language Models** — Shahrad Mohammadzadeh, Jacob Chmura, Ivan Anokhin, Jacob-Junqi Tian, Mandana Samiei, Taz Scott-Talib, Irina Rish, Doina Precup, Reihaneh Rabbany, Nishanth Anand
- **Aligning LLMs Toward Multi-Turn Conversational Outcomes Using Iterative RLHF** — Daniel Jiang, Ankur Samanta, Yukai Yang, Jalaj Bhandari, Rémi Munos, Tyler Lu
- **Alignment Propagation: Spreading Cooperative Behaviors in Multi-Agent Systems through Seed Agents** — Asuka Yuxi Zheng, Nicole Hsing, Yi Zhao, Haoqin Tu, Jen-tse Huang
- **AlphaApollo: A System for Deep Agentic Reasoning** — Zhanke Zhou, Chentao Cao, Xiao Feng, Xuan Li, Zongze Li, Xiangyu Lu, Jiangchao Yao, Weikai Huang, Tian Cheng, Jianghangfan Zhang, Tangyu Jiang, Linrui Xu, Yiming Zheng, Brando Miranda, Tongliang Liu, Sanmi Koyejo, Masashi Sugiyama, Bo Han
- **Asymmetric Goal Drift in Coding Agents Under Value Conflict** — Magnus Saebo, Spencer Gibson, Tyler Crosse, Achyutha Menon, Eyon Jang, Diogo Cruz
- **Benchmarking Continual Agent Memory for Online Learning, Transfer, and Forgetting** — Zihang Ma, Jinyi Liu, Hongyao Tang, Yi Ma, Ruitao Wang, Yifu Yuan, YAN ZHENG, Jianye HAO
- **Beyond Reward Maximization: Evaluating the Diversity of Trajectories in Reinforcement Learning with Temporal Vendi Score** — Stanic Tom, Marco Jiralerspong, Zhang Xiaofeng, Danilo Vucetic, Gauthier Gidel
- **BEYOND SYNTAX: ACTION SEMANTICS LEARNING FOR APP AGENTS** — Dezhao Luo, Bohan Tang, Jianheng Liu, Jingxuan Chen, Shaogang Gong, Jianye HAO, Jun Wang, Kun Shao
- **BioProAgent: Neuro-Symbolic Grounding for Constrained Scientific Planning** — Yuyang Liu, Jingya Wang, Liuzhenghao Lv, Yonghong Tian
- **BrowseConf: Confidence-Guided Test-Time Scaling for Web Agents** — Litu Ou, Kuan Li, Huifeng Yin, Liwen Zhang, Zhongwang Zhang, Xixi Wu, Rui Ye, Zile Qiao, Pengjun Xie, Jingren Zhou, Yong Jiang
- **Can We Predict Before Executing Machine Learning Agents?** — Jingsheng Zheng, Jintian Zhang, Yujie Luo, Yuren Mao, Yunjun Gao, Lun Du, Huajun Chen, Ningyu Zhang
- **CAP: A Scalable Benchmark for Evaluating Cross-Site Browser Agents with Complex Actions and Perception** — XuZejun, Taiyi Chen, Jin Li, Yongtong Gu, QiCheng, Lvaixuan, Zhu shuai, ZhuPengfei, Kaichen Yang, Sun Boyu, YixianYang, Mulong Xie, Xiaoteng Ma, Hongru WANG
- **CF-Router: Closed-Form Solution for Expert Selection in Multimodal Agent Lifelong Learning** — Jiaxu Li, Zhijie Zheng, Jianyu Qi, Rongchang Zhao
- **CoDaPO: Confidence and Difficulty-Adaptive Policy Optimization for LLM Reasoning** — Zhanke Zhou, Xiangyu Lu, Chentao Cao, Brando Miranda, Tongliang Liu, Bo Han, Sanmi Koyejo
- **Cold-Start Personalization via Training-Free Priors from Structured World Models** — Avinandan Bose, Shuyue Stella Li, Faeze Brahman, Pang Wei Koh, Simon Shaolei Du, Yulia Tsvetkov, Maryam Fazel, Lin Xiao, Asli Celikyilmaz
- **Constructive Specification for Plug-and-Play Learnware Agents** — Jian-Dong Liu, Zi-Chen Zhao, Hao Sun, Lin-Xing Wu, Huan ZHang, Pengyuan Wang, ZhaoMing, Xinyu Chu, Shu Yan, Yongbei Zhu, Weijun Zhong, Zhi-Hao Tan, SHANG JING, Yang Yu, Zhi-Hua Zhou
- **Continuum: Efficient and Robust Multi-Turn LLM Agent Scheduling with KV Cache Time-to-Live** — Hanchen Li, Qiuyang Mang, Runyuan He, Qizheng Zhang, Huanzhi Mao, Xiaokun Chen, Hangrui Zhou, Alvin Cheung, Joseph E. Gonzalez, Ion Stoica
- **CUA-Suite: Massive Human-annotated Video Demonstrations for Computer-Use Agents** — Xiangru Jian, Shravan Nayak, Kevin Qinghong Lin, Aarash Feizi, Kaixin Li, Patrice Bechard, Spandana Gella, Sai Rajeswar
- **DETACH: Cross-domain Learning for Long-Horizon Tasks via  Mixture of Disentangled Experts** — Yutong Shen, Hangxu Liu, Lei Zhang, Penghui Liu, Ruizhe Xia, Tongtong Feng
- **DomusMind: A Benchmark for Evaluating Lifelong Smart Home Agents Under Drift** — Rong Xu, Yinxin Wan, Xiaochan Xue
- **DRPG (Decompose, Retrieve, Plan, Generate): An Agentic Framework for Academic Rebuttal** — Peixuan Han, YingJie Yu, Jingjun Xu, Jiaxuan You
- **DSGym: A Standardized and Holistic Framework for Advancing Data Science Agents** — Fan Nie, Junlin Wang, Harper Hua, Federico Bianchi, Yongchan Kwon, Zhenting Qi, Owen Queen, Shang Zhu, James Zou
- **DéjàQ: Open-Ended Evolution of Diverse, Learnable and Verifiable Problems** — Willem Röpke, Samuel Coward, Andrei Lupu, Thomas Foster, Tim Rocktäschel, Jakob Nicolaus Foerster
- **Efficient Tree-Structured Deep Research with Adaptive Resource Allocation** — Lunyiu Nie, Nedim Lipka, Ryan A. Rossi, Swarat Chaudhuri
- **Embodied-Reasoner: Synergizing Visual Search, Reasoning, and Action for Embodied Interactive Tasks** — Wenqi Zhang, Mengna Wang, Gangao Liu, Huixin Xu, Yiwei Jiang, Yongliang Shen, Guiyang Hou, Zhe Zheng, Hang Zhang, Xin Li, Jiajun Liu, Weiming Lu, Peng Li, Yueting Zhuang
- **EnterpriseOps-Gym: Environments and Evaluations for Stateful Agentic Planning and Tool Use in Enterprise Settings** — Shiva Krishna Reddy Malay, Shravan Nayak, Jishnu Sethumadhavan Nair, Sagar Davasam, Aman Tiwari, Sathwik Tejaswi Madhusudhan, Sridhar Krishna Nemala, Srinivas Sunkara, Sai Rajeswar
- **EvoTac: A Self-Evolving LLM Agent for Eliciting Reusable Tacit Negotiation Heuristics from Terminal Outcomes** — Runjie Shen, Zhilong Li, Bingzhe Wu
- **ExecTune: Effective Steering of Black-Box LLMs with Guide Models** — Vijay Lingam, Aditya Golatkar, Anwesan Pal, Ben Vo, Narayanan Sadagopan, Alessandro Achille, Jun Huan, Anoop Deoras, Stefano Soatto
- **Experiential Reinforcement Learning** — Taiwei Shi, Sihao Chen, Bowen Jiang, Linxin Song, Longqi Yang, Jieyu Zhao
- **Federated Agent Reinforcement Learning** — Canyu Chen, Kangyu Zhu, Zhaorun Chen, Zhanhui Zhou, Shizhe Diao, Yiping Lu, Tian Li, Manling Li, Dawn Song
- **FocusAgent: Simple Yet Effective Ways Of Trimming The Large Context of Web Agents** — Imene Kerboua, Sahar Omidi Shayegan, Xing Han Lù, Léo Boisvert, Megh Thakkar, Massimo Caccia, Jérémy Espinas, Alex Aussem, Véronique Eglin, Alexandre Lacoste
- **From Word to World: Can Large Language Models be Implicit Text-based World Models?** — Yixia Li, Hongru WANG, Jiahao Qiu, Zhenfei Yin, Dongdong Zhang, Cheng Qian, Zeping Li, Xiaoteng Ma, Guanhua Chen, Heng Ji
- **GASP: Guided Asymmetric Self-Play For Coding LLMs** — Swadesh Jana, Cansu Sancaktar, Tomáš Daniš, Georg Martius, Antonio Orvieto, Pavel Kolev
- **GenEnv: Difficulty-Aligned Co-Evolution Between LLM Agents and Environment Simulators** — Jiacheng Guo, Ling Yang, Peter Chen, Qixin Xiao, Yinjie Wang, Xinzhe Juan, Jiahao Qiu, Ke Shen, Mengdi Wang
- **Generative Control as Optimization: Time Unconditional Flow Matching for Adaptive and Robust Robotic Control** — Zunzhe Zhang, Runhan Huang, Yicheng Liu, Shaoting Zhu, Linzhan Mou, Hang Zhao
- **Group-Evolving Agents: Open-Ended Self-Improvement via Experience Sharing** — Zhaotian Weng, Antonis Antoniades, Deepak Nathani, Zhen Zhang, Sophia Xiao Pu, Xin Eric Wang
- **Hierarchical Agenda Reasoning for Strategic Multi-Turn Dialogue Agents** — Marwa Abdulhai, Ryan Cheng, Aryansh Shrivastava, Aviral Kumar, Sergey Levine
- **Human-Guided Harm Recovery for Computer Use Agents** — Christy Li, Sky CH-Wang, Andi Peng, Andreea Bobu
- **InfoPO: Information-Driven Policy Optimization for User-Centric Agents** — Fanqi Kong, Jiayi Zhang, Mingyi Deng, Chenglin Wu, Yuyu Luo, Bang Liu
- **Inherited Goal Drift: Contextual Pressure Can Undermine Agentic Goals** — Achyutha Menon, Magnus Saebo, Tyler Crosse, Spencer Gibson, Eyon Jang, Diogo Cruz
- **Intrinsic Credit Assignment for Long Horizon Interaction** — Ilze Amanda Auzina, Joschka Strüber, Sergio Hernández-Gutiérrez, Shashwat Goel, Ameya Prabhu, Matthias Bethge
- **Learning Agent Routing From Early Experience** — Yimin Wang, Jiahao Qiu, Xuan Qi, Xinzhe Juan, Jingzhe Shi, Zelin Zhao, Hongru WANG, Shilong Liu, Mengdi Wang
- **Learning on the Job: An Experience-Driven Self-Evolving Agent for Long-Horizon Tasks** — Cheng Yang, Xuemeng Yang, Licheng Wen, Daocheng Fu, Jianbiao Mei, Rong Wu, Pinlong Cai, Yufan Shen, Nianchen Deng, Jia Xu, Botian Shi, Yu Qiao, Haifeng Li
- **Learning Physical Principles from Interaction: Self-Evolving Embodied Planning via Test-Time Memory** — Haoyang Li, Yang You, Hao Su, Leonidas Guibas
- **Learning to Evolve: Scaling Open-Ended Discovery with Relative-Progress RL** — Xuan Li, Zhanke Zhou, Zongze Li, Jiangchao Yao, Bo Han
- **Learning to Self-Evolve** — Xiaoyin Chen, Canwen Xu, Yite Wang, Boyi Liu, Zhewei Yao, Yuxiong He
- **Learning Transferable Skills in Action RPGs via Directed Skill Graphs and Selective Adaptation** — Ali Najar
- **Learning What to Learn: Curriculum Curation for Test-Time Agent Learning** — Qizheng Zhang, Sherry Ruan, Shubhangi Upasani, Fenglu Hong, Changxiu Ji, Changran Hu, Bo Li, Hanchen Li, Kunle Olukotun
- **LHAW: Controllable Underspecification for Long-Horizon Tasks** — George Pu, Michael S. Lee, Udari Madhushani Sehwag, David J. Lee, Bryan Zhu, Yash Maurya, Mohit Raghavendra, Yuan Xue, Samuel Marc Denton
- **Lifelong Contextual Safety Alignment at Test Time for Multi-Modal LLMs** — Ce Zhang, Jinxi He, Junyi He, Katia P. Sycara, Yaqi Xie
- **Log-Augmented Generation: Scaling Test-Time Reasoning with Reusable Computation** — Peter Baile Chen, Yi Zhang, Dan Roth, Samuel Madden, Jacob Andreas, Mike Cafarella
- **MAGE: Meta-Reinforcement Learning for Language Agents toward Strategic Exploration and Exploitation** — lu Yang, Zelai Xu, Minyang Xie, Jiaxuan Gao, zhao shok, Yu Wang, Yi Wu
- **Mem$^2$Evolve: Towards Self-Evolving Agents via Co-Evolutionary Capability Expansion and Experience Distillation** — Zihao Cheng, Zeming Liu, Yingyu Shan, Xinyi Wang, Xiangrong Zhu, Yunpu Ma, Hongru WANG, Yuhang Guo, Wei Lin, Yunhong Wang
- **MemoryCD: Benchmarking Long-Context User Memory of  LLM Agents for Lifelong Cross-Domain Personalization** — Weizhi Zhang, Xiaokai Wei, Wei-Chieh Huang, Zheng Hui, Chen Wang, Michelle Gong, Philip S. Yu
- **MindZero: Learning Online Mental Reasoning With Zero Annotations** — Shunchi Zhang, Jin Lu, Chuanyang Jin, Yichao Zhou, Zhining Zhang, Tianmin Shu
- **MobileMem: Evaluating Long-Horizon Memory for Language Agents in Real-World Mobile Environments** — Xinle Deng, Yida Xue, Yijun Chen, Mingjun Mao, Ruobin Zhong, Buqiang Xu, Jizhan Fang, Haoming Xu, Tingwei Wu, Yajing Xu, Shumin Deng, Haofen Wang, Huajun Chen, Ningyu Zhang
- **Narrow Fine-Tuning Erodes Safety Alignment in Vision-Language Agents** — Idhant Gulati, Shivam Raval
- **Navigating the Cost-Performance Pareto Frontier of Test-Time LLM Agent Adaptation** — Konrad Szafer, Xiaozhe Yao, Maximilian Böther, Gregor Bachmann, Tiago Pimentel, Ana Klimovic
- **Not All Clients Are Equal: Collaborative Model Personalization on Heterogeneous Multi-Modal Clients** — Minhyuk Seo, Taeheon Kim, Hankook Lee, Jonghyun Choi, Tinne Tuytelaars
- **Noticing the Watcher: LLM Agents Can Infer CoT Monitoring from Blocking Feedback** — Thomas Jiralerspong, Flemming Kondrup, Yoshua Bengio
- **OceanGym: Evaluating Language-Grounded Embodied Agents in Underwater Environments** — Yida Xue, Mingjun Mao, Xiangyuan Ru, Yuqi Zhu, Baochang Ren, Shuofei Qiao, Mengru Wang, Shumin Deng, Xinyu An, Ningyu Zhang, Ying Chen, Huajun Chen
- **On Group Relative Policy Optimization Collapse in Agent Search: The Lazy Likelihood-Displacement** — Wenlong Deng, Yushu Li, Boying Gong, Yi Ren, Christos Thrampoulidis, Xiaoxiao Li
- **On Path to Multimodal Historical Reasoning: HistBench and HistAgent** — Jiahao Qiu, Fulian Xiao, Yimin Wang, Yuchen Mao, Yijia Chen, Xinzhe Juan, Siran Wang, Xuan Qi, Tongcheng Zhang, Zixin Yao, Jiacheng Guo, Yifu Lu, Charles Argon, Jundi Cui, Daixin Chen, Junran Zhou, Shuyao Zhou, Zhanpeng Zhou, Ling Yang, Shilong Liu, Hongru WANG, Kaixuan Huang, xun jiang, Xi Gao, Mengdi Wang
- **One Model, Many Goals: Meta-Learning Preference-Conditioned Alignment for Lifelong LLM Agents** — Fatemeh Nourzad, Daouda Sow, Yingbin Liang, Ming Shi, Ming Zhang, Yunxuan Li, Eylem Ekici, Ness Shroff
- **PACEvolve: Enabling Long-Horizon Progress-Aware Consistent Evolution** — Minghao Yan, Bo Peng, Benjamin Coleman, Ziqi Chen, Zhouhang Xie, Shuo Chen, Zhankui He, Noveen Sachdeva, Isabella Ye, Weili Wang, Chi Wang, Ed H. Chi, Fernando Pereira, Wang-Cheng Kang, Derek Zhiyuan Cheng, Beidou Wang
- **Paying Less Generalization Tax: A  Cross-Domain Generalization Study of RL Training  for LLM Agents** — Zhihan Liu, Lin Guan, Yixin Nie, Kai Zhang, Zoey Hao, Lin Chen, Asli Celikyilmaz, Zhaoran Wang, Na Zhang
- **PEARL: Self-Evolving Assistant for Time Management** — Bingxuan Li, Jeonghwan Kim, Cheng Qian, Xiusi Chen, Eitan Anzenberg, Niran Kundapur, Heng Ji
- **PlugMem: A Task-Agnostic Plugin Memory Module for LLM Agents** — Ke Yang, Zixi Chen, Xuan He, Jize Jiang, Michel Galley, Chenglong Wang, Jianfeng Gao, Jiawei Han, ChengXiang Zhai
- **PolicyBank: Evolving Policy Understanding For Evolving Agents** — Jihye Choi, Jinsung Yoon, Long T. Le, Somesh Jha, Tomas Pfister
- **Pushing Forward Pareto Frontiers of Proactive Agents with Behavioral Agentic Optimization** — Yihang Yao, Zhepeng Cen, Haohong Lin, Shiqi Liu, Zuxin Liu, Jiacheng Zhu, Zhang-Wei Hong, Laixi Shi, Ding Zhao
- **ReCreate: Reasoning and Creating Domain Agents Driven by Experience** — Zhezheng Hao, Hong Wang, Jian Luo, Jianqing Zhang, Yuyan Zhou, Qiang Lin, Can Wang, Hande Dong, Jiawei Chen
- **ReMix: Reinforcement Routing for Mixtures of LoRAs in LLM Finetuning** — Ruizhong Qiu, Hanqing Zeng, Yinglong Xia, Yiwen Meng, Ren Chen, Jiarui Feng, Dongqi Fu, Qifan Wang, Jiayi Liu, Jun Xiao, Xiangjun Fan, Benyu Zhang, Hong Li, Zhining Liu, Hyunsik Yoo, Zhichen Zeng, Tianxin Wei, Hanghang Tong
- **Residual Off-Policy RL for Finetuning Behavior Cloning Policies** — Lars Lien Ankile, Zhenyu Jiang, Rocky Duan, Guanya Shi, Pieter Abbeel, Anusha Nagabandi
- **ScenDroid: A Scenario-Level Benchmark for Long-Horizon, Time-Evolving GUI Agents** — Zhe Wu, Yongxin Kang, Dabin Sheng, Junliang Xing, Guokun Wu, Derek Yuen, Donglin Mo, Yuheng Jing, Kai Li, Weilin Luo, Kun Shao, Yuanchun Shi
- **Self-Distilled Reasoner: On-Policy Self-Distillation for Large Language Models** — Siyan Zhao, Zhihui Xie, Mengchen Liu, Jing Huang, Guan Pang, Feiyu Chen, Aditya Grover
- **Self-Questioning Language Models** — Lili Chen, Mihir Prabhudesai, Katerina Fragkiadaki, Hao Liu, Deepak Pathak
- **SimpleMem: Efficient Lifelong Memory for LLM Agents** — Jiaqi Liu, Yaofeng Su, Peng Xia, Siwei Han, Zeyu Zheng, Cihang Xie, Mingyu Ding, Huaxiu Yao
- **SkillRL: Evolving Agents via Recursive Skill-Augmented Reinforcement Learning** — Peng Xia, Jianwen Chen, Hanyang Wang, Jiaqi Liu, Kaide Zeng, Yu Wang, Siwei Han, Yiyang Zhou, Xujiang Zhao, Haifeng Chen, Zeyu Zheng, Cihang Xie, Huaxiu Yao
- **Streaming Memory Benchmark: Stage-level Diagnosis with Evidence Dependency Control** — Guanming Liu, Haoran Yin, LITIANCHEN, Sikuan Yan, Hongru WANG, Baian Chen, Xiaoteng Ma
- **SWITCH: Benchmarking Interaction and Verification on Real-World Interfaces in Lifelong Embodied Agents** — Jieru Lin, Zhiwei Yu, Börje F. Karlsson
- **The Agent's First Day: Benchmarking Learning, Exploration, and Scheduling in the Workplace Scenarios** — Daocheng Fu, Jianbiao Mei, Rong Wu, Xuemeng Yang, Jia Xu, Yufan Shen, Ding Wang, Pinlong Cai, Yong Liu, Licheng Wen, Botian Shi
- **The Hidden Costs of Domain Fine-Tuning: Pii-Bearing Data Degrades Safety and Increases Leakage** — Jayesh Choudhari, Piyush Singh
- **TSR: Trajectory‑Search Rollouts for Multi‑Turn RL of LLM Agents** — Aladin Djuhera, Swanand Ravindra Kadhe, Farhan Ahmed, Heiko Ludwig, Holger Boche
- **TTCS: Test-Time Curriculum Synthesis for Self-Evolving** — Chengyi Yang, Zhishang Xiang, Yunbo Tang, Zongpei Teng, Chengsong Huang, Yuhan Liu, Jinsong Su
- **Understanding Knowledge Acquisition and Release in Language Models via Circuits** — Kiran Raja, Arav Maheria, Andrew Bae, Alan Sun
- **Understanding Reasoning Collapse in Multi-Turn Agent Reinforcement Learning** — Zihan Wang, Chi Gui, Xing Jin, Qineng Wang, Licheng Liu, Kangrui Wang, Shiqi Chen, Linjie Li, Zhengyuan Yang, Pingyue Zhang, Yiping Lu, Jiajun Wu, Li Fei-Fei, Lijuan Wang, Yejin Choi, Manling Li
- **Universe Routing: Why Self-Evolving Agents Need Epistemic Control** — Zhaohui Geoffrey Wang
- **Verifying the Verifiers: Failure Attribution for Agentic Benchmark Diagnostics and Training Data Curation** — Jesse Hu, Pratyush Shukla, Ke Huang
- **VerlTool: Towards Holistic Agentic Reinforcement Learning with Tool Use** — Dongfu Jiang, Yi Lu, Zhuofeng Li, Zhiheng Lyu, Ping Nie, Haozhe Wang, Alex Su, Hui Chen, Kai Zou, Chao Du, Tianyu Pang, Wenhu Chen
- **Weasel: Out-of-Domain Generalization for Web Agents via Importance-Diversity Data Selection** — Fatemeh Pesaran zadeh, Seyeon Choi, Xing Han Lù, Siva Reddy, Gunhee Kim
- **When Drafts Evolve: Speculative Decoding Meets Online Learning** — Yu-Yang Qian, Hao-Cong Wu, Yichao Fu, Hao Zhang, Peng Zhao
- **Which Memory Operation Drives Recovery? A Factorial Study of Retrieve, Write, and Manage Adaptation under Domain Shift** — Zhaoxiang Feng, Mingyang Yao, Charlie Sun, David Scott Lewis
- **Zombie Agents: Persistent Control of Self-Evolving LLM Agents via Self-Reinforcing Injections** — XIANGLIN YANG, Yufei He, Shuo Ji, Bryan Hooi, Jin Song Dong

## SlidesLive IDs

- No SlidesLive presentation IDs were found in the ICLR workshop HTML. The only SlidesLive-related artifact in the page source is the generic embed script `https://slideslive.com/embed_presentation.js`.

## Organizers

- Emre Can Acikgoz
- Cheng Qian
- Hongru WANG
- Zhenfei Yin
- Manling Li
- Yun-Nung Chen
- Jiahao Qiu
- Guanhua Chen
- Caiming Xiong
- Mengdi Wang

## Extraction notes

- The ICLR workshop HTML exposed the workshop abstract, organizers, room, and event timing.
- The logged-out ICLR page did not include inline schedule rows, invited-talk abstracts, or talk/poster lists; those sections were supplemented from the public workshop website and the public OpenReview API for this workshop.
- No concrete SlidesLive presentation IDs were found in the ICLR HTML; the page only includes a generic `https://slideslive.com/embed_presentation.js` script tag.
- Public OpenReview counts retrieved during capture: 4 oral papers (`LLA 2026 top5Oral`) and 100 poster papers (`LLA 2026 Poster`).
