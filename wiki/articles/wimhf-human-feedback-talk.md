---
title: "What's In My Human Feedback? — Summary"
type: "article"
tags: [iclr-2026, talk, interpretability, human-feedback, rlhf, sparse-autoencoders]
related: ["wiki/papers/whats-in-my-human-feedback.md", "wiki/summaries/iclr-2026-oral-session-2d-llms-evaluation.md", "wiki/concepts/mechanistic-interpretability.md", "wiki/concepts/value-alignment.md"]
sources: ["raw/wimhf-openreview.md", "wiki/papers/whats-in-my-human-feedback.md", "raw/iclr-2026-oral-session-2d-llms-evaluation.md"]
---

# What's In My Human Feedback?

## Overview

The WIMHF talk asks a question that much of post-training still leaves oddly underspecified: what exactly is encoded in
human preference data?

Across the [OpenReview capture](../../raw/wimhf-openreview.md), [paper summary](../papers/whats-in-my-human-
feedback.md), and [ICLR oral-session listing](../../raw/iclr-2026-oral-session-2d-llms-evaluation.md), the answer is
that preference datasets contain a surprisingly rich, structured, and sometimes unsafe mix of signals.

The authors propose WIMHF, a method that uses sparse autoencoders over embedding differences to discover a small set of
human-interpretable features explaining much of the preference prediction signal in seven datasets.

The method distinguishes between two things: what a dataset is capable of measuring, and what annotators actually
express.

That distinction is the heart of the work.

It makes human feedback legible not only as a training resource, but as an object of scientific analysis.

The oral-session abstract highlights several striking findings.

Different datasets encode very different tastes.

Reddit users may prefer informality and jokes.

HH-RLHF and PRISM annotators may dislike them.

LMArena users may systematically vote against refusals, even when that preference aligns with toxic content.

And because the discovered features are interpretable, they can be used for targeted data curation, yielding large
safety gains without hurting general performance.

This makes WIMHF one of the conference's clearest bridges between interpretability, concept representation learning,
steering, and human-AI feedback loops.

## Key Points

### Human feedback is powerful but poorly understood

The basic problem, stated consistently across the sources, is that human feedback can alter language models in
unpredictable and undesirable ways because practitioners do not know what the data are really encoding.

Standard preference pipelines treat the labels as a target, not as an object requiring interpretation.

WIMHF reverses that stance.

It treats feedback datasets as learned cultural artifacts whose internal structure can and should be analyzed.

### Sparse autoencoders make preference structure inspectable

The core technical idea is to train sparse autoencoders on embedding differences between preferred and dispreferred
responses.

The resulting features are then described in natural language, allowing researchers to map latent preference dimensions
to human-readable traits.

This is important because it turns preference modeling into a concept discovery problem.

Rather than pre-specifying a shortlist of attributes such as length or sycophancy, WIMHF tries to discover salient
features directly from the data.

That makes the method both more exploratory and more useful for auditing unknown failure modes.

### Measurable preferences and realized preferences are different

One of the paper's most useful conceptual distinctions is between what a dataset is capable of measuring and what
annotators actually choose.

A dataset may make certain distinctions visible in principle, but annotators may still prefer only a subset of them.

This matters because it separates the affordances of the data collection design from the values expressed by the
labelers.

That is a very helpful lens for anyone working on alignment.

A preference dataset is not just a mirror of human values.

It is a measurement instrument with its own constraints.

### A small set of features explains much of the signal

Across seven datasets, WIMHF finds that a relatively small number of interpretable features explains most of the
preference prediction signal achieved by black-box models.

That result is both optimistic and cautionary.

Optimistic, because it suggests human feedback may be more structured than it appears.

Cautionary, because if a small number of latent dimensions drive the labels, then small biases in those dimensions may
have outsized downstream impact.

### Preference varies sharply across datasets and populations

The oral-session abstract emphasizes dataset-level heterogeneity.

Users on Reddit may prefer informality and jokes.

Annotators in HH-RLHF or PRISM may disprefer them.

This is not just a colorful observation.

It is evidence that "human preference" is not a unitary object.

Different data collection contexts produce different value landscapes.

This aligns strongly with the Prolific talk and broader conference themes around whose preferences are actually being
optimized.

### WIMHF surfaces unsafe preferences directly

One of the talk's most practically important results is that the method uncovers potentially unsafe preferences, such as
LMArena users tending to vote against refusals, often in favor of toxic content.

This is valuable for two reasons.

First, it shows that preference data can encode harmful tendencies even when it looks benign at the aggregate level.

Second, it shows that interpretability can surface those tendencies before they are fully baked into post-trained
models.

### Interpretable features enable targeted data curation

The talk does not stop at analysis.

The authors use the discovered features for data curation.

In the Arena setting, relabeling harmful examples produces a reported 37% safety gain with no general performance cost.

That is a striking steering result.

Instead of only changing the reward model or policy objective, one can steer model behavior by cleaning the data using
interpretable feature structure.

### Personalization becomes more legible

The paper summary also notes that WIMHF supports fine-grained personalization by learning annotator-specific weights
over subjective features.

This is significant because personalization is often discussed as if it required opaque user embeddings or black-box
reward models.

WIMHF suggests a more interpretable route: represent users as differing mixtures over understandable preference
dimensions.

That creates a promising bridge between alignment and user-specific adaptation.

### The method is useful precisely because it is not purely mechanistic

Although sparse autoencoders are associated with mechanistic interpretability, WIMHF applies them to a very different
object: preference datasets.

The Area Chair meta-review explicitly describes this as a rare practical application of interpretability methods to
alignment.

That is part of what makes the talk stand out.

It shows that interpretability can be useful not only inside models, but in the datasets that shape them.

### The paper is careful about limitations

The OpenReview discussion also surfaces important caveats.

Feature descriptions are not unique.

Correlation is not causation.

Embedding choice matters.

The measurable features are not exhaustive.

And some datasets remain harder to explain than others.

These limitations do not weaken the practical contribution.

Instead, they locate the method correctly: as an interpretable audit tool, not a complete theory of human value.

## Connections to Research Interests

### Interpretability

WIMHF is explicitly an interpretability paper, but an unusually applied one.

It treats preference datasets as things that can be reverse-engineered into human-readable features.

That is interpretability aimed at the alignment stack.

### Human-AI feedback loops

Preference data are one of the most important human-to-model feedback channels in modern LLM training.

WIMHF analyzes what actually travels through that channel and how it can be cleaned or redirected.

### Uncertainty estimation

The work does not center uncertainty in the Bayesian sense, but it does expose ambiguity and heterogeneity in what
preference labels mean.

That is a form of epistemic uncertainty over the target itself.

### Concept representation learning

This is arguably the paper's central ML contribution.

It learns latent, interpretable preference concepts directly from data and shows that a small set can explain much of
the observed signal.

### Causal inference

The authors are careful not to equate discovered correlations with true causal human motives.

Still, their downstream relabeling results show that intervening on the data using the learned features can causally
improve safety outcomes.

### Robotics and world models

The direct robotics link is limited, but any embodied alignment system that learns from preference data could benefit
from interpretable preference features rather than opaque reward proxies.

### Steering techniques

WIMHF offers a concrete steering mechanism: use interpretable features to curate, filter, and personalize feedback
datasets before they shape model behavior.

## Takeaways

- WIMHF asks not just how to use human feedback, but how to understand what it contains.
- Sparse autoencoders recover interpretable preference features that explain much of the signal in seven datasets.
- The work reveals substantial variation across datasets, including potentially unsafe preferences.
- Those features are useful for steering: targeted relabeling can improve safety without hurting general performance.
- This talk is one of ICLR 2026's strongest examples of interpretability methods being applied directly to alignment
  data rather than only to model internals.
