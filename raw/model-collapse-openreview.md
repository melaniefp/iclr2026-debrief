---
title: "Model Collapse Is Not a Bug but a Feature in Machine Unlearning for LLMs"
url: "https://openreview.net/forum?id=1MCQzboBrR"
source: "openreview"
author: "Yan Scholten, Sophie Xhonneux, Leo Schwinn, Stephan Günnemann"
date: "2026-04-23"
captured: "2026-05-13"
tags:
  - iclr-2026
  - openreview
  - machine-unlearning
  - model-collapse
  - large-language-models
  - llms
related:
  - "wiki/papers/model-collapse.md"
---

# Model Collapse Is Not a Bug but a Feature in Machine Unlearning for LLMs

**OpenReview:** [1MCQzboBrR](https://openreview.net/forum?id=1MCQzboBrR)
**Venue:** ICLR 2026 Poster

## Abstract

Current unlearning methods for LLMs optimize on the private information they seek to remove by incorporating it into their fine-tuning data. We argue this not only risks reinforcing exposure to sensitive data, but also fundamentally contradicts the principle of minimizing its use. As a remedy, we propose a novel unlearning method—Partial Model Collapse (PMC), which does not require unlearning targets in the unlearning objective. Our approach is inspired by recent observations that training generative models on their own generations leads to distribution collapse, effectively removing information from model outputs. Our central insight is that model collapse can be leveraged for machine unlearning by deliberately triggering it for data we aim to remove. We theoretically analyze that our approach converges to the desired outcome, i.e. the model unlearns the data targeted for removal. We empirically demonstrate that PMC overcomes four key limitations of existing unlearning methods that explicitly optimize on unlearning targets, and more effectively removes private information from model outputs while preserving general model utility. Overall, our contributions represent an important step toward more comprehensive unlearning that better aligns with real-world privacy constraints.

**TL;DR:** We show that model collapse can be intentionally triggered to make LLMs unlearn specific information, turning it into a practical method for machine unlearning.

## Decision

**Decision:** Accept (Poster)

## Area Chair Meta-Review

This submission makes a novel connection between model collapse and machine unlearning in the context of generative models such as LLMs and question-answering tasks, and proposed a novel unlearning scheme --- Partial Model Collapse or PMC --- that does not require the explicit use of the ground-truth answers for the questions in the forget set. The submission presents a multi-faceted unlearning evaluation on the TOFU dataset, highlighting the strong utility-unlearning tradeoff of PMC compared to existing unlearning baselines, as well as novel failure modes for existing unlearning schemes (which the proposed PMC continues to be robust). All reviewers acknowledge this novelty, and the well-structured and high-quality writing in the submission.

However, all reviewers raised the following concerns:

- The evaluation is limited to a single unlearning dataset TOFU. Thus, while the results demonstrate extremely strong performance of the proposed PMC, it is not clear whether the conditions underlying the motivations behind PMC would hold for unlearning setups other than TOFU.
  - The authors responded to this by providing an additional evaluation on a subset of the MUSE dataset, demonstrating similar strong performance for the proposed PMC. The authors also argue that the thorough multi-faceted evaluation on the TOFU dataset is also of high value in its own accord.
  - In my opinion, this partially addresses the issue though a thorough evaluation on MUSE and WMDP benchmarks would completely address this issue.
- The computational overhead of the proposed PMC requiring multiple rounds of generations for each forget set query is not clear, and an proper evaluation of approximate unlearning requires analysis of the unlearning-utility-runtime tradeoff.
  - The authors responded by providing a more detailed evaluation of the computational costs of PMC relative to the NPO and SimNPO baselines.
  - One interesting aspect of the additional results presented in Appendix C.3 is the sudden dramatic initial drop in the utility of the model for PMC, which the model recovers as the unlearning continues. However, this implies that, within a 10-15 minute unlearning time-frame (for the models considered here), the unlearning quality of the proposed PMC and the baselines SimNPO and NPO are comparable, while the utility of the proposed PMC is significantly worse. This is one aspect of the unlearning dynamics that was not apparent in the initial analysis, and is made clear with this additional evaluations of computational costs. The current analysis also does not show the interplay of the balancing parameter $\lambda$, where a smaller value of $\lambda$ might extend the amount of time required for the utility recovery.
  - If we are allowing additional time, fine-tuning on the retain set (with similar amount of time) is also an important baseline to consider. It is known that fine-tuning only on the retain set can induce catastrophic forgetting on the forget set, thereby leading to empirical unlearning, and extended fine-tuning can improve unlearning efficacy. Thus, it is important to show that, for the same amount of unlearning time, the proposed PMC can significantly outperform unlearning via fine-tuning only on the retain set.
  - Thus, in my opinion, this concern is again only partially addressed as the response itself raised some more questions (for example, in terms of the intermediate time-frame performance of PMC and the consideration of other baselines such as fine-tuning).


Thus, overall, I think this is an interesting submission, making a very intuitive connection between model collapse and machine unlearning, leading to a novel unlearning scheme with extremely strong performance (in a somewhat limited evaluation on only a single benchmark). I am recommending an accept though this can be bumped down if necessary.

## Review 1 (Reviewer_Jbgi)

**Rating:** 6
**Confidence:** 3
**Soundness:** 3
**Presentation:** 4
**Contribution:** 3

### Summary
The study introduced PMC, Partial Model Collapseas, as a effective unlearning method for LLMs. PMC is to let a model relearn on its own generated outputs on targeted queries. This self-training gradually collapses the model’s confidence on unwanted responses while maintaining general utility.

### Strengths
Overall, the study offers a novel unlearning approach based on model collapse, which is often viewed as a defect. The proposed PMC method is original in both formulation and intuition, achieving unlearning without relying on the sensitive information that needs to be removed. The preference-guided self-training mechanism is also an interesting idea.

The technical quality of this paper is strong, with a solid theoretical foundation and convincing empirical validation on the benchmark. The comparisons with prior methods, e.g. GA, GD, NPO, and SimNPO, clearly demonstrate the effectiveness of PMC. The ablation studies on temperature, sample count, and weighting are also thorough and well executed.

The paper is well written and easy to follow. The overall presentation is clear and well organized.

### Weaknesses
The experiments rely solely on the TOFU dataset, which is somewhat limiting. It would be beneficial to validate the performance on additional benchmarks such as MUSE, WMDP, or others to strengthen the empirical evidence.

PMC is compared against GA, GD, NPO, and SimNPO, but not against several recent unlearning methods, such as SCRUB, DPO, or Negative Preference Fine-Tuning. Including these comparisons would provide a more comprehensive evaluation of the proposed approach.

It would also be valuable to discuss the potential applicability and performance of PMC in other domains, such as image or tabular data, to better understand its generality.

Moreover, the discussion and analysis of computational cost could be expanded, including runtime, resource usage, and scalability with model size and data volume.

### Questions
L132, "In this work, we study empirical machine unlearning for generative models..." Should that be just LLM?

" Note that we do not require access to the ground truth answers for the forget questions, and we assume disjoint support of pf(q) and the marginal distribution pr(q), i.e. we either want to unlearn the response to a question or not." What if there are overlaps between responses to be removed and not to be removed?

L840, minor latex issue, ’Yes’ -> `Yes’

## Review 2 (Reviewer_ugX6)

**Rating:** 6
**Confidence:** 4
**Soundness:** 3
**Presentation:** 3
**Contribution:** 3

### Summary
The paper introduces Partial Model Collapse (PMC), a learning-to-forget procedure that reframes machine unlearning as iterative relearning on self-generated samples. It presents a practical algorithm for LLMs that avoids using ground-truth forget answers by sampling candidate responses and updating on a preference-selected sample while jointly training on retain data. Theoretically, the paper proves convergence properties of the iterative process under idealized assumptions, and motivates the approach via categorical-distribution warm-ups. Empirically, PMC expands the Pareto front between unlearn quality and utility.

### Strengths
- The paper offers a interesting perspective: leveraging model collapse via iterative relearning on self-generated data as a mechanism for unlearning, with a clear derivation from categorical settings and a principled LLM instantiation.

- The theoretical section establishes convergence of the reward and vanishing variance for the iterative update under stated assumptions, providing a clear link between the objective and unlearning behavior.

- The algorithmic procedure is explicit and the narrative emphasizes why avoiding ground-truth forget answers can prevent unintended reinforcement.

- PMC expands the utility–unlearn-quality Pareto front for backbone model, indicating practical promise.

### Weaknesses
- Evaluation scope is narrow. Experiments focus on a single unlearning benchmark (TOFU), two LLMs (Phi-1.5, Llama-3.2-3B-Instruct), limiting generality. Additional datasets and tasks would bolster claims.

- Computational cost. The method depends on sampling from the model distribution and the paper acknowledges overhead for LLMs. A clearer cost–benefit analysis or experimental comparisons versus baselines would enhance soundness.

- Assumptions behind the theory are strong. Theoretical arguments rely on idealized settings, e.g., no approximation error, rendering parts of the proofs rather trivial.

### Questions
1. How does PMC perform under prompt-injection attack?

2. Is PMC able to achieve superior efficiency in the trade-off between computational resources and performance benefits relative to the baseline models?

## Review 3 (Reviewer_PRv6)

**Rating:** 4
**Confidence:** 3
**Soundness:** 3
**Presentation:** 3
**Contribution:** 3

### Summary
This paper introduces Partial Model Collapse (PMC), a novel paradigm for machine unlearning in large language models (LLMs). Unlike existing methods that rely on direct optimization against sensitive unlearning targets, PMC leverages the natural information loss inherent in model collapse—the degradation observed when models are repeatedly fine-tuned on self-generated data. The core idea is to intentionally trigger partial collapse in response to sensitive queries, allowing the model to “forget” without reusing private data.

### Strengths
- The paper reinterprets model collapse, typically seen as undesirable, into a constructive mechanism for unlearning—an elegant and theoretically grounded insight.

- Clear mathematical derivation of convergence properties (Lemma 1, Theorem 2) and ablation studies validating the hyperparameter behavior.

- The paper is clearly structured, visually intuitive, and well-written.

### Weaknesses
- While conceptually elegant, PMC requires multiple sampling and fine-tuning iterations, potentially increasing computational cost. Could the authors quantify runtime and explore lightweight approximations?

- The method’s performance hinges on the choice of reward function r(x). How robust is PMC to alternative reward definitions, and can it generalize beyond ROUGE-based divergence metrics?

- The theoretical analysis assumes idealized convergence. How does PMC behave when unlearning large sets simultaneously or when errors accumulate over many collapse steps?

### Questions
Refer to the Weakness above.

## Review 4 (Reviewer_G3SG)

**Rating:** 4
**Confidence:** 4
**Soundness:** 3
**Presentation:** 2
**Contribution:** 2

### Summary
The paper proposes Partial Model Collapse (PMC), a new machine unlearning method for large language models. The key idea is to deliberately induce controlled model collapse by fine-tuning a model only on its own generated outputs for questions whose answers must be forgotten. Unlike existing empirical unlearning methods, PMC does not require access to or optimization directly over the private “forget” answers, which the authors claim reduces leakage risk and preserves privacy. The paper includes a theoretical formulation showing convergence toward a collapsed output distribution and presents empirical results on the TOFU benchmark indicating improved unlearning-utility trade-offs and reduced side effects.

### Strengths
The paper challenges the dominant paradigm of unlearning systems that explicitly suppress or optimize against ground truth sensitive answers, proposing a more privacy-aligned direction: remove private knowledge without touching the private data itself. This direction is well-motivated in regulatory contexts such as GDPR. The high-level design is simple and connects strongly with recent discussions about distribution collapse in synthetic self-training. Empirical results show improvements on several relevant axes including utility retention, robustness under sampling attacks, and reduced unintended suppression of semantically similar tokens. These highlight that the authors care not only about benchmark metrics but also about subtle security implications.

### Weaknesses
There are notable limitations in the current form. First, the theoretical results are built on highly abstract distributions and reward convergence assumptions, and the paper does not convincingly bridge these assumptions with actual LLM behavior. Second, all experiments are on a synthetic dataset (TOFU), so claims of “privacy-preserving” remain hypothetical. Third, some baselines are insufficiently understood or tuned to ensure fairness: certain hyperparameter choices appear inconsistent with prior literature. Fourth, the collapse mechanism could potentially degrade knowledge in areas semantically close to the forget domain, yet the evaluation of utility is relatively narrow, relying mostly on ROUGE. Last, computational overhead implications are minimized rather than rigorously quantified.

### Questions
It would help to clarify how PMC avoids “over-forgetting” in more complex semantic spaces. For example, if the model self-generates answers that gradually omit related but still essential information, how do you detect and prevent cascading collapse? Better visualization of token-level drift could strengthen this point.

The paper acknowledges that computational cost of repeated sampling is a bottleneck, but offers no concrete profiling or mitigation strategies. Could a smaller proxy model or distillation-based filtering accelerate collapse while preserving safety? Please include runtime vs unlearning efficacy trade-offs.

On the theoretical side, Theorem 2 depends on no statistical or function approximation error. LLMs always operate under approximation, so the guarantee is weakened. Could you provide empirical convergence plots matching the theorem’s predicted reward evolution?
The TOFU benchmark, while convenient, lacks realistic attack surfaces and nuanced sensitive information patterns. Any evidence on real-world factual unlearning tasks would dramatically improve credibility.

Hyperparameter search for baselines might be unintentionally restrictive. For example, NPO often shows higher stability when λ is dynamically adjusted. Please clarify search ranges and why they fairly reflect best-practice settings.

For privacy claims, you state that PMC avoids using sensitive data. However, model self-generations may already encode the sensitive data. Under what conditions does PMC not reinforce hidden memorization before collapse? More discussion of this risk is needed.