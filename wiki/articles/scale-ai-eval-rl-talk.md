---
title: "Scale AI on Evaluation and RL Frontiers — Summary"
type: "article"
tags: [iclr-2026, talk, evaluation, reinforcement-learning, ai-agents, steering-techniques]
related: ["wiki/summaries/scale-ai-new-frontier-eval-rl-expo-talk.md", "wiki/concepts/llm-evaluation.md", "wiki/concepts/reward-hacking.md"]
sources: ["raw/scale-ai-new-frontier-eval-rl-expo-talk.md"]
---

# Scale AI on Evaluation and RL Frontiers

## Overview

Scale AI's expo talk, [captured here](../../raw/scale-ai-new-frontier-eval-rl-expo-talk.md), argues that the next
capability bottleneck for large language models is not raw scale but verification.

The abstract contrasts domains with cheap correctness signals, such as math and code, with long-horizon domains where
correctness is delayed, weak, or ambiguous, such as research planning and strategic work.

This "verification asymmetry" explains why some benchmark curves rise quickly while broader agentic competence remains
limited.

The talk then presents three evaluation frameworks: Humanity's Last Exam, Remote Labor Index, and Visual ToolBench.

Together they paint a picture of frontier systems that are often wrong, overconfident, poor at automating real labor,
and bottlenecked more by perception than by reasoning in multimodal settings.

Scale AI's proposed response is to shift from static benchmarks toward training environments where evaluation rubrics
become reward signals.

The key mechanism is Rubrics as Rewards within a GRPO framework, with dynamic rubrics outperforming static hand-written
ones and reducing reward hacking.

That makes the talk especially relevant to steering, uncertainty, world models, and human-AI feedback loops.

It is a strong statement that alignment and capability progress now depend on building better evaluative environments,
not just bigger models.

## Key Points

### Verification asymmetry is the new bottleneck

The abstract's central concept is verification asymmetry.

Some tasks provide cheap and reliable correctness signals.

If a solution compiles, passes tests, or matches a mathematical answer, RL can optimize it aggressively.

Other tasks, especially strategic or long-horizon ones, lack such immediate feedback.

That means capability progress is uneven across domains, not necessarily because the model lacks raw potential, but
because the training and evaluation signals are weak.

This framing is important because it explains why benchmark progress can look impressive while real-agent performance
remains limited.

### Humanity's Last Exam exposes overconfidence at expert level

The first evaluation framework, Humanity's Last Exam, is described as showing that frontier models are frequently wrong
and overconfident at the human-expert level.

This matters because the problem is not simply accuracy.

It is miscalibrated confidence on difficult tasks.

That connects directly to uncertainty estimation.

A system that fails confidently on expert-level questions is dangerous in settings where users may not be able to verify
answers themselves.

### Remote Labor Index grounds evaluation in real work

The second framework, Remote Labor Index, reports that current agents automate only about 2.5% of real paid freelance
work.

This is a valuable corrective to synthetic benchmark optimism.

It says, in effect, that even if models look strong on curated tasks, real-world task bundles remain resistant to
automation.

That suggests evaluation should focus more on task ecology: coordination, error recovery, context switching, and
incomplete instructions.

It also ties naturally to human-AI feedback loops, because paid work often includes iterative clarifications, quality
checks, and shifting goals.

### Visual ToolBench shows perception remains a major failure point

The third framework, Visual ToolBench, finds that 70-80% of multimodal agent failures stem from visual perception rather
than reasoning.

This is important because the field often assumes reasoning is the limiting factor once language models become tool-
using agents.

Scale AI's data suggest that for many multimodal workflows, the bottleneck is still getting the world state right in the
first place.

That has immediate implications for robotics and world models.

An agent cannot plan reliably if its perceptual grounding is weak.

### Static benchmarks are giving way to evaluative environments

The talk's main strategic proposal is to move beyond static benchmark suites.

Static evaluations are useful snapshots, but they are poor substitutes for environments in which agents must act,
receive feedback, and adapt.

Scale AI names this destination explicitly with Scale Gymnasium: high-fidelity RL environments for training through
interaction rather than imitation.

This is a major shift in perspective.

Evaluation is no longer the thing done after training.

Evaluation becomes the environment in which training happens.

### Rubrics as Rewards makes human judgment operational

Rubrics as Rewards is the talk's most direct bridge between human evaluation and RL.

The idea is to use evaluation rubrics as reward signals so that training can extend beyond domains with hard verifiers.

This is interesting because rubrics are usually viewed as soft guidance for annotators or judges.

Scale AI turns them into optimization targets.

That raises an important research question: how should fuzzy human criteria be represented so they are useful for
optimization without collapsing into brittle shortcuts?

### Dynamic rubrics outperform static ones

The abstract reports that dynamic rubrics, which adaptively elicit criteria by contrasting model outputs during
training, outperform static human-written rubrics and reduce reward hacking in the high-reward regime.

This is a strong claim.

It suggests that the reward function itself may need to be interactive and contextual.

A fixed reward specification is often too easy to exploit.

A dynamically updated rubric can track what distinctions actually matter between candidate outputs.

That is a steering insight.

Instead of trying to write the perfect static objective, one can build a system that refines the objective as failure
modes appear.

### Reward hacking remains central

The talk explicitly positions dynamic rubrics as a way to reduce reward hacking.

That is important because the frontier beyond verifiable domains is exactly where reward misspecification becomes most
dangerous.

When correctness is weakly observed, models have more room to exploit proxies.

The keynote therefore ties capability progress directly to oversight quality.

### The proposed frontier is jointly evaluative and generative

Scale AI's broader vision is not just to measure what models can do, but to build environments in which richer
evaluation yields better learning.

This is a powerful human-AI feedback-loop story.

Humans define rubrics, models generate candidate behaviors, the rubric updates, and the new reward shapes future policy.

If this works, evaluation and training stop being separate phases and become a single adaptive loop.

## Connections to Research Interests

### Interpretability

Rubrics make optimization criteria more legible than raw scalar rewards alone.

They provide a natural-language or structured explanation of what behavior is being rewarded.

That is not full interpretability, but it is a useful step toward more inspectable RL objectives.

### Human-AI feedback loops

This talk is centrally about turning human evaluative judgment into iterative training signal.

Dynamic rubrics are a direct instantiation of that feedback loop.

### Uncertainty estimation

Humanity's Last Exam puts calibration and overconfidence at the center of the evaluation story.

The talk implicitly argues that long-horizon agents need stronger uncertainty awareness if they are to move beyond
narrow verifier-rich domains.

### Concept representation learning

Rubrics represent latent evaluative concepts: usefulness, faithfulness, completeness, safety, or task success.

Learning to operationalize those concepts for optimization is a core challenge.

### Causal inference

Dynamic rubrics can be read as interventions on the reward function designed to see which evaluative distinctions
actually cause better downstream behavior.

### Robotics and world models

Visual ToolBench's failure analysis is highly relevant to robotics.

If most multimodal failures are perceptual, then stronger world models require better grounded perception before more
elaborate planning can pay off.

### Steering techniques

Rubrics as Rewards is explicitly a steering technique.

It steers agent behavior through structured evaluative criteria, and dynamic rubrics add a meta-steering layer that
adapts the criteria as the model changes.

## Takeaways

- Scale AI argues that verification asymmetry is now the main capability bottleneck for long-horizon agents.
- Its three evaluation frameworks show that models remain overconfident, weak on real labor, and often bottlenecked by
  perception.
- Static benchmarks are insufficient for the next stage of agent training.
- Rubrics as Rewards turns human evaluation criteria into RL signal, while dynamic rubrics help reduce reward hacking.
- The talk is a strong case for evaluation environments as the next frontier of both alignment and capability research.
