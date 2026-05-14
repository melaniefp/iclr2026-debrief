---
title: "World Models"
type: "concept"
tags: [world-models, planning, robotics, multimodal-learning]
related:
  - "wiki/summaries/iclr-2026-workshop-world-models.md"
  - "wiki/summaries/iclr-2026-workshop-lifelong-agents.md"
  - "wiki/articles/world-models-workshop.md"
  - "wiki/articles/lifelong-agents-workshop.md"
  - "wiki/concepts/human-robot-interaction.md"
  - "wiki/concepts/uncertainty-in-llms.md"
  - "wiki/concepts/socially-assistive-robotics.md"
sources:
  - "raw/iclr-2026-workshop-world-models.md"
  - "raw/iclr-2026-workshop-world-models-talk/README.md"
  - "raw/iclr-2026-workshop-world-models-talk/transcript.md"
---

# World Models

## Definition

World models are learned internal models of environment dynamics that support
prediction, planning, and control. In modern ML they can be video predictors,
latent transition systems, action-conditioned simulators, or multimodal models
that compress the structure of an environment into reusable internal state.

The ICLR 2026 [World Models workshop article](../articles/world-models-workshop.md)
shows a field moving beyond “next-frame generation” toward a broader question:
what kind of representation helps an agent understand and act in the world?
Across invited talks and papers, world models were tied to robotics, creator
control, causal reasoning, uncertainty, and hierarchical abstraction.

This concept therefore sits close to embodied AI. It links predictive modeling to
planning, user steering, and evaluation under intervention rather than only to
sample quality.

## Key Ideas

- **Predictive compression creates reusable structure**: good world models distill
  regularities from high-dimensional streams into latent abstractions.
- **Action conditioning is central**: the key question is often “what happens if
  I do this?” rather than just “what comes next?”
- **Abstraction is a feature, not a bug**: planners often need latent summaries,
  subgoals, and controllable factors rather than pixel-perfect futures.
- **Embodiment is a stress test**: robotics exposes failures that can be hidden in
  offline video or language generation benchmarks.
- **Uncertainty must be exposed**: planning with a world model is unsafe if the
  system cannot represent when its imagined futures are unreliable.
- **Steering matters at multiple levels**: prompts, fine-tuning, latent actions,
  and controller interfaces all shape how a world model is used.

## Related Work at ICLR 2026

- [Workshop: World Models — Understanding, Modelling and Scaling](../articles/world-models-workshop.md)
  synthesizes the workshop's emphasis on abstraction, planning, uncertainty, and
  multimodal scale.
- The raw [World Models workshop page](../../raw/iclr-2026-workshop-world-models.md)
  explicitly connects world models to evaluation, safety, causal reasoning, and
  control.
- The [workshop transcript](../../raw/iclr-2026-workshop-world-models-talk/transcript.md)
  highlights Jürgen Schmidhuber on queryable internal structures, Sarah Parisot
  on creator-centered interaction, and Sergey Levine on autonomous robotic data.
- [Workshop: Lifelong Agents — Key Takeaways](../articles/lifelong-agents-workshop.md)
  reinforces the link between memory, continual learning, and action-conditioned
  reasoning in agents.

## Open Questions

- What is the right abstraction level for a useful world model in robotics or
  long-horizon agents?
- How should world models expose uncertainty to downstream planners and users?
- Which evaluations best distinguish genuine world understanding from plausible
  but non-actionable generation?
- Can one model support both human-centered creative control and reliable
  autonomous planning?
