---
title: "Workshop: Principled Design for Trustworthy AI — Key Takeaways"
type: "article"
tags:
  - iclr-2026
  - workshop
  - trustworthy-ai
  - interpretability
  - robustness
  - uncertainty
  - safety
related:
  - "raw/iclr-2026-workshop-trustworthy-ai.md"
  - "wiki/summaries/iclr-2026-workshop-trustworthy-ai.md"
  - "wiki/concepts/mechanistic-interpretability.md"
  - "wiki/concepts/uncertainty-in-llms.md"
sources:
  - "raw/iclr-2026-workshop-trustworthy-ai.md"
  - "raw/iclr-2026-workshop-trustworthy-ai-talk/"
---

# Workshop: Principled Design for Trustworthy AI — Key Takeaways

## Overview

The [Trustworthy AI workshop](../../raw/iclr-2026-workshop-trustworthy-ai.md) is unusually broad without becoming vague.
Its description spans interpretability, inference-time monitoring, multimodal trust, robustness, formal verification, uncertainty, trust calibration, and LLM-agent safety.
What holds those topics together is the phrase “principled design.”
The workshop is less interested in patching symptoms after deployment than in designing systems whose representations, objectives, and interfaces make trustworthy behavior more likely from the beginning.

The transcript supports that framing.
The opening remarks enumerate six pillars: interpretable models, inference-time safety, multimodal trust challenges, robustness and threat models, trust evaluation, and safe LLM agents.
The keynotes then instantiate those pillars from very different angles.
Mihaela van der Schaar argues for moving beyond forecasting toward understanding dynamical systems.
Fernanda Viégas argues for user-facing transparency dashboards.
Hamed Hassani focuses on catastrophic forgetting in post-training.
Violet Peng presents compute-efficient interventions for safety and multilingual control.
Yan Liu focuses on actionable interpretability through feature interaction.

Taken together, the workshop suggests that trustworthy AI needs multiple layers of understanding.
We need internal representation analysis.
We need causal and temporal understanding of system behavior.
We need monitoring tools that ordinary users can access.
We need post-training methods that do not destroy earlier capabilities.
And we need efficient steering mechanisms that work under real compute constraints.
This makes the workshop directly relevant to nearly all of the requested research interests.

### Program signal

- The workshop description explicitly spans the full lifecycle from training to deployment.
- The six pillars in the opening remarks give a clean organizing framework.
- The keynote lineup covers causality, user-facing interpretability, continual robustness, safety interventions, and feature interactions.
- The spotlight paper list extends this to LoRA brittleness, sparse autoencoders, subgroup fairness, and test-time training failures.
- The workshop consistently treats trust as a property of systems and processes, not only of outputs.

## Key Invited Talks

### 1. Mihaela van der Schaar — Stop Forecasting! Start Understanding Time Series Dynamics and Causality!

Van der Schaar's talk is the clearest causal-inference keynote in the workshop.
Her main argument is that high-stakes settings require more than accurate forecasting.
We need interpretable-by-design representations of trajectories and eventually semantic representations of the underlying dynamical system itself.

Key takeaways from van der Schaar's talk:

- Forecasting is insufficient for trustworthy use in medicine, finance, and other high-stakes settings.
- Post hoc explanation and uncertainty estimation help, but they do not solve the core problem.
- Time-series trajectories should be represented in human-meaningful motifs and compositions.
- Interpretability by design allows the system to answer “what if,” “how to,” and “how still” questions about trajectories.
- The next step is semantic modeling of the underlying dynamical system rather than only the observed signal.
- This is explicitly tied to causal reasoning, interventions, and distribution shift.
- The talk is highly relevant to world models because it asks what it means to understand system dynamics rather than merely imitate them.

### 2. Fernanda Viégas — How AI Chatbots See Us: Making Interpretability User-Facing

Viégas pushes interpretability in a different direction.
Instead of asking only how researchers inspect models, she asks what end users should be allowed to see about how a system is modeling them.
This is perhaps the most direct human-centered interpretability talk in the workshop.

Key takeaways from Viégas's talk:

- LLMs can build latent user models even when they refuse to tell users what they infer.
- Dashboard-style instrumentation can expose these internal inferences in real time.
- Hidden user models can alter outputs in biased and even factually incorrect ways.
- This matters for trust calibration because users may otherwise overtrust a system whose behavior is shaped by opaque assumptions about them.
- User-facing interpretability can also become a mechanism for control, not just observation.
- The talk broadens interpretability from a developer tool into a public interface question.
- It directly connects interpretability to fairness, privacy, and governance.

### 3. Hamed Hassani — Robust Policy Optimization to Prevent Catastrophic Forgetting

Hassani's keynote addresses a structural problem in post-training: each new round of alignment or specialization may erase previous capabilities.
For trustworthy agents, this is a major issue because safety, privacy, planning, and usefulness all need to coexist in one system.

Key takeaways from Hassani's talk:

- Modern models often undergo many successive post-training stages.
- That creates a continual-learning problem at the system level.
- Catastrophic forgetting is not just an optimization nuisance; it is a trust problem.
- A safe or capable system cannot be trusted if later tuning silently deletes earlier guarantees.
- The key challenge is to obtain multiple capabilities within one model without destructive interference.
- This is especially urgent for household robots and agentic systems that must satisfy several constraints simultaneously.
- The talk links robustness to continual learning rather than only to adversarial examples.

### 4. Nanyun (Violet) Peng — David and Goliath: Compute-Efficient Safety Interventions for LLMs

Peng's talk is one of the workshop's most concrete steering talks.
She argues that academia can still make meaningful safety contributions by finding interventions that do not require frontier-scale compute.
The two main examples in the transcript are MOE routing interventions and prompt-level control.

Key takeaways from Peng's talk:

- Safety remains unsolved despite larger and larger models.
- Compute-efficient interventions are therefore strategically important.
- In MOE models, some experts are more associated with safe or unsafe behavior than others.
- Steering router activations can shift behavior toward or away from safety.
- This exposes both an opportunity and a risk: efficient safety interventions can also be repurposed for jailbreaks.
- Similar ideas extend to multilingual behavior and prompt-level control.
- The broader implication is that trustworthy behavior may depend on controllable internal routing, not only on retraining.

### 5. Yan Liu — Actionable Interpretability through the Lenses of Feature Interaction

Liu's talk asks what interpretability is good for if it does not change downstream action.
Her answer is that feature interactions can provide a more faithful summary of model logic and support model compression, debugging, and even fairness analysis.

Key takeaways from Liu's talk:

- Interpretability without downstream action is limited.
- Feature interactions can capture richer structure than single-feature importance scores.
- Neural models can be mined for interaction sets that summarize higher-order relationships.
- These interaction sets can support white-box surrogates with strong predictive performance.
- The approach also helps with model debugging and fairness analysis.
- This is a compelling route from explanation to intervention.
- It is especially relevant to concept representation learning because interactions often correspond to domain-meaningful combinations rather than isolated variables.

## Themes & Takeaways

### Interpretability

Interpretability is the dominant theme, but the keynote lineup shows that it has multiple meanings.

- Van der Schaar wants interpretable trajectory and system representations.
- Viégas wants user-facing instrumentation of model inferences.
- Liu wants actionable structural summaries through feature interaction.
- Peng adds a routing-level perspective: interpretable experts can also be steerable experts.
- The workshop therefore suggests a stack of interpretability layers: semantic, user-facing, structural, and controllable.
- This is a much richer view than standard post hoc explanation alone.

### Human-AI feedback loops

Feedback loops appear in several forms.

- Viégas's dashboards make user reactions part of the transparency loop.
- Hassani's continual-learning framing implies that post-training itself is an iterative feedback process.
- Peng's safety interventions operate in response to observed failure modes and jailbreak behaviors.
- Van der Schaar's time-series work is aimed at decision support under intervention, which is a feedback setting in the broad sense.
- The workshop makes it clear that trust is produced through interaction and revision, not only through one-time certification.

### Uncertainty estimation

Uncertainty is one of the workshop's explicit pillars and also a recurring background assumption.

- Van der Schaar notes that forecasting plus uncertainty still falls short of genuine understanding.
- Safety in high-stakes domains requires knowing when the model is outside its reliable regime.
- Spotlight and poster papers cover quantized-model bias shifts, selective prediction, uncertainty-aware autonomous systems, and calibration.
- Peng's steering results imply uncertainty should also attach to which experts are active and why.
- The broader lesson is that uncertainty should inform both system outputs and control policies.

### Concept representation learning

Concept-level structure appears in several keynotes.

- Van der Schaar's motifs and compositions are concept-level representations of trajectories.
- Liu's feature interactions can be read as concept combinations learned by the model.
- Peng's expert analysis asks whether internal submodules line up with behavioral concepts.
- Viégas's user-model probes raise the question of what personal concepts a model builds internally.
- The workshop therefore pushes concept learning toward interpretability and intervention, not only benchmark gains.

### Causal inference

Causality is most explicit in van der Schaar's keynote but matters elsewhere too.

- Van der Schaar directly argues for understanding system dynamics and interventions.
- Liu's feature interactions help identify structured dependencies that can support better downstream reasoning.
- Viégas's dashboard examples show that changing internal assumptions about the user changes system outputs.
- Hassani's continual-learning problem is also causal in a training sense: which post-training stage caused which behavior loss?
- The workshop encourages causal thinking at both deployment time and training time.

### Robotics

Robotics is not the main keynote focus, but it is present in the workshop's design.

- The workshop description explicitly includes safe LLM agents, planning failures, and autonomous systems.
- Hassani uses household robots as a motivating example for why multiple capabilities must coexist.
- Several accepted papers address autonomous systems, harm recovery for computer-use agents, and multimodal safety.
- The takeaway for robotics is clear: trustworthy physical agents need interpretability, continual robustness, and intervention mechanisms at once.

### World models

World-model relevance is strongest through temporal and multimodal understanding.

- Van der Schaar's semantic dynamical-system modeling is world-model adjacent in the clearest sense.
- The workshop's multimodal-trust framing implies that many future systems will need internal models of time, state, and intervention.
- Trustworthy deployment therefore overlaps with the problem of building faithful predictive world models.
- This is an important bridge to interests in physical reasoning and structured latent dynamics.

### Steering techniques

Steering is one of the most actionable themes in the workshop.

- Peng provides routing-level and prompt-level interventions.
- Liu's actionable interpretability supports interventions on model form.
- Viégas's dashboards support user-facing control and auditing.
- Hassani's work suggests we need steering methods that do not destroy prior safety properties.
- The workshop overall treats steering as something that should be principled, inspectable, and robust over time.

## Connections to PAI Research

This workshop is especially valuable because it unifies many topics that often live apart.

### For the core agenda

- Interpretability: the workshop offers semantic, structural, and user-facing versions.
- Human-AI feedback loops: dashboards, post-training, and continual learning all appear as feedback systems.
- Uncertainty estimation: treated as necessary for deployment, not optional diagnostics.
- Concept representation learning: motifs, feature interactions, and routed experts all point toward concept-level control.
- Causal inference: central for time series, interventions, and training-stage analysis.

### For robotics, world models, and steering

- Hassani's household-robot framing makes trust a multi-capability systems problem.
- Van der Schaar's system understanding is a strong template for trustworthy world models.
- Peng's MOE interventions are directly relevant to steering work.
- Viégas's dashboards suggest a path for user-facing controls in embodied or agentic systems.
- Liu's feature interactions could support interpretable control and debugging in multimodal agents.

### Practical opportunities

- Build dashboards that expose both user models and system uncertainty.
- Study catastrophic forgetting as a safety regression problem.
- Use interaction-based explanations to support trustworthy local steering.
- Connect time-series causal representations to agentic world-model evaluation.
- Explore whether routed experts or interaction sets can become explicit intervention targets.

## Signals from Contributed Talks and Posters

The keynote themes were echoed strongly in the spotlight and poster program.
That broader program shows where the community currently sees the most urgent trust failures.

### Spotlight signals

- **LoRA Users Beware** highlights how small spurious correlations can dominate adapted models.
- **DLM-Scope** connects sparse autoencoders to interpretability for diffusion language models.
- **Uncertainty Drives Social Bias Changes in Quantized LLMs** links compression to bias and calibration drift.
- **Black-box Optimization of LLM Outputs by Asking for Directions** shows how attack signals can emerge even with minimal access.
- **Exact Certification against Label Poisoning** reinforces the workshop's formal-robustness thread.
- **Investigating Data Interventions for Subgroup Fairness** shows that distributional heuristics can fail at the subgroup level.
- **Test-Time Training Undermines Existing Safety Guardrails** is an especially sharp warning for adaptive-deployment settings.

### Poster-level signals worth tracking

- A large cluster of papers studies inference-time safety for LLMs, code models, and diffusion systems.
- Several contributions examine monitoring, sabotage detection, and long-context supervision failures in agentic settings.
- Watermarking, privacy collapse, and backdoor persistence all show up repeatedly, indicating that trustworthy AI is as much about infrastructure as about model quality.
- Concept bottlenecks, model diffing, and attribution methods suggest a strong continued appetite for mechanistic and structural explanations.
- Calibration and selective prediction remain prominent, especially in high-stakes or autonomous settings.
- The breadth of modalities in the poster list supports the workshop's central promise that trustworthiness should cut across language, vision, audio, and time series.

## Why this workshop matters now

- Frontier-model deployment is widening faster than agreement on what “trustworthy” should mean operationally.
- Inference-time interventions are becoming common, but their failure modes are not yet well characterized.
- User-facing transparency is still rare despite its obvious value for trust calibration.
- Continual post-training is making forgetting and safety regression more important than static benchmark snapshots suggest.
- The workshop provides a useful design-oriented alternative to treating trust as only a compliance or reporting issue.

## Reading the workshop as a whole

One way to read this workshop is as a blueprint for a layered trustworthy-AI stack.

- First, models need internal structure that can be interpreted or controlled.
- Second, they need interfaces that expose relevant state to developers and end users.
- Third, they need post-training procedures that preserve rather than erase critical properties.
- Fourth, they need monitoring and calibration for deployment under shift.
- Fifth, they need intervention mechanisms that are cheap enough to use in practice.
- The keynote lineup covers each of these layers from a different angle.
- That makes the workshop especially valuable as a synthesis point rather than just a collection of isolated techniques.
- It offers a coherent picture of what “trustworthy by design” might actually require.

## Open Questions

- What should trustworthy user-facing instrumentation look like for multimodal and agentic systems?
- How can we prevent post-training from erasing previously acquired safety properties?
- When do routed experts correspond to stable behavioral concepts rather than transient heuristics?
- How do we combine uncertainty estimation with actionable interpretability in a single interface?
- What is the right abstraction level for understanding high-stakes dynamical systems?
- Can interaction-based white-box models preserve enough fidelity for real deployment?
- How should causal reasoning and fairness analysis meet in modern foundation-model systems?
- What forms of steering remain reliable under continual adaptation?

## Sources

- [Workshop page](../../raw/iclr-2026-workshop-trustworthy-ai.md) — workshop description, keynote titles, spotlight list, and trustworthiness pillars.
- [Workshop recording capture](../../raw/iclr-2026-workshop-trustworthy-ai-talk/README.md) — metadata for the recorded livestream.
- [Workshop transcript](../../raw/iclr-2026-workshop-trustworthy-ai-talk/transcript.md) — opening remarks and keynote segments for Mihaela van der Schaar, Fernanda Viégas, Hamed Hassani, Violet Peng, and Yan Liu.
