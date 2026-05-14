---
title: "Percy Liang on Open Development — Summary"
type: "article"
tags: [iclr-2026, keynote, open-development, frontier-ai, scaling-laws, human-ai-feedback-loops]
related: ["wiki/articles/marin-open-development-frontier-ai.md", "wiki/concepts/marin-project.md", "wiki/concepts/open-source-ai.md", "wiki/concepts/neural-scaling-laws.md"]
sources: ["raw/iclr-2026-schedule-day3-sat.md", "raw/iclr-2026-invited-talk-marin-open-development-frontier-ai-talk/"]
---

# Percy Liang on Open Development

## Overview

Percy Liang's keynote, listed on [ICLR's day-3 schedule](../../raw/iclr-2026-schedule-day3-sat.md) as "Marin: Open
Development of Frontier AI," argues that the central scarcity in frontier AI is no longer just compute.

It is scientific visibility.

Capabilities are rising, but openness is falling.

The public, and often even the broader research community, knows less and less about how powerful models are trained,
what experiments were tried, and why particular design decisions were made.

Liang's proposed response is Marin: a model-development process conducted in the open, with experiments, failures,
suggestions, and reviews happening publicly through GitHub.

The schedule abstract frames this as a better way of doing science, one that improves on preregistration,
reproducibility, and peer review.

The longer existing synthesis in [the Marin article](./marin-open-development-frontier-ai.md) and the linked raw keynote
materials make clear that Liang's talk also includes substantive technical results on optimizers, scaling laws, and
recipe design.

But the deepest idea in the keynote is organizational.

Open development is presented as a way to create tighter, more legible, and more cumulative human-AI research loops.

That makes the talk especially relevant to interpretability, steering, uncertainty, and feedback-oriented research
cultures.

## Key Points

### Capabilities are increasing while openness is decreasing

The schedule abstract begins with a stark contrast: as AI capabilities skyrocket, openness plummets.

That single sentence sets up the keynote's main concern.

Even open-weight models often hide the process that produced them.

Training data curation, optimizer choices, failed runs, middleware patches, and scaling decisions remain invisible.

Liang treats this as a scientific problem, not only a governance problem.

When the process is hidden, research becomes harder to reproduce, critique, and improve collaboratively.

### Marin treats frontier AI as an open process, not a closed artifact

The central proposal is that every experiment should be done in the open and that outsiders should be able to suggest,
review, and even run experiments through GitHub.

This is more ambitious than simply releasing weights or code at the end.

It relocates openness from the output to the workflow.

That matters because the workflow is where most of the real knowledge lives: which runs failed, which hypotheses were
rejected, which stabilizers mattered, and which small-scale results really transferred.

Liang is effectively arguing that frontier model development should look more like open-source software engineering and
less like sealed industrial R&D.

### Better science requires predictability, not just heroics

The existing Marin article emphasizes Liang's distinction between ad hoc "YOLO" runs and principled scaling recipes.

That distinction is already latent in the schedule abstract, which highlights new optimizers and scaling laws as outputs
of the Marin process.

The idea is that serious science needs predictability.

A scaling recipe is not just a configuration.

It is a function from compute budget to hyperparameter choices.

If that function is stable, small experiments can meaningfully forecast what will happen at much larger scale.

This is a major connection to uncertainty estimation.

Liang is not merely asking for bigger models.

He is asking for forecasts about training behavior that can be checked publicly.

### Preregistration becomes practical when the recipe is sound

One of the most original parts of the broader Marin story is the use of public preregistration of expected losses before
large runs complete.

Why is that significant?

Because it converts scaling-law claims from post hoc storytelling into falsifiable predictions.

In the context of the keynote, preregistration is not bureaucratic overhead.

It is a scientific stress test for whether a recipe is actually reliable.

That makes open development a powerful human-AI feedback loop.

The community can inspect the prediction, watch the run, and update its beliefs based on the outcome.

### Open development changes who can participate in frontier research

Liang's process argument is also an inclusion argument.

If experiments are visible and contribution pathways are public, then researchers outside the most compute-rich
institutions can still engage with frontier model development in a meaningful way.

They may not own the largest clusters, but they can analyze curves, suggest interventions, review methods, run smaller
tests, and contribute to the design of scaling recipes.

That is not full democratization, but it is a real shift in the feedback structure of the field.

### The talk links meta-science to concrete technical progress

A potential criticism of open-development rhetoric is that it could sound merely procedural.

Liang avoids that by grounding the argument in technical outputs: new optimizers, validated scaling laws, and open
experimental records.

The schedule abstract explicitly mentions these scientific results.

The existing Marin synthesis adds concrete details such as hyperball, QK norm, small-to-large extrapolation, and public
loss predictions.

The resulting message is that better process is not separate from better algorithms.

It is one route to them.

### Open development is a steering mechanism for the field itself

The keynote can also be read as an intervention on research culture.

By changing what gets recorded, who gets to comment, and how predictions are exposed, open development steers the
priorities of a project.

It rewards legibility, forecasting discipline, and community review.

That may produce different choices about data, architecture, and evaluation than a sealed development pipeline would.

In that sense, Liang is proposing a steering technique not for a single model, but for the social system that builds
models.

### Marin is a model of cumulative human-AI collaboration

At a deeper level, the keynote suggests that frontier AI development should itself be treated as a human-AI
collaborative system.

Humans generate hypotheses, runs produce traces, scaling laws summarize regularities, and future humans act on those
regularities.

The "model" is not the only learner.

The project learns too.

Open development makes that project-level learning legible.

## Connections to Research Interests

### Interpretability

Liang's argument is interpretability-adjacent in a broad sense.

He is asking for interpretability of the development process: why the model ended up the way it did, which experiments
mattered, and what scaling evidence supports current beliefs.

That complements mechanistic interpretability rather than replacing it.

### Human-AI feedback loops

This is the keynote's strongest connection.

Open development creates explicit loops among contributors, runs, predictions, and postmortems.

The point is to make those loops faster, public, and cumulative.

### Uncertainty estimation

Public scaling predictions, preregistered losses, and recipe validation are all forms of uncertainty management.

The keynote is about making uncertainty visible early, when it can still shape experimental design.

### Concept representation learning

Liang's work on scaling recipes also implies learning higher-level concepts for training dynamics: what counts as a
stable recipe, what patterns transfer across scale, and which optimizer behaviors are genuinely robust.

Those are meta-level concepts about model development itself.

### Causal inference

Open experimental records improve causal reasoning about training outcomes.

If every intervention and failure is logged, it becomes easier to ask which changes actually improved stability or
efficiency.

### Robotics and world models

The robotics link is indirect, but the world-model connection is strong.

Scaling recipes and predictive training laws are a kind of model of the training world: a structured account of how
interventions propagate across scale.

### Steering techniques

Open development is a governance and research steering technique.

It changes incentives, visibility, and contribution pathways, which in turn change what systems get built and how.

## Takeaways

- Liang's keynote treats openness as a scientific bottleneck, not just a policy preference.
- Marin is presented as an open-development workflow in which experiments and scientific reasoning are exposed in real
  time.
- The technical story about optimizers and scaling laws supports, rather than distracts from, the meta-scientific
  argument.
- Public prediction and preregistration are central tools for making frontier AI more legible and falsifiable.
- For researchers interested in steering, uncertainty, and human-AI feedback loops, Liang's proposal is one of the
  conference's clearest process-level agendas.
