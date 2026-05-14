---
title: "Workshop: World Models — Understanding, Modelling and Scaling — Key Takeaways"
type: "article"
tags:
  - iclr-2026
  - workshop
  - world-models
  - robotics
  - multimodal-learning
  - causal-reasoning
related:
  - "raw/iclr-2026-workshop-world-models.md"
  - "wiki/summaries/iclr-2026-workshop-world-models.md"
  - "wiki/concepts/world-models.md"
  - "wiki/concepts/stochastic-thermodynamics.md"
sources:
  - "raw/iclr-2026-workshop-world-models.md"
  - "raw/iclr-2026-workshop-world-models-talk/"
---

# Workshop: World Models — Understanding, Modelling and Scaling — Key Takeaways

## Overview

The [World Models workshop](../../raw/iclr-2026-workshop-world-models.md) is one of the clearest places in the repo where “world model” means more than generative prediction.
The workshop description ties world models to knowledge extraction, rigorous evaluation, multimodal scaling, control, reproducibility, safety, and causal reasoning.
That framing is important.
It signals that the field is moving from “can we generate plausible futures?” to “what kind of internal model helps an agent understand and act in the world?”

The transcript reinforces this shift.
Jürgen Schmidhuber argues for world models as reusable internal structures that agents should query rather than only roll out step by step.
Sarah Parisot focuses on interactive entertainment and creator tooling.
Sergey Levine grounds the conversation in robotics and autonomous data.
Later invited speakers, as listed on the workshop page, extend the day toward evaluation, multimodality, planning, and scale, even when the local source materials do not expose full titles.

What emerges is a field with two simultaneous pressures.
First, world models are becoming broader: they now touch video, language, robotics, active perception, and planning.
Second, they are becoming more accountable: researchers increasingly ask how these systems are evaluated, what abstractions they learn, and how they fail under intervention.
That makes this workshop especially relevant to interpretability, uncertainty, concept learning, causal inference, robotics, and steering.

### Program signal

- The workshop description explicitly names causal reasoning, multimodal scaling, and control.
- The morning transcript begins with a historical and architectural view of world models.
- Sarah Parisot's talk shows a creator-centered, interactive use case rather than a purely agentic one.
- Levine's robotics talk emphasizes autonomous data and real-world RL loops.
- The accepted papers and awards stress verification, embodied cognition, uncertainty-aware world models, and action-conditioned planning.
- The overall framing treats world models as infrastructure for intelligent behavior, not only as next-frame predictors.

## Key Invited Talks

### 1. Jürgen Schmidhuber — world models as promptable internal structures

The workshop page does not expose a formal title for Schmidhuber's talk, but the transcript provides a detailed throughline.
He traces world-model ideas from early recurrent networks and artificial curiosity to modern latent predictive architectures.
The central argument is that world models should not only support dense millisecond-by-millisecond simulation.
They should also become structured internal resources that controllers learn to query.

Key takeaways from Schmidhuber's segment:

- A world model should absorb as much raw experience as possible rather than prematurely discarding data.
- Predictive compression is useful because it extracts reusable regularities from high-dimensional streams.
- Prompting an internal world model may be more efficient than exhaustive low-level rollout planning.
- The controller's job is to learn which latent structures in the world model are worth addressing.
- Curiosity is naturally framed as searching for parts of the environment where prediction can still improve.
- Hierarchical planning should operate over abstractions and subgoals, not only over tiny action increments.
- This talk is unusually strong on concept representation learning: the world model's value lies in its internal abstractions.

### 2. Sarah Parisot — creator-centered interactive world models

Parisot gives one of the clearest concrete use cases for world models outside robotics.
Her focus is interactive entertainment and creative prototyping.
The key shift is from asking whether world models are on the path to AGI to asking whether they let creators quickly test ideas in interactive environments.

Key takeaways from Parisot's segment:

- World models can be useful as creative tools even when AGI is not the primary objective.
- Real-time interaction matters: next-token image generation is too slow for live prototyping.
- User studies with creative professionals surface three priorities: rapid prototyping, personalization, and creator control.
- Moving from the original WHAM model to real-time versions required architectural changes rather than just more data.
- Data collection can be deliberate and narrow; a hundred hours of targeted gameplay can outperform brute-force scale for some tasks.
- Fine-tuning with explicit control mechanisms allows new behaviors without retraining from scratch.
- This is a strong example of steering via interface and fine-tuning, not only via reward models.

### 3. Sergey Levine — robotic learning with autonomous data

Levine's talk appears in this workshop as well as the Lifelong Agents workshop, and it plays a similar role here.
It grounds the world-model conversation in physical interaction, autonomous data collection, and sample-efficient RL.

Key takeaways from Levine's segment:

- The richest test for world models may be the physical world rather than static digital tasks.
- Robot foundation models need post-training loops that go beyond imitation.
- RL specialists can generate high-quality data that later improves generalist models.
- A useful world model is one that supports policy improvement under realistic data budgets.
- Real deployment requires algorithms that are simple and sample-efficient enough to run in situ.
- This view emphasizes action-conditioned understanding over passive prediction.
- It also keeps robotics tied to lifelong learning, intervention, and human correction.

### 4. Mahmoud Assran — predictive world-model pretraining and collapse

The workshop page lists Assran as an invited speaker but does not expose a local abstract or title.
Within the workshop's surrounding paper list, however, issues like JEPA-style architectures, collapse in predictive pretraining, and representation quality are prominent.
Assran's slot clearly fits this thread.

Useful workshop-level takeaways from this slot:

- Predictive world-model pretraining is becoming a representational learning problem as much as a planning problem.
- Collapse prevention and stable predictive representations remain unresolved.
- The field is still negotiating how much abstraction is useful before the model loses control-relevant detail.
- This directly matters for concept representation learning and interpretability.

### 5. Michael Rabbat — evaluation and planning in learned environments

Rabbat's public local slot likewise lacks a visible title, but the workshop's contributed talks and panel themes make the role of this part of the program clear.
It connects learned predictive representations to actual planning and evaluation.

Key workshop-level takeaways:

- World models should be judged by the quality of downstream planning they support.
- Learned representations need to support compositional reasoning, not only perceptual fidelity.
- Benchmarking and software infrastructure are becoming first-class concerns in world-model research.
- This contributes to the workshop's push for rigorous evaluation and reproducibility.

### 6. Jiajun Wu — embodied cognition and structured world understanding

Wu's slot is well aligned with the workshop's own paper lineup, especially ENACT and embodied world-model benchmarks.
Even without a title in the local page, the surrounding workshop material makes the emphasis legible.

Key workshop-level takeaways:

- Embodied cognition is a strong stress test for whether a model genuinely represents action-conditioned state change.
- Egocentric interaction exposes weaknesses that static VLM benchmarks often hide.
- World models need to capture not only object appearance but how actions reorganize the scene.
- This is especially relevant to robotics and concept representation at the action level.

### 7. Kevin Murphy — probabilistic structure, uncertainty, and modular reasoning

Murphy's presence in the workshop fits its explicit interest in rigorous evaluation, scaling, and causal coherence.
While the local source does not provide the title, the workshop materials repeatedly highlight verification, uncertainty, and planning.

Key workshop-level takeaways:

- Probabilistic and modular views of world models remain crucial even in the age of giant generative systems.
- Uncertainty estimates matter when a world model is used for planning rather than only for generation.
- Structured latent spaces are likely to matter for safe decision-making.
- This is a natural bridge between world models and uncertainty-aware control.

### 8. Shane Gu — scalable multimodal world models and safety

The workshop's later schedule and panel structure suggest a growing concern with aligning large multimodal world models to useable goals.
Gu's slot likely played into that systems-scale perspective.

Key workshop-level takeaways:

- Scaling world models raises safety, controllability, and evaluation problems at the same time.
- Multimodal integration is useful only if the system can coordinate evidence across sensors.
- Steering world models may require interventions at training time, inference time, and planning time.
- The workshop increasingly treats these as one integrated problem.

### 9. Hao Su — embodied control, planning, and physical grounding

Su's slot rounds out the workshop with a strong embodied-control orientation.
That is consistent with the accepted-paper list, which includes manipulation, planning, latent action models, and RL with learned models.

Key workshop-level takeaways:

- Physical grounding remains one of the hardest tests of whether a world model is actionable.
- Good video prediction is not enough; the model must support control decisions.
- Spatial reasoning, latent action abstraction, and long-horizon planning all matter.
- This is another strong connection point to robotics and world-model research.

## Themes & Takeaways

### Interpretability

Interpretability in this workshop is mostly about usable abstractions.

- Schmidhuber explicitly argues for latent structures that controllers can query.
- Parisot cares about creator control, persistency of edits, and understandable behavior.
- Predictive representation learning work in the workshop materials repeatedly asks what the model has actually encoded.
- Embodied benchmarks like ENACT are interpretability probes in disguise: they test whether the model's internal world is action-sensitive.
- The workshop therefore pushes toward structural interpretability rather than surface explanation.

### Human-AI feedback loops

Human feedback appears in data collection, creator tooling, and robotics.

- Parisot's work starts from interviews with creative professionals.
- Creators define what makes an interactive world model useful.
- Levine's robotics framing uses human intervention and autonomous data together.
- Workshop papers on action verification and self-improving world models suggest further loops between prediction and correction.
- The field seems to be moving toward interactive evaluation rather than static offline metrics alone.

### Uncertainty estimation

Uncertainty is central even when it is not always foregrounded.

- The accepted papers include uncertainty-aware robotic world models and evidential latent world models.
- Murphy's slot fits the workshop's explicit interest in rigorous evaluation and reliability.
- Planning with world models is unsafe if uncertainty is ignored.
- Robotics especially needs uncertainty to determine when simulated futures can be trusted.
- This suggests that uncertainty estimation should be treated as part of the world-model interface to planners.

### Concept representation learning

This is arguably the workshop's deepest shared theme.

- Schmidhuber frames the problem as learning useful latent abstractions from raw streams.
- Parisot needs representations that preserve interaction mechanics while allowing editing and control.
- Assran-style predictive pretraining questions are about what representations emerge and when they collapse.
- ENACT-like work asks whether models represent actions and consequences in a reusable form.
- Hierarchical latent actions and predictive representations in the paper list push the same direction.
- World models increasingly live or die on whether they learn the right concepts, not only high-fidelity outputs.

### Causal inference

This workshop comes closest to making causal language operational.

- The description explicitly includes causal reasoning.
- Levine and Wu frame the problem through action-conditioned state change.
- Several accepted papers deal with counterfactual simulation, causal spatial reasoning, and intervention-aware planning.
- Parisot's creator use case also depends on the model responding correctly to edits and interventions.
- The common thread is that a world model should support “what happens if I do this?” rather than only “what usually happens next?”

### Robotics

Robotics is central rather than peripheral.

- Levine and Su anchor the embodied-control side of the program.
- Many accepted papers focus on manipulation, robot planning, and adaptation from simulation to reality.
- Robotics forces the field to care about uncertainty, sample efficiency, and control relevance.
- It also turns evaluation from visual plausibility into action success.
- The workshop strongly suggests that robotics remains one of the best stress tests for world-model usefulness.

### World models

The workshop's own topic is also the most plural.

- For Schmidhuber, world models are reusable predictive computers with rich latent structure.
- For Parisot, they are interactive generative engines for creative worlds.
- For Levine, they are part of an RL and data-collection loop.
- For the accepted papers, they include action models, video models, latent predictors, and verification systems.
- The field still lacks a single settled definition, but the workshop suggests a pragmatic one: a world model is whatever supports understanding and action in a structured environment.

### Steering techniques

Steering appears through prompts, edits, routing, and planning.

- Parisot explicitly studies text-triggered behavior changes and parameter-efficient fine-tuning.
- Schmidhuber's controller-as-prompt-engineer is a steering story at the architectural level.
- Robotics uses reward design and intervention as steering tools.
- Safety and controllability concerns in the broader schedule imply that inference-time steering will matter for large multimodal systems too.
- The takeaway is that world models need steerable abstractions rather than only unconstrained imagination.

## Connections to PAI Research

This workshop is almost a direct map onto the requested research interests.

### Core relevance

- Interpretability becomes the study of learned abstractions and control-relevant representations.
- Human-AI feedback loops appear in creator tooling, robotics, and self-improving predictive systems.
- Uncertainty estimation is necessary for planning and safe deployment.
- Concept representation learning is the center of the field, not an auxiliary topic.
- Causal inference enters through action-conditioned prediction and counterfactual simulation.

### Relevance for robotics, world models, and steering

- Levine and Su make robotics a primary application domain.
- Parisot shows that world models can matter for human-centered creativity, not only agent autonomy.
- The accepted-paper list suggests a strong future in verification, latent action abstraction, and embodied evaluation.
- Steering problems appear both in creator-facing controls and in planner-facing interfaces.
- Work that connects representations, planning, and interaction should fit naturally into this ecosystem.

### Practical opportunities

- Study when latent abstractions help planners versus hiding useful detail.
- Build interfaces that let humans inspect and edit world-model beliefs.
- Treat uncertainty as a first-class output of a world model.
- Create embodied evaluations that stress action-conditioned understanding rather than only video realism.
- Explore concept-level steering methods that operate on latent dynamics rather than only output prompts.

## Signals from Contributed Talks and Posters

The invited talks are strengthened by an unusually coherent contributed program.
The paper list makes clear which problems are turning into standard tests for the field.

### Contributed talks and award papers

- **World Action Verifier** connects forward and inverse consistency to self-improving world models.
- **ENACT** emphasizes embodied cognition and egocentric world modeling rather than static scene understanding.
- **A Lightweight Library for Energy-Based JEPAs** shows that tooling and infrastructure now matter for reproducible experimentation.
- Award papers such as **World Action Models are Zero-shot Policies** reinforce the planning-and-control orientation of the workshop.

### Poster-level signals

- Multiple papers study uncertainty-aware or evidential world models, showing that confidence estimation is becoming a standard expectation.
- Several contributions focus on hierarchical world models, latent actions, or jumpy planning, which all point toward abstraction as the main scalability mechanism.
- A recurring theme is grounding video generation in executable plans, not only in visual plausibility.
- Causal language appears often in paper titles, especially around spatial reasoning, counterfactual simulation, and intervention-aware learning.
- There is also a strong robotics cluster: manipulation, navigation, simulation-to-real transfer, and offline RL with world models.
- The program therefore supports the workshop's claim that world models are becoming system-level infrastructures rather than isolated model families.

## Open Questions

- What is the right abstraction level for a useful world model in robotics?
- How can we evaluate whether a world model supports causal reasoning instead of only next-state prediction?
- When do creator-facing controls generalize to agent-facing controls?
- What is the best way to expose uncertainty to downstream planners?
- How should world models trade off fidelity, abstraction, and controllability?
- Can one learned model support both creative editing and reliable decision-making?
- How do we prevent predictive-pretraining collapse while preserving useful latent structure?
- What benchmarks best distinguish world understanding from surface video imitation?
- How should world models be steered when they are integrated with powerful generalist agents?

## Sources

- [Workshop page](../../raw/iclr-2026-workshop-world-models.md) — workshop framing, invited speakers, paper list, and high-level themes.
- [Workshop recording capture](../../raw/iclr-2026-workshop-world-models-talk/README.md) — metadata for the recorded livestream.
- [Workshop transcript](../../raw/iclr-2026-workshop-world-models-talk/transcript.md) — Jürgen Schmidhuber, Sarah Parisot, and Sergey Levine segments used as primary evidence in this synthesis.
