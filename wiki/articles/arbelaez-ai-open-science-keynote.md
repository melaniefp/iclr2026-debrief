---
title: "Pablo Arbeláez on AI for Open Science — Summary"
type: "article"
tags: [iclr-2026, keynote, ai-for-science, open-science, robotic-surgery, drug-discovery]
related: []
sources: ["raw/iclr-2026-schedule-day3-sat.md"]
---

# Pablo Arbeláez on AI for Open Science

## Overview

Pablo Arbeláez's keynote is programmatic rather than narrowly technical, and that is part of its value.

In the short abstract on [ICLR's day-3 schedule](../../raw/iclr-2026-schedule-day3-sat.md), Arbeláez describes ongoing
work at CinfonIA, the Center for AI at Universidad de los Andes, on "Artificial Intelligence for Open Science."

The examples are deliberately broad: robotic surgery, spatial transcriptomics, drug discovery, geology, and nature
conservation.

Even with only a compact abstract, a clear research agenda emerges.

Arbeláez is advocating for AI systems that do not live inside a single product vertical or benchmark silo.

Instead, AI becomes shared scientific infrastructure across multiple domains where data are multimodal, experiments are
expensive, and downstream decisions have real material consequences.

That makes this keynote especially relevant to research interests that cut across fields.

The talk sits at the intersection of robotics, scientific world models, causal reasoning, uncertainty estimation, and
human-AI collaboration.

It also places unusual emphasis on openness.

Open science is not just about releasing papers.

It is about making tools, data, methods, and collaborative workflows usable across institutional and geographic
boundaries.

That is a strong framing for a conference talk, especially from a center positioned as the first AI-focused academic hub
in Latin America.

## Key Points

### AI is being presented as scientific infrastructure

The talk's first striking feature is its breadth.

Robotic surgery, spatial transcriptomics, drug discovery, geology, and conservation are not naturally adjacent benchmark
categories.

What binds them together is a common workflow structure.

Each domain requires integrating heterogeneous measurements, learning from limited or costly labels, and helping human
experts reason over complex systems.

That suggests Arbeláez is presenting AI less as a monolithic solver and more as shared scientific infrastructure.

This matters for ML because it pushes the field away from single-task thinking.

A useful scientific system often has to support search, annotation, hypothesis generation, uncertainty communication,
and decision support all at once.

### Open science is about collaboration loops, not only access

The phrase "AI for Open Science" signals more than public availability.

It implies collaborative scientific loops in which models, experimentalists, and domain experts continually update one
another.

A biologist uses a model to prioritize measurements.

Those measurements create new data.

The updated data reshape the model.

A surgeon tests a robotic workflow, finds a failure mode, and the learning system changes accordingly.

That is a human-AI feedback loop with unusually concrete stakes.

In this framing, open science requires that these loops remain inspectable and transferable.

If the loop is locked inside a proprietary system, science becomes less cumulative.

### Robotic surgery foregrounds embodied decision support

Among the example domains, robotic surgery is the most obvious connection to robotics.

Even from the abstract alone, its inclusion suggests a focus on embodied AI that must operate in tight interaction with
human expertise, physical constraints, and safety-critical uncertainty.

Robotic surgery is not just motor control.

It is perception, assistance, planning, annotation, and trust calibration.

That makes it a good example of how scientific AI and embodied AI can converge.

A surgical model may need to segment tissue, predict safe trajectories, flag uncertainty, and communicate
recommendations to a clinician who retains ultimate authority.

### Spatial transcriptomics highlights multimodal representation learning

Spatial transcriptomics is a canonical modern AI-for-science problem because it requires integrating molecular
measurements with spatial structure.

Even though the abstract provides no methodological details, its inclusion is revealing.

This is the kind of domain where concept representation learning matters: models must discover meaningful latent
organization in biological tissue while respecting measurement geometry and biological context.

It is also the kind of domain where interpretability matters by necessity.

Researchers do not just want predictive accuracy.

They want representations that support biological explanation, comparison, and experimental follow-up.

### Drug discovery is an uncertainty management problem

Drug discovery appears in many AI-for-science roadmaps, but in the context of this keynote it likely serves a specific
function.

Drug pipelines are full of sparse supervision, expensive experiments, and cascading uncertainty.

Models propose candidates, experiments reject most of them, and the whole loop depends on prioritization under
uncertainty.

That is important because it clarifies what "scientific usefulness" means.

A system does not need to solve chemistry end to end.

It needs to be useful enough to improve the sequence of expert decisions.

That again reinforces the keynote's emphasis on open, collaborative, iterative science.

### Geology and conservation widen the scope of AI for science

The inclusion of geology and nature conservation makes the keynote broader than standard laboratory science.

These are domains where causal structure is messy, measurements are often incomplete, and interventions unfold over long
timescales.

They also highlight that AI for open science is not only about accelerating already well-funded experimental pipelines.

It is also about making modeling and decision support available in settings where resources, compute, and data
collection may be unevenly distributed.

This is where the keynote's institutional context matters.

An open-science framing from Latin America implicitly broadens the geography of who gets to build and benefit from
frontier scientific AI.

### CinfonIA is positioned as a coordination hub

Arbeláez's bio notes that CinfonIA is the first AI-focused academic center in Latin America.

That institutional fact helps explain the keynote's design.

The talk is not just a list of applications.

It is a statement about how centers can coordinate interdisciplinary work across medicine, biology, Earth science, and
conservation.

In other words, open science here also means open coordination: a place where tooling, expertise, and shared methodology
can circulate between fields.

### The keynote implicitly argues for domain-grounded world models

Across all of the example domains, the recurring need is a model of hidden structure that links measurements to the
underlying system being studied.

In robotic surgery, it may be anatomy, instrument state, and procedure context.

In transcriptomics, it may be cell states arranged in space.

In geology, it may be subsurface structure inferred from indirect signals.

In conservation, it may be ecological dynamics inferred from sparse observations.

That is essentially a family of domain-specific world models.

The keynote's unifying idea is that AI can help construct and update those models in collaboration with experts.

## Connections to Research Interests

### Interpretability

Open science is hard to reconcile with opaque systems.

If a model is meant to support biology, medicine, or conservation, its outputs must be communicable to domain experts.

Arbeláez's cross-domain framing strongly suggests interpretability as a practical requirement, not a post hoc add-on.

### Human-AI feedback loops

This keynote is saturated with feedback loops.

Scientists define questions, models prioritize possibilities, experiments return evidence, and human judgment updates
the next round.

That cycle is the real engine of progress in most of the example domains.

### Uncertainty estimation

Every listed application features costly, partial, or noisy evidence.

A strong AI-for-science system therefore needs to distinguish high-confidence signals from exploratory suggestions.

Uncertainty is central to triage, resource allocation, and safe decision support.

### Concept representation learning

The domains in the abstract all require meaningful latent concepts: cell neighborhoods, surgical states, chemical
properties, geological structures, and ecological patterns.

Learning those concepts in forms experts can reuse is a core shared challenge.

### Causal inference

Open science is about explanation and intervention, not just prediction.

Drug discovery, conservation, and surgery all demand some account of what causes what and which interventions will
matter.

That places causal reasoning near the center of the agenda.

### Robotics and world models

Robotic surgery anchors the keynote in embodied, safety-critical robotics, while the broader scientific examples suggest
a generalized world-modeling perspective across domains.

The common task is inferring latent structure from imperfect observations and using it to guide action.

### Steering techniques

The steering angle here is methodological rather than prompt-based.

Datasets, interfaces, expert constraints, and open workflows all steer model behavior toward scientifically usable
outputs.

The keynote suggests that the most important steering variables in science may be institutional and procedural.

## Takeaways

- Arbeláez presents AI for open science as a cross-domain infrastructure project rather than a collection of
  disconnected demos.
- The example domains all share a need for multimodal learning, uncertainty-aware inference, and expert-centered
  feedback loops.
- Robotic surgery gives the agenda a concrete embodied dimension, while transcriptomics, drug discovery, geology, and
  conservation expand the scientific scope.
- The talk points toward domain-grounded world models that remain useful to human experts.
- Even from a short abstract, the keynote reads as a persuasive argument for open, interdisciplinary, globally
  distributed AI for science.
