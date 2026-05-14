---
title: "Workshop: I Can't Believe It's Not Better — Where LLMs Need to Improve — Key Takeaways"
type: "article"
tags:
  - iclr-2026
  - workshop
  - llm-evaluation
  - llm-limitations
  - reward-hacking
  - safety
related:
  - "raw/iclr-2026-workshop-icbinb-llms.md"
  - "wiki/summaries/iclr-2026-workshop-icbinb-llms.md"
  - "wiki/concepts/llm-evaluation.md"
  - "wiki/concepts/mechanistic-interpretability.md"
  - "wiki/concepts/reward-hacking.md"
sources:
  - "raw/iclr-2026-workshop-icbinb-llms.md"
  - "raw/iclr-2026-workshop-icbinb-llms-talk/"
---

# Workshop: I Can't Believe It's Not Better — Where LLMs Need to Improve — Key Takeaways

## Overview

The [ICBINB LLMs workshop](../../raw/iclr-2026-workshop-icbinb-llms.md) is organized around a simple scientific norm: negative results should be treated as signal, not embarrassment.
The workshop description explicitly centers hallucination, brittle reasoning, alignment failure, and efficiency limits.
It also argues that field-wide incentives still favor positive stories over informative failures.
That makes the event less about one capability area and more about how to do reliable model science.

The transcript continues in exactly that spirit.
The opening remarks frame the workshop as a venue for turning failure modes into design principles.
Instead of asking only how to scale LLMs, the invited talks ask when more inference-time compute hurts, where generative models underperform old baselines, why next-token prediction hits creativity limits, how factuality and uncertainty should be handled, and whether MoE modularity is real or mostly architectural rhetoric.

That combination makes this one of the strongest workshop programs in the repo for the requested research interests.
Interpretability appears through internal signals, probes, and modularity questions.
Human-AI feedback loops appear through reward models, preference data, and evaluation incentives.
Uncertainty estimation is central.
Concept learning and causal reasoning appear through the attempt to separate genuine capability from shortcuts.
And steering shows up in both inference-time alignment and intervention limits.

### Program signal

- The workshop explicitly asks for rigorous limitations studies and null results.
- The opening remarks frame failure analysis as a route to reliability.
- The invited program covers reward hacking, tabular prediction limits, next-token creativity limits, factuality and uncertainty, and MoE modularity.
- Spotlight papers extend the same concerns to hallucination detection, fairness, modality gaps, and safety drift.
- The poster list reinforces the breadth of failure analysis, from steering to uncertainty to spatial reasoning and robustness.

## Key Invited Talks

### 1. Adam Block — When Best-of-N is Worse: Coverage, Reward Hacking, and Pessimism in Inference-Time Alignment

Block's talk is the workshop's clearest theoretical account of why inference-time scaling can fail.
The key point is that sampling more candidates and optimizing against an imperfect reward model does not necessarily improve the true objective.
It can instead amplify reward hacking.

Key takeaways from Block's talk:

- Best-of-N improves estimated reward even when true quality gets worse.
- The right lens is not “more samples are better” but the interaction among coverage, reward-model quality, and evaluation metric.
- Reward hacking emerges because the selected samples are no longer typical under the distribution where the reward model was accurate.
- Pessimistic decoding strategies can mitigate this by penalizing suspiciously high-reward outputs.
- Uncertainty estimates are therefore not optional extras; they are part of alignment at inference time.
- The talk is highly relevant to steering because it shows test-time control can point search in the wrong direction.
- It also offers a strong caution for any agent loop that uses learned verifiers.

### 2. Marta Garnelo — Tree-vial Pursuits: How Humble Decision Trees Still Outsmart the Generative Giants

Garnelo's talk delivers a sharp reminder that linguistic fluency should not be confused with numeric competence.
The central contrast is between strong generative models and old-fashioned tabular methods on prediction tasks where structured data matters more than language priors.

Key takeaways from Garnelo's talk:

- LLM success in language does not imply strong performance on tabular prediction.
- Decision trees and related methods can still outperform much larger generative systems on data modalities they were built for.
- The gap is practically important because much real enterprise and scientific data is tabular.
- This is a caution against reading general intelligence into benchmark wins on text-heavy tasks.
- For interpretability, it suggests that simpler inductive biases may remain valuable in high-stakes settings.
- For PAI, it also raises the possibility that hybrid systems may be more useful than insisting on pure end-to-end LLM solutions.

### 3. Aditi Raghunathan — The Creative Limits of Next-token Prediction

Raghunathan's talk is one of the most direct challenges to the standard autoregressive paradigm in the workshop.
The claim is not that next-token prediction is useless.
It is that it can be systematically myopic on tasks requiring long-range stochastic planning and diverse exploration.

Key takeaways from Raghunathan's talk:

- Next-token learning struggles on tasks that require farsighted planning.
- Multi-token approaches can outperform standard autoregression on those tasks.
- Temperature is a poor universal solution for eliciting diversity.
- Injecting randomness earlier, such as through seed-conditioning, can work better.
- Mode-conditioning can increase reasoning diversity and improve efficiency for math-style search.
- The talk directly connects model objective design to the failure of naive inference-time scaling.
- This is relevant to concept learning because it suggests standard token-level training may not induce the right planning abstractions.

### 4. Preslav Nakov — Towards Truly Open, Language-Specific, Safe, Factual, and Specialized Large Language Models

Nakov's talk is the broadest systems-and-infrastructure talk in the invited lineup.
It connects openness, language coverage, safety, factuality, uncertainty, and specialization.
The most important contribution for this synthesis is that it treats factuality and uncertainty as tool-building problems rather than only benchmark results.

Key takeaways from Nakov's talk:

- Open, language-specific, and specialized models remain necessary despite generalist frontier models.
- Safety must be supported by explicit datasets and evaluation tools such as Do-Not-Answer.
- Factuality requires dedicated infrastructure, including fact-checking systems.
- Cheap uncertainty estimation is valuable enough to deserve standalone tooling, as in LM-Polygraph.
- Machine-generated text detection remains part of the reliability stack.
- The talk highlights multilingual and language-specific failure modes that broad English-centric evaluation can hide.
- It is one of the best examples in the workshop of combining capability building with uncertainty-aware monitoring.

### 5. Sewon Min — Are Mixture-of-Experts Modular? Why It Matters and How to Fix It

Min's talk is about whether MoE architectures are actually modular in a functional sense.
That is a subtle but important question because many practical hopes for control, efficiency, and adaptation depend on modularity being real rather than nominal.

Key takeaways from Min's talk:

- Architectural sparsity does not automatically produce functional modularity.
- If experts are not meaningfully modular, downstream selective use and efficient adaptation become harder.
- ModMoE aims to make modularity a learned property rather than an assumption.
- Semantic specialization matters more than lexical partitioning.
- Better modularity could help both efficiency and controllability.
- This talk connects interpretability to infrastructure design: you cannot steer or analyze experts cleanly if they are not functionally distinct.
- It also resonates with interests in steering and concept representation.

## Themes & Takeaways

### Interpretability

Interpretability here is mostly about finding the source of failure.

- Block studies when reward models stop meaningfully tracking the true objective.
- Min asks whether experts correspond to real functional modules.
- Several spotlight talks use internal signals for hallucination detection or chain-of-thought analysis.
- Garnelo's challenge to tabular reasoning implies that some failures come from representational mismatch, not only missing scale.
- The workshop therefore encourages a mechanistic attitude toward failure rather than surface benchmarking alone.

### Human-AI feedback loops

The workshop repeatedly shows that feedback quality matters as much as model size.

- Block's talk revolves around learned reward models and their failure modes.
- Nakov discusses safety datasets and fact-checking frameworks built around human objectives.
- Clinical and fairness spotlight talks show that user preference and actual safety can come apart.
- The workshop itself is a meta-level intervention on feedback loops in science: it tries to reward informative negative results.
- That is an underappreciated but important design choice.

### Uncertainty estimation

Uncertainty is one of the clearest recurring threads.

- Block uses pessimism and uncertainty-aware penalties to mitigate reward hacking.
- Nakov highlights LM-Polygraph as part of a factuality toolchain.
- Poster titles like “The Anatomy of Uncertainty in LLMs” show the broader community interest.
- Uncertainty is treated as useful at inference time, not only as a reporting metric.
- This is especially relevant to agents, retrieval, and verification loops.

### Concept representation learning

Several talks indirectly ask what concepts current LLMs fail to represent well.

- Garnelo points to structured numerical and tabular concepts.
- Raghunathan points to long-range planning concepts.
- Min focuses on whether experts encode semantically meaningful concepts.
- Many poster titles probe temporal, spatial, or physical concepts that scaling alone does not recover.
- The workshop suggests that failure analysis is often concept analysis in disguise.

### Causal inference

Causality appears in the form of intervention reasoning and failure diagnosis.

- Block studies what happens when we intervene by scaling inference-time compute.
- Raghunathan studies how different generation mechanisms change downstream reasoning behavior.
- Nakov's factuality tooling and detection systems implicitly aim to separate cause from correlation in model outputs.
- Many posters investigate when benchmark behavior reflects format sensitivity rather than real capability.
- The core question is causal in spirit: what changed the behavior, and did that change actually improve the intended property?

### Robotics

Robotics is not central in the invited talks, but it still appears in the broader workshop theme via multimodal failures and physical reasoning papers.

- The poster list includes failures on live task guidance and physical problem solving.
- This matters because reliability claims in LLMs often fail even faster when the model is attached to physical tasks.
- The workshop's general warning is therefore relevant to embodied assistants too: benchmark success can hide fragile internal competence.

### World models

World-model language is not dominant, but several failures touch internal simulation.

- Raghunathan's critique of myopic next-token prediction suggests current models may lack good internal long-horizon search.
- Spatial, temporal, and physical-reasoning posters reinforce that concern.
- The workshop's emphasis on negative results is healthy for world-model research because it pushes beyond glossy demos toward boundary conditions.

### Steering techniques

Steering is one of the most directly discussed topics in the workshop.

- Block shows why naive steering via reward maximization can fail.
- Min suggests modular expert structure may make steering more targeted.
- Posters on prompt interventions, barrier steering, and chain-of-thought unfaithfulness show both the promise and brittleness of steering approaches.
- The broad lesson is that steering must be uncertainty-aware and metric-aware.
- Otherwise it may optimize proxies instead of goals.

## Connections to PAI Research

This workshop is especially useful because it foregrounds failure analysis as a research method.

### For the core agenda

- Interpretability benefits from studying where reward models, experts, and internal signals mislead us.
- Human-AI feedback work gains from Block's and Nakov's analyses of reward modeling and safety datasets.
- Uncertainty estimation is central rather than peripheral.
- Concept learning questions show up in tabular reasoning, planning, modularity, and multilingual reliability.
- Causal inference appears through intervention analysis and proxy-goal failures.

### For robotics, world models, and steering

- Steering is the clearest connection: this workshop shows both why it is necessary and why it fails.
- Raghunathan's critique is relevant to world-model and planning work that depends on meaningful search diversity.
- Physical and multimodal failure papers suggest robotics systems cannot inherit reliability assumptions from text benchmarks.
- If experts become genuinely modular, they may become better interfaces for controllable embodied systems.

### Practical opportunities

- Build inference-time alignment methods that expose uncertainty rather than hide it.
- Compare tabular, symbolic, and hybrid systems against LLM baselines in high-stakes niches.
- Test whether modular experts actually support cleaner steering and monitoring.
- Use negative-result workshops as input to benchmark and evaluation design.
- Study where proxy metrics diverge from the properties users actually care about.

## Signals from Contributed Talks and Posters

The invited program was matched by a broad contributed slate that makes the workshop's diagnosis concrete.
The oral and poster titles show just how many distinct ways “not better” can manifest.

### Contributed talks that sharpen the main claims

- **Lost in Translation** highlights language-specific failure modes that global averages can hide.
- **Sharpness-Aware Pretraining Mitigates Catastrophic Forgetting** suggests that some “model limitations” are really optimization limitations.
- **Attention Sinks as Internal Signals for Hallucination Detection** links interpretability to uncertainty and safety monitoring.
- **Preference–Safety Disassociation in Clinical LLM Evaluation** shows that alignment metrics can diverge from real safety goals.
- **Voice Evaluation of Reasoning Ability** reveals modality-induced capability gaps that standard text benchmarks miss.
- Together these talks reinforce the invited message that failure analysis should look across language, optimization, internals, and evaluation design.

### Poster-level signals worth tracking

- Many posters attack counting, temporal reasoning, spatial reasoning, and physical reasoning, implying that basic structure is still a major weakness.
- Several papers question whether chain-of-thought is faithful, transferable, or even genuinely causal for performance gains.
- There is a strong cluster on prompt interventions and safety control, often emphasizing non-monotonic or brittle effects.
- Uncertainty and calibration appear in multilingual, clinical, and judge-model settings, suggesting that confidence failures remain cross-cutting.
- A number of posters specifically probe steering, probe-based evidence, and hidden confounds, which is highly relevant to interpretability research.
- The poster list also includes multiple “I can't believe...” titles, which fits the workshop norm of making failure itself legible and memorable.
- The breadth of failure modes is itself a result: reliability work cannot rely on one benchmark family or one task distribution.

## Why this workshop matters now

- Inference-time scaling is spreading faster than our understanding of its failure modes.
- Evaluation pipelines increasingly rely on learned judges and reward models, making reward hacking a practical problem.
- Simple capability narratives still dominate public discussion, while boundary conditions are underreported.
- Multilingual, multimodal, and safety-critical use cases expose failures sooner than general-purpose chat benchmarks do.
- A workshop like this helps turn scattered anomalies into a coherent research agenda.

## Reading the workshop as a whole

A useful meta-takeaway from ICBINB is that failure analysis is becoming a first-class methodology for LLM research.

- The workshop treats negative results as compressed scientific information.
- It encourages careful distinction between proxy metrics and actual goals.
- It makes room for cases where more compute, more scale, or more prompting does not help.
- It also normalizes reporting where a baseline stays competitive for principled reasons.
- That cultural shift matters because many reliability problems only become visible when researchers are rewarded for publishing boundary conditions.
- The event therefore contributes not only technical results, but a healthier evaluation norm.
- For researchers working on safety, uncertainty, and steering, that norm is itself a useful research asset.
- It should make future capability claims easier to trust.

## One-sentence synthesis

ICBINB's core message is that the fastest way to build more reliable LLMs may be to study exactly where current recipes break, plateau, or optimize the wrong proxy.

- It also legitimizes publishing careful “this did not work” results.
- That matters for safer deployment, because hidden failures do not stay hidden for long.
- The workshop therefore improves both technical understanding and research culture.

This makes the workshop a useful template for future reliability workshops.

## Open Questions

- How should inference-time alignment balance search power against reward hacking risk?
- What kinds of uncertainty estimates are cheap enough to use by default in deployed systems?
- Are MoEs truly becoming modular, or are we still projecting structure onto them?
- Where exactly does next-token prediction fail for planning and creativity?
- How much of multilingual and multimodal unreliability comes from missing data versus wrong architecture?
- When do simple baselines remain better than giant generative models for structured tasks?
- Can we design steering methods that are robust to proxy misspecification?
- How should scientific incentives change so that negative results become part of normal model development?

## Sources

- [Workshop page](../../raw/iclr-2026-workshop-icbinb-llms.md) — workshop description, invited-talk abstracts, schedule, and contributed-paper context.
- [Workshop recording capture](../../raw/iclr-2026-workshop-icbinb-llms-talk/README.md) — metadata for the recorded livestream.
- [Workshop transcript](../../raw/iclr-2026-workshop-icbinb-llms-talk/transcript.md) — opening remarks and Adam Block's detailed talk segment used here.
