---
title: "Maja Matarić on Human-Centered Robotics — Summary"
type: "article"
tags: [iclr-2026, keynote, robotics, human-centered-ai, socially-assistive-robotics, affective-computing]
related: ["wiki/concepts/socially-assistive-robotics.md", "wiki/concepts/human-robot-interaction.md", "wiki/concepts/affective-computing.md", "wiki/summaries/challenges-human-centered-ai-robotics.md"]
sources: ["raw/iclr-2026-schedule-day1-thu.md", "raw/challenges-human-centered-ai-robotics-talk/README.md"]
---

# Maja Matarić on Human-Centered Robotics

## Overview

Maja Matarić's keynote argues that the next phase of AI will not be won by adding mobility to existing models alone.

It will depend on whether we can build systems that understand people as changing, embodied, socially situated agents.

Her central claim is simple.

Physical AI is not ready for everyday life if human-robot interaction is treated as an afterthought.

In the conference schedule abstract, [ICLR's day-1 program](../../raw/iclr-2026-schedule-day1-thu.md) frames the problem
as a gap between what users expect from intelligent machines and what current robotics systems can actually deliver.

Users want machines that can understand moods, anticipate needs, adapt over months, and respond to subtle multimodal
signals.

Matarić's talk argues that these capabilities do not emerge automatically from better locomotion or manipulation.

They require long-term user modeling, real-time multimodal behavioral processing, and affective computing woven directly
into robot design.

The longer transcript in [the captured keynote materials](../../raw/challenges-human-centered-ai-robotics-
talk/README.md) makes the same point more sharply.

Matarić presents socially assistive robotics as a field built around augmentation rather than replacement: robots should
help people help themselves.

That framing matters for healthcare, education, therapy, and aging, but it also matters for frontier AI more broadly.

If future systems are meant to operate in homes, clinics, schools, and workplaces, then the decisive bottleneck may be
neither raw reasoning nor motor control.

It may be the quality of the human-AI feedback loop.

## Key Points

### Human intelligence is embodied and socio-emotional

Matarić repeatedly contrasts current AI with the conditions under which human intelligence evolved.

Humans are not just disembodied predictors.

They are embodied, situated, and fundamentally social.

In the transcript, she argues that the field now understands the importance of embodiment, but still underestimates the
socio-emotional dimension.

That omission is not cosmetic.

Her view is that social and emotional structure helped drive human intelligence itself.

If that is right, then systems that ignore socio-emotional grounding may remain narrow, even when their language or
planning abilities look impressive.

This is one of the talk's strongest links to robotics and world models.

A useful world model for a household or clinical robot cannot just encode objects, geometry, and actions.

It must also model expectations, comfort, trust, fatigue, attention, and motivation.

### Socially assistive robotics is about augmentation, not replacement

Matarić defines socially assistive robotics as a way of changing human behavior through social interaction rather than
physical substitution.

The robot is not there to do the exercise, therapy, or self-regulation for the user.

It is there to coach, motivate, and scaffold the user into doing it.

That distinction separates her program from much of the automation discourse.

She explicitly warns that many current technologies are oriented toward replacement rather than augmentation.

Her lab's work instead assumes that the most valuable AI systems will often be those that preserve human agency while
improving adherence, engagement, and consistency.

The schedule abstract reinforces this point when it emphasizes support across ages, abilities, contexts, and deployment
durations extending up to six months.

That is a very different design target from benchmark-driven chatbot success.

It assumes long-horizon interaction, personal adaptation, and durable relationships.

### Information alone rarely changes behavior

One of the keynote's clearest arguments is that self-knowledge and monitoring do not reliably translate into action.

Matarić contrasts simple "quantified self" feedback with systems that can actually influence motivation.

Her point is not anti-measurement.

It is that behavioral change usually depends on socio-emotional support, not just more dashboards.

This is crucial for any research agenda centered on human-AI feedback loops.

A model can explain, measure, and remind, but still fail to change outcomes if it does not intervene at the level of
motivation.

For researchers working on alignment or preference learning, this is a useful inversion.

Instead of asking only how humans shape model behavior, Matarić asks how machines shape human behavior.

That reciprocal loop is where many real deployment risks and benefits live.

### Real-time multimodal understanding remains hard

The keynote is also notable for its skepticism about generic, one-size-fits-all models for behavioral understanding.

Matarić argues that real-time affect recognition, intent inference, and user understanding remain difficult, especially
in personal and clinical settings.

In the transcript, she says current foundation models are still poor at tasks such as personalized affect recognition.

Specialized deep models often do better.

That claim matters because the talk is not nostalgic for pre-foundation-model methods.

It is diagnostic.

Behavioral data are sparse, noisy, heterogeneous, non-stationary, and deeply personalized.

Those are exactly the settings where average-case scaling stories often break down.

This is where uncertainty estimation enters the picture.

A socially assistive robot has to act on weak signals: facial expression, prosody, posture, engagement, turn-taking, and
deviations from personal baselines.

A system that cannot represent uncertainty over these inferences will either miss opportunities to help or intervene in
brittle, overconfident ways.

### Personality and persona are control surfaces

A large section of the talk studies how robot persona changes human response.

Matarić reviews older work showing that personality matching between robot and user can increase exercise duration and
enjoyment.

She also describes newer work on psychometrically grounded personality prompting for large models.

The through-line is that "personality" is not decoration.

It is a steering mechanism.

Back-channel behavior, proxemics, voice, phrasing, and conflict style all influence whether people cooperate, persist,
or disengage.

This is highly relevant to steering techniques more broadly.

In current language-model research, steering is often discussed in terms of vectors, prompts, or reward-model
interventions.

Matarić's talk highlights a more ecological view.

Steering works because the system enters a social loop with a user, and the user updates too.

A successful intervention changes both sides of the interaction.

### Embodiment changes learning and trust

Matarić emphasizes that physical embodiment alters expectations and outcomes.

People infer rich capabilities from form.

Animal-like robots are expected to behave like animals.

Humanoids inherit the full burden of human expectation.

That makes abstract or non-humanoid embodiments attractive in many settings, because they produce fewer misleading
priors.

She also describes evidence that people disclose more to systems they believe are autonomous, and that physically
embodied systems can produce stronger engagement than purely screen-based tools.

This reinforces a broader robotics lesson.

The embodiment is part of the learning interface.

It shapes what data can be collected, what interventions are acceptable, and what kinds of concept representations are
needed internally.

A robot that must read gaze, repair misunderstandings, and regulate distance is solving a concept learning problem over
socially loaded latent variables.

### The hardest data regime is the clinically relevant one

Matarić repeatedly returns to populations such as autistic children, stroke survivors, people with dementia, and users
facing anxiety or depression.

These are not data-rich, IID environments.

They are high-variance, personal, and often non-stationary.

That is partly why the talk feels different from mainstream benchmark culture.

The most important settings for human-centered AI may be the ones least amenable to large homogeneous datasets.

This observation ties together concept representation learning and causal inference.

To personalize well, a system has to infer which latent factors are stable traits, which are temporary states, and which
interventions actually cause behavioral improvement.

Those are causal questions, not just predictive ones.

## Connections to Research Interests

### Interpretability

Matarić's emphasis on affect, intent, engagement, and personality makes interpretability a deployment necessity, not an
optional scientific luxury.

If a robot is influencing therapy adherence or child development, we need to know what signals it thinks it is reading,
which internal user model it is updating, and why it selected a given intervention.

Interpretability in this setting is closely tied to trust and auditability.

### Human-AI feedback loops

This keynote is fundamentally about a two-way adaptive loop.

The robot observes the user, updates a user model, changes its behavior, and thereby changes the user's future behavior.

That new behavior becomes the next training signal.

The loop is long-horizon, multimodal, and socially mediated.

Many alignment problems become easier to see once framed this way.

### Uncertainty estimation

Personalized behavioral inference is noisy by default.

A robot may be uncertain whether a user is disengaged, frustrated, overstimulated, or simply tired.

Matarić's examples suggest that robust systems must reason over these uncertainties explicitly, particularly in safety-
sensitive settings such as healthcare or child-facing interventions.

### Concept representation learning

The key internal concepts in this talk are not object categories.

They are socially meaningful latent variables: rapport, affect, confidence, overconfidence, personality, engagement, and
need.

Learning representations for those concepts in sparse, heterogeneous, personal data is one of the deepest ML problems
the keynote points to.

### Causal inference

The practical question is not merely whether certain cues correlate with better outcomes.

It is whether a particular intervention caused improvement.

Did personality matching increase adherence?

Did a vulnerable persona increase empathy?

Did physical embodiment change therapeutic alignment?

These are intervention questions, and the talk implicitly argues for more causal methodology in HRI.

### Robotics and world models

The keynote insists that robotics without social modeling is incomplete.

A household or clinical robot needs a world model that includes human routines, preferences, and changing capacities.

That is a richer and more demanding notion of world modeling than spatial prediction alone.

### Steering techniques

Much of the talk can be read as a catalog of socially grounded steering strategies: embodiment choice, persona design,
personality matching, prosody, vulnerability, and turn-taking.

The system is steered, but so is the user.

That bidirectionality is the main lesson.

## Takeaways

- Matarić's keynote reframes physical AI as a human-centered interaction problem, not just a control or perception
  problem.
- Socially assistive robotics offers a concrete template for augmentation-first AI systems that preserve human agency.
- Real progress in HRI depends on multimodal, long-horizon, personalized modeling under severe uncertainty.
- The most important latent variables are often socio-emotional rather than purely functional.
- For researchers interested in interpretability, steering, and feedback loops, socially assistive robotics is not
  peripheral. It is an unusually realistic testbed.
