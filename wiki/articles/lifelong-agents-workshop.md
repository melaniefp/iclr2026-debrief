---
title: "Workshop: Lifelong Agents: Learning, Aligning, Evolving — Key Takeaways"
type: "article"
tags:
  - iclr-2026
  - workshop
  - lifelong-agents
  - agent-alignment
  - continual-learning
  - human-ai-feedback
  - robotics
related:
  - "raw/iclr-2026-workshop-lifelong-agents.md"
  - "wiki/summaries/iclr-2026-workshop-lifelong-agents.md"
  - "wiki/concepts/world-models.md"
  - "wiki/concepts/human-robot-interaction.md"
sources:
  - "raw/iclr-2026-workshop-lifelong-agents.md"
  - "raw/iclr-2026-workshop-lifelong-agents-talk/"
---

# Workshop: Lifelong Agents: Learning, Aligning, Evolving — Key Takeaways

## Overview

The [Lifelong Agents workshop](../../raw/iclr-2026-workshop-lifelong-agents.md) framed a clear agenda: agents should not be trained once and then frozen, but should instead keep learning, stay aligned with people, and improve under real deployment constraints.
The workshop page emphasizes continual learning, long-term alignment, self-improvement, and sustainability.
The opening portion of the [workshop transcript](../../raw/iclr-2026-workshop-lifelong-agents-talk/transcript.md) sharpens that agenda into a concrete systems picture.
The recurring message is that lifelong agency is not one technique.
It is a stack.
It needs self-awareness, memory, world modeling, reward design, and post-deployment adaptation.

Several practical constraints are foregrounded from the start.
Agents should know when not to call tools.
They should reason about uncertainty before acting.
They should remain legible to users across long conversations.
They should improve from feedback without requiring endless expensive retraining.
And they should remain efficient enough to be viable outside frontier-model-only deployments.

That combination makes this workshop especially relevant to interpretability, human-AI feedback loops, uncertainty, concept-level memory, causal reasoning about action consequences, robotics, world models, and steering.
Rather than treating those as separate themes, the workshop suggests they are parts of the same deployment problem.
The most interesting talks are the ones that connect them.

### Program signal

- The workshop description centers continuous learning, alignment, and evolution.
- The opening talk argues for self-awareness about knowledge boundaries.
- The invited talks span robotics, safety, memory, and small-model deployment.
- The oral papers reinforce the same agenda with context engineering, world modeling, text feedback, and continual learning.
- The transcript repeatedly returns to efficiency, memory, and adaptation after deployment.
- The overall impression is that lifelong agents are becoming a systems problem rather than a benchmark problem.

## Key Invited Talks

### 1. Robotic Learning with Autonomous Data — Sergey Levine

Levine's talk is the workshop's clearest bridge to robotics and embodied AI.
In the transcript, he argues that lifelong learning becomes much more meaningful in the physical world because the world is richer than text corpora and richer than closed games.
The core message is that robot foundation models need a post-training loop that learns from real interaction rather than only imitation.

Key takeaways from Levine's segment:

- Real-world robotics is a strong testbed for lifelong learning because the environment is genuinely open-ended.
- Pretraining provides broad priors, but post-training is where robust action policies are shaped.
- Reinforcement learning for robotics is hard because the system must be sample-efficient, operate with large models, and still improve difficult tasks.
- One practical solution is to train narrow RL specialists first, then use their data to improve generalist models.
- This creates a plausible lifelong loop: specialists improve the generalist, and the generalist can later seed better specialists.
- The robotics framing makes human-AI feedback loops concrete: people intervene, correct, and supply preferences during physical execution.
- For robotics-oriented work, this is a strong argument that progress may depend less on a single monolithic model and more on modular data-generation loops.

### 2. LLM Safety is a Multi-agent Problem — Natasha Jaques

Jaques makes the strongest direct case that safety should be modeled as an interactive, multi-agent process rather than as a static single-model property.
Her talk connects adversarial training, human adaptation, and online personalization.
It is one of the most relevant invited talks for human-AI feedback loops.

Key takeaways from Jaques's segment:

- Once deployed, LLMs always operate in multi-agent settings because people adapt to them.
- Safety should therefore be stress-tested against adaptive adversaries, not only against fixed prompts.
- Two-player training setups can improve refusal robustness without heavily sacrificing helpfulness.
- Reward models still matter, but they are not enough on their own.
- The deeper issue is that models shape human communication, not just answers.
- Her writing studies suggest current RLHF-style systems homogenize language and can alter user intent.
- That motivates personalization methods that help a model approximate what a user would have done, rather than steering them toward a generic style.
- The personalized, online user-modeling work she describes is a direct example of a lifelong feedback loop inside the interaction itself.

### 3. Memory-based reinforcement learning for deployment-time learning — Jun Wang

The workshop page does not publish a formal title for Jun Wang's talk, but the transcript makes the theme explicit.
Wang presents a memory-centric approach to letting agents learn at deployment time without changing the base model weights.
That makes the talk one of the clearest contributions to concept representation and test-time adaptation.

Key takeaways from Wang's segment:

- Lifelong learning should not assume continual gradient updates to the base LLM.
- A more practical alternative is to let the agent read from and write to memory over time.
- Reflection over memory can function like policy improvement.
- Writing new experience back to memory can function like policy evaluation.
- This reframes case-based reasoning as a live reinforcement-learning loop for agents.
- Consolidation matters: agents should not store every trajectory verbatim.
- They need summaries, abstractions, and compressed lessons.
- This is concept representation learning in an operational form: the system builds reusable high-level cases rather than only raw traces.

### 4. Invited Talk 4 — Asli Celikyilmaz

The captured workshop page lists [Asli Celikyilmaz](../../raw/iclr-2026-workshop-lifelong-agents.md) as an invited speaker but does not expose a public title or abstract.
The surrounding transcript does, however, reveal the role this slot played in the day's argument.
Later speakers reference her discussion of belief drift and the difficulty of keeping agents synchronized with updated user beliefs.

Useful takeaways from the surrounding context:

- Lifelong agents need mechanisms for belief updating, not just memory accumulation.
- A stored memory that is never revised becomes a liability.
- Alignment therefore requires tracking when a user's beliefs or goals have changed.
- This is tightly linked to interpretability because a system must expose what it thinks the current user state is.
- It also links to steering, since the system needs ways to redirect itself when stale assumptions are detected.

### 5. Lifelong Agents from Small Language Models — Siva Reddy

Reddy's talk complements Levine by arguing that practical lifelong agents may need to move downscale, not upscale.
The question is not only whether a frontier model can serve as an agent, but whether a smaller, specialized, privacy-preserving model can do the job well enough while staying trainable.

Key takeaways from Reddy's segment:

- Building lifelong agents on top of frontier APIs is expensive, slow, and hard to personalize.
- Small language models become attractive if they can be distilled into domain competence.
- Distillation should include reasoning traces, not just outputs.
- Persona-conditioned synthetic tasks are useful for training narrow but strong agents.
- Personalization should come from user history and interaction traces, not only explicit profiles.
- Memory retrieval should ideally be handled by the same small model rather than by a separate heavy stack.
- This is a strong systems argument for local agents that can keep learning near the user.
- The talk is especially relevant to steering and efficient deployment.

### 6. Invited Talk 6 — Azalia Mirhoseini

The captured workshop page lists [Azalia Mirhoseini](../../raw/iclr-2026-workshop-lifelong-agents.md) but does not expose a title or abstract in the local sources.
Even with that limitation, her placement at the end of the invited program reinforces one of the workshop's repeated concerns: scaling lifelong adaptation requires careful systems design, not just better prompting.

What this slot contributes at the workshop level:

- Efficiency is not a side issue for lifelong agents.
- Any deployment-time learning scheme must fit real latency and cost budgets.
- The workshop repeatedly returns to sustainable adaptation, which aligns with Mirhoseini's broader systems profile.
- This strengthens the case that lifelong agents need joint progress in learning algorithms and systems optimization.

## Themes & Takeaways

### Interpretability

The workshop does not treat interpretability as a standalone analysis tool.
Instead, interpretability shows up as self-awareness and introspection in agent loops.

- The opening talk argues that agents should know their own knowledge boundary.
- Tool use becomes an interpretability problem: the system must expose why it is acting.
- Granular rewards for format, correctness, and tool use create more inspectable training signals.
- Wang's memory loop suggests interpretable units of experience can be stored as reusable cases.
- Jaques's user-modeling work implies that if a system builds a model of the user, that model should be inspectable.
- Reddy's small-model framing makes interpretability more actionable because the deployed system is closer to the user and easier to audit.
- Overall, the workshop favors operational interpretability over purely post hoc explanation.

### Human-AI feedback loops

This is arguably the central theme of the workshop.

- The opening talk explicitly splits reward into fine-grained components and conversational trajectories.
- Text feedback, simulated users, and trajectory-level rewards all appear as richer feedback channels.
- Jaques reframes safety as adaptation under interaction rather than a one-shot alignment objective.
- Reddy frames personalization as learning from behavioral traces already produced by the user.
- Levine shows feedback entering through human intervention in robotic RL.
- The oral papers on context engineering, RL from text feedback, and self-distillation further reinforce that feedback should remain inside the loop.
- The net message is that lifelong agents improve when feedback is continuous, structured, and cheap enough to collect.

### Uncertainty estimation

Uncertainty is present in several different forms.

- The opening talk uses uncertainty as a trigger for self-augmentation.
- An agent should decide whether it knows enough before acting.
- World models are useful only if the agent knows when to trust them.
- Levine's robotics setting makes uncertainty unavoidable because real-world exploration is costly.
- Jaques's safety framing implies uncertainty should also attach to user models and adversarial robustness.
- Reddy's push toward small models raises the further question of how to quantify confidence under heavy personalization.
- The workshop's implicit view is that uncertainty is a control signal for acting, querying, retrieving, or deferring.

### Concept representation learning

The memory and abstraction story is one of the workshop's most distinctive contributions.

- Wang emphasizes storing experiences as cases and then consolidating them.
- Consolidation is a step toward concept-level memory rather than raw episodic storage.
- The opening talk similarly distinguishes internal cognition from external tools.
- Reddy's specialization story suggests that useful concepts may be domain-specific and user-specific.
- Oral papers on agentic context engineering and continual learning support the same idea from different angles.
- A lifelong agent probably needs multiple representation scales: traces, cases, summaries, and stable preferences.
- That makes concept learning a memory-design problem as much as a model-design problem.

### Causal inference

Causal language is not the dominant vocabulary of the workshop, but causal reasoning about action consequences is everywhere.

- The opening talk's world-model discussion is explicitly about predicting consequences before acting.
- Levine's robotics argument depends on learning what actions do in the real world.
- Jaques's multi-agent framing adds strategic causality: other agents respond to what the model does.
- Wang's memory loop can be read as collecting intervention-outcome pairs over time.
- The contributed papers on embodied world modeling and RL from feedback further emphasize state change under action.
- The workshop therefore treats causality less as formal graph discovery and more as actionable counterfactual competence.

### Robotics

Robotics is not an add-on in this workshop.
It is one of the clearest settings where lifelong learning becomes necessary.

- Levine argues that robotic learning exposes richer novelty than text-only environments.
- Real-world interaction creates opportunities for continual improvement and human correction.
- Sample efficiency matters more in robotics than in purely digital settings.
- Safety constraints are sharper because actions have physical consequences.
- Embodied tasks create a natural testbed for world models, long-horizon memory, and user alignment.
- For robotics work, this is perhaps the workshop's strongest argument that lifelong-agent research should stay grounded in physical interaction.

### World models

World models appear twice: as internal sandboxes in the opening talk and as concrete embodied research problems in posters and talks.

- The opening talk treats text-based world models as a way to verify actions, synthesize trajectories, and warm-start RL.
- It also highlights a major failure mode: agents often do not know how to use the world model well.
- That makes world-model utilization, not only world-model accuracy, a core research problem.
- Levine brings the same issue into robotics through data collection and RL specialists.
- Oral paper themes like ENACT push toward embodied evaluation rather than purely generative fidelity.
- The takeaway is that world models should be judged by how they support action selection and adaptation.

### Steering techniques

Steering is present in both reward design and memory design.

- The opening talk proposes explicit penalties for unnecessary tool use.
- That is a form of behavioral steering through reward shaping.
- Jaques's adversarial training steers a model toward robust refusals.
- Wang's read/write memory loop steers action through retrieved experience.
- Reddy's personalization agenda is essentially user-conditioned steering.
- Across the workshop, steering is not treated as a last-minute patch.
- It is built into rewards, memories, interfaces, and retrieval policies.

## Connections to PAI Research

This workshop lines up unusually well with these research interests.

### Why it matters for the core agenda

- Interpretability is being operationalized as self-awareness, memory inspection, and user modeling.
- Human-AI feedback loops are treated as the basic training substrate for lifelong agents.
- Uncertainty estimation is framed as the control variable for acting, asking, or abstaining.
- Concept representation learning appears as memory consolidation and context engineering.
- Causal reasoning appears through predictive simulation and intervention-aware planning.

### Why it matters for robotics, world models, and steering

- Levine's talk directly argues for robotics as the richest deployment setting for lifelong learning.
- The opening talk and the ENACT oral slot both suggest world models should be evaluated by utility for action.
- Wang and Reddy together imply that long-lived agents will need both structured memory and efficient local deployment.
- Jaques's talk shows steering cannot stop at prompt engineering; it has to account for strategic interaction.
- The workshop repeatedly emphasizes that deployment constraints change what counts as a good learning algorithm.

### Practical research opportunities suggested by the workshop

- Build agents that expose their current user model and memory state.
- Study when world-model consultation improves outcomes versus creating overthinking.
- Compare weight updates, memory updates, and retrieval updates as three different lifelong-learning mechanisms.
- Design small-model agent stacks that can be personalized locally.
- Create robotics evaluations where safety, adaptation, and feedback richness matter simultaneously.
- Treat steering as a systems problem spanning rewards, retrieval, interfaces, and monitoring.

## Signals from Contributed Talks and Posters

The invited talks were only part of the story.
The oral and poster lineup sharpened the same agenda.

- **Agentic Context Engineering** suggests that evolving prompts and memories may serve as lightweight continual-learning substrates.
- **ENACT** pushes world-model evaluation into egocentric embodied settings.
- **RL from Text Feedback** reinforces the workshop's view that scalar rewards are too weak for many real interactions.
- **Self-Distillation Enables Continual Learning** directly targets forgetting in sequential skill acquisition.
- Poster themes such as context compression, self-evolving agents, and agent routing all point to memory management as a bottleneck.
- Many poster titles frame safety and alignment drift as long-horizon problems, not single-turn ones.
- The oral program therefore supports the invited talks' claim that lifelong agency needs both better algorithms and better interfaces.
- It also shows that the workshop community is already converging on memory, feedback, and environment modeling as the main axes of progress.

## Open Questions

- What is the right division of labor between model weights, external memory, and retrieval-time steering?
- When should a lifelong agent update beliefs versus preserving stable user preferences?
- How can agents tell whether a world model is trustworthy enough to guide action?
- What forms of feedback are rich enough to improve behavior but cheap enough to scale?
- Can small local models match frontier-model agents on narrow but real personal tasks?
- How should we evaluate catastrophic forgetting in agents that store large external memories?
- What is the right benchmark for lifelong safety in multi-agent environments?
- Can robotics provide the most realistic path to studying lifelong alignment under real consequences?
- How do we keep personalized agents from becoming overly sycophantic or overly conservative?
- What abstractions should memory consolidation preserve so that agents learn reusable concepts rather than brittle anecdotes?

## Sources

- [Workshop page](../../raw/iclr-2026-workshop-lifelong-agents.md) — workshop framing, schedule, invited speakers, and oral-paper themes.
- [Workshop recording capture](../../raw/iclr-2026-workshop-lifelong-agents-talk/README.md) — metadata for the recorded livestream.
- [Workshop transcript](../../raw/iclr-2026-workshop-lifelong-agents-talk/transcript.md) — opening vision, Sergey Levine, Natasha Jaques, Jun Wang, and Siva Reddy segments that anchor this synthesis.
