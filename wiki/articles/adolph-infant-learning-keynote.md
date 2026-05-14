---
title: "Karen Adolph on Infant Learning — Summary"
type: "article"
tags: [iclr-2026, keynote, infant-learning, embodied-intelligence, robotics, open-science]
related: ["wiki/concepts/human-robot-interaction.md"]
sources: ["raw/iclr-2026-schedule-day3-sat.md", "raw/learning-while-developing-infants-intelligent-behavior-talk/README.md"]
---

# Karen Adolph on Infant Learning

## Overview

Karen Adolph's keynote is one of the clearest reminders at ICLR 2026 that intelligence is not best understood as a
static capability.

It is a developmental process.

The abstract in [the day-3 schedule](../../raw/iclr-2026-schedule-day3-sat.md) already states the argument succinctly:
infants become flexible, adaptive, and functional by learning while developing.

Their everyday practice is time-distributed, variable, error-filled, and often self-motivated rather than externally
goal-directed.

The full transcript in the captured talk materials expands this into a powerful program for embodied AI.

Adolph focuses on motor development, especially walking, but repeatedly argues that the same logic applies much more
broadly.

Babies learn intelligent behavior by generating enormous amounts of natural interaction data while their bodies, skills,
and environments are all changing at once.

That means their training distribution is not static.

It is developmentally staged, actively sampled, and deeply embodied.

For machine learning, this keynote is valuable on at least three fronts.

First, it reframes exploration and error as productive components of learning rather than nuisances to suppress.

Second, it links intelligence to affordance discovery, not just task completion.

Third, it makes a strong case for open behavioral data, especially shared video, as infrastructure for scientific
progress.

The result is a keynote that speaks directly to robotics, world models, concept representation learning, uncertainty,
and human-AI feedback loops.

## Key Points

### Behavior is the visible substrate of intelligence

Adolph opens by arguing that behavior is "everything we do" and therefore the right place to study how intelligence
develops.

In the transcript, she emphasizes looking, reaching, locomotion, interaction, and social behavior as observable windows
into developmental learning.

This matters because it shifts attention away from abstract competence scores and toward the mechanisms that generate
adaptive action in the world.

For ML, that is a useful corrective.

A model may appear capable on a benchmark, just as a child may appear capable in a constrained task, without having
learned the more general skill of detecting affordances, planning under change, and generating new solutions.

### Intelligent behavior is learned, not preloaded

One of the keynote's strongest claims is that intelligent human behavior is not innate.

Infants must learn at least three things: perceive affordances, explore and modify ongoing action, and find new
behavioral solutions.

Adolph's experiments with slopes, bridges, drop-offs, and other apparatuses show that novice walkers are often wildly
overconfident.

They repeatedly attempt actions beyond their current ability.

Experience, not maturation alone, turns that overconfidence into calibrated perception of affordances.

This is directly relevant to uncertainty estimation.

The infant is not just learning "how to walk."

The infant is learning when a planned action is safe, risky, or impossible.

In modern AI language, that is an embodied calibration problem.

### Development itself structures the curriculum

Adolph stresses that babies learn in changing bodies with changing skills in a changing world.

A crawling infant and a walking infant inhabit the same room, but they do not experience the same environment.

Crawling points the head downward and limits access.

Walking opens the room, expands visual range, and changes what can be touched, reached, and traversed.

This is one of the talk's most important lessons for robotics and world models.

The data distribution is not just something the learner samples from.

It is changed by the learner's morphology and competencies.

As capacity changes, the accessible world changes too.

That means developmental embodiment acts like an automatic curriculum.

### Exploration is often intrinsically motivated

Adolph asks a deceptively simple question: why do infants move so much?

Her experiments show that infants move extensively even in empty rooms, not only in toy-filled ones.

Much of their motion has no obvious external destination.

From this, she argues that movement is often intrinsically rewarding.

The "frolicking forager" model, which adds internal reward for movement, fits infant exploration better than purely
goal-directed optimal foraging.

This is important for AI because it highlights a failure mode in purely extrinsic views of exploration.

Not all intelligent action is best understood as reward-maximizing pursuit of external objects.

Some of it is self-generated data acquisition.

That connects naturally to curiosity, active learning, and intrinsic motivation in RL and robotics.

### Variability is a feature, not a bug

The schedule abstract calls infant practice variable and error-filled.

The transcript turns this into a central thesis.

Walking bouts are short, curved, omnidirectional, and context-dependent.

Infants practice across changing surfaces, room layouts, and social conditions.

This variability is not evidence of poor control alone.

It is part of what makes the learning process robust.

Adolph is explicit: variability keeps the system practicing, encountering new inputs, and discovering new solutions.

That observation connects strongly to concept representation learning.

A learner exposed only to narrow, clean, straight-line trajectories may learn brittle motor concepts.

A learner exposed to naturally varied behavior may build more transferable representations of balance, steering,
support, and recovery.

### Errors are common, but low penalty can be beneficial

Infants fall frequently.

Adolph reports about 40 falls per hour of locomotion, yet babies recover quickly and continue exploring.

The key point is not that errors are pleasant.

It is that they are low-cost enough not to halt practice.

Her collaboration with roboticist Peter Stone makes this especially relevant to ML.

In robot simulations, training on real infant paths beats training on neat geometric paths.

Moreover, robots trained with low penalty for falling transfer better to new paths than robots trained with stronger
negative penalties.

This is a provocative result.

It suggests that high error aversion can damage exploration and weaken transfer, especially in early skill acquisition.

For reinforcement learning, that translates into a challenge to overly punitive reward shaping.

### Infant practice regimens are surprisingly data-rich

Adolph emphasizes just how much natural data infants generate.

She reports thousands of steps per hour, large numbers of short walking bouts, and rich variability over time and
context.

The lesson is not merely that infants have "lots of data."

It is that their data are behaviorally grounded, interactive, and self-collected.

That is a different kind of scale from modern web pretraining.

It suggests that embodied systems may need smaller but more causally relevant and better structured datasets.

### Open video sharing is scientific infrastructure

The keynote ends with a strong argument for Databrary and open video sharing.

Adolph presents large-scale video repositories as a way to accelerate discovery, reproducibility, and cross-disciplinary
reuse.

She argues that video captures behavior at the timescale where intelligent action actually unfolds, and that future
researchers can ask questions the original collectors did not anticipate.

This is a powerful point for AI research.

Open, reusable behavioral data could become the bridge between developmental psychology, computer vision, robotics, and
multimodal learning.

It is also a human-AI feedback loop at the field level: scientists collect behavior, ML systems analyze it, and the
resulting tools motivate better future measurement.

## Connections to Research Interests

### Interpretability

Adolph's framework is unusually interpretable because the objects of study are behavioral strategies, affordance
judgments, and environmental interactions.

The emphasis is on understanding what learners are doing and why, not just whether they succeed.

That makes her work a strong template for behavior-centered interpretability in robotics.

### Human-AI feedback loops

Although the talk is about infants, it provides a concrete design philosophy for human-AI loops.

The learner samples data through action, updates its internal model, and then encounters a new environment partly
created by that action.

That recursive structure is exactly what many deployed agents will face.

### Uncertainty estimation

Perceiving affordances is a practical form of uncertainty estimation.

The learner has to know whether the current body and situation support a planned action.

Adolph's novice-versus-expert comparisons show how calibration improves with experience.

### Concept representation learning

The talk repeatedly points toward latent concepts such as support, risk, traversability, reward, and exploration value.

These are not symbolic labels handed to the learner.

They are distilled through embodied practice.

That is a rich agenda for concept learning research.

### Causal inference

Adolph's claims are stronger than simple correlation.

Her apparatus studies and robot simulations intervene on slopes, bridges, penalties, and path distributions to ask what
causes better learning and transfer.

That interventionist logic is a valuable model for AI experimentation.

### Robotics and world models

This keynote is deeply relevant to robotics.

It suggests that good world models are not just predictive maps of external state.

They must encode the relation between body, ability, and environment.

A world model for a developing agent is also a self-model.

### Steering techniques

The biggest steering lesson is negative.

Overly clean curricula, excessive penalties, and narrow trajectories may steer learners toward brittle competence.

Adolph's evidence suggests that better steering may involve preserving variability and keeping the cost of error low
enough for continued practice.

## Takeaways

- Adolph presents infant learning as a developmental, embodied, data-rich process rather than a static benchmark success
  story.
- Variability, intrinsic motivation, and low-cost errors appear central to robust skill acquisition.
- Her robot experiments imply that more realistic training distributions can outperform cleaner, more engineered ones.
- The keynote offers a compelling developmental perspective on robotics, uncertainty, and concept learning.
- Open video sharing is not just archival infrastructure. It is a platform for future multimodal science.
