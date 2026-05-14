---
title: "LLMs Get Lost in Multi-Turn Conversation — Summary"
type: "article"
tags: [iclr-2026, talk, llm-evaluation, multi-turn-conversation, uncertainty-estimation, human-ai-feedback-loops]
related: ["wiki/papers/llms-get-lost-in-multi-turn-conversation.md", "wiki/summaries/iclr-2026-oral-session-2d-llms-evaluation.md", "wiki/concepts/multi-turn-conversation.md", "wiki/concepts/llm-evaluation.md"]
sources: ["raw/llms-get-lost-in-multi-turn-conversation-talk/README.md", "wiki/papers/llms-get-lost-in-multi-turn-conversation.md", "raw/iclr-2026-oral-session-2d-llms-evaluation.md"]
---

# LLMs Get Lost in Multi-Turn Conversation

## Overview

The oral talk for [LLMs Get Lost in Multi-Turn Conversation](../../raw/llms-get-lost-in-multi-turn-conversation-
talk/README.md) explains a deceptively simple failure mode: large language models perform substantially worse when
information is revealed across several conversational turns rather than given all at once.

The corresponding [paper summary](../papers/llms-get-lost-in-multi-turn-conversation.md) and [oral-session
listing](../../raw/iclr-2026-oral-session-2d-llms-evaluation.md) make clear that this was not a niche result.

It received an Outstanding Paper Award, and the empirical pattern held across 15 models and six generation tasks.

The central result is stark.

Average performance drops by about 39% in the multi-turn, underspecified setting.

More importantly, the talk argues that this is not mainly a loss of underlying aptitude.

It is a loss of reliability.

Models make a wrong assumption early, commit to it, and then fail to recover even as later turns reveal the missing
details.

That observation is highly relevant to anyone interested in human-AI feedback loops, uncertainty estimation, world
models, and steering.

Interactive systems are supposed to help users refine intent over time.

If multi-turn interaction itself is the source of brittleness, then many current agent and assistant paradigms are more
fragile than their single-turn benchmarks suggest.

## Key Points

### The benchmark problem is underspecification, not just task difficulty

In the talk transcript, Philippe Laban explains that the original motivation came from saturated single-turn coding
benchmarks such as HumanEval.

The key question was not whether the tasks were too easy, but whether they resembled how people actually use
conversational systems.

Users often do not start with a fully specified request.

They refine intent over several turns.

The paper's "sharded instruction" setup formalizes this idea by splitting one fully specified task into a sequence of
conversational shards that reveal the same information gradually.

This is important because it isolates a real deployment phenomenon.

The issue is not simply long context.

It is interactive underspecification.

### The concat control shows that wording is not the main cause

A major strength of the work is the concat control described in both the talk and the paper summary.

The authors take the same sharded content and concatenate it into a single-turn bullet list.

Performance in this concat condition remains close to the original full single-turn condition.

That means the performance drop is not primarily due to paraphrasing or information loss during sharding.

It is the multi-turn interaction structure itself that hurts the models.

This is a key scientific contribution, because it rules out a simpler explanation.

### Multi-turn degradation is universal across model families

The paper summary reports that all 15 tested models, including GPT-4.1, Gemini 2.5 Pro, Claude 3.7 Sonnet, o3, and
DeepSeek-R1, show major degradation in sharded multi-turn settings.

The oral talk shows the same pattern across code, database, tool-calling, math, data-to-text, and summarization tasks.

That universality matters.

The phenomenon is not a quirk of one architecture or one task family.

It appears to be a basic weakness in how current LLMs handle partially revealed intent over time.

### The main failure is unreliability, not incapacity

One of the talk's most useful conceptual contributions is the separation between aptitude and unreliability.

Aptitude measures something like best-case performance.

Unreliability measures the spread between best and worst outcomes across repeated simulations.

According to both the paper summary and the oral-session description, aptitude drops only modestly.

Unreliability, by contrast, more than doubles.

In other words, models still often know how to solve the task.

They just become much more likely to get derailed.

This is why the phrase "get lost" is so apt.

The issue is path dependence, not simple inability.

### Early assumptions poison the rest of the conversation

The talk transcript gives a clean intuitive explanation.

Models answer too early, before they have all the necessary information.

Once they commit, they rely too heavily on those initial assumptions.

Later turns then fail to fully overwrite the earlier internal trajectory.

The paper's qualitative analysis sharpens this into four recurring patterns: premature answer attempts, answer bloat,
loss-in-middle-turns, and over-verbosity.

All four point to a similar internal dynamic.

The model acts as though it is building a conversational world model, but it updates that model poorly once it has
locked onto the wrong state.

### More memory helps only a little

A natural mitigation is to summarize the conversation so far.

The authors test recap and snowball strategies that restate information as the conversation unfolds.

These agent-like memory mechanisms help somewhat, but only recover a fraction of the lost performance.

That is a sobering result.

Many people assume that if models lose track, the solution is simply better memory management.

This paper shows that memory alone is not enough.

The deeper problem is how the model reasons over an evolving, underspecified interaction state.

### Lower temperature does not fix the reliability problem

The oral talk also evaluates temperature.

Reducing temperature helps reliability in single-turn settings, but has almost no effect in multi-turn sharded
conversations.

The explanation is insightful.

Even a small divergence in an early turn cascades into an entirely different interaction trajectory.

This means that stochasticity is not the main source of failure.

Structural conversational brittleness is.

That is highly relevant to uncertainty estimation.

The model may sound confident regardless of whether its current latent task representation is on track.

### Reasoning models do not escape the problem

The paper summary notes that models with explicit reasoning traces, such as o3 and DeepSeek-R1, still degrade
substantially.

That suggests the failure is not cured simply by giving models more test-time reasoning tokens.

The difficult part is staying calibrated about missing information and revising earlier assumptions as the conversation
unfolds.

### The result matters because real assistants are interactive by design

The oral-session description makes the practical stakes clear.

LLMs are supposed to help users define, explore, and refine their needs through dialogue.

If multi-turn interaction itself produces a 39% performance drop, then standard single-turn evaluations systematically
overestimate user-facing reliability.

This is one of the talk's biggest contributions.

It redefines what "robustness" should mean for conversational AI.

## Connections to Research Interests

### Interpretability

The paper's decomposition into aptitude and unreliability is already a useful interpretability move.

It tells us which part of the failure is due to missing capability and which is due to trajectory instability.

The qualitative root causes push further toward mechanistic questions about when models prematurely commit.

### Human-AI feedback loops

This talk is fundamentally about a feedback loop between user clarification and model update.

The user refines the task, but the model often fails to revise its internal state accordingly.

That makes the loop brittle in a way that static evaluations miss.

### Uncertainty estimation

The models do not know when they should withhold commitment.

They act as though they are certain too early.

The work therefore points directly to the need for uncertainty-aware dialogue policies and confidence estimates over
task completion state.

### Concept representation learning

The sharded setting pressures models to maintain an evolving concept of the user's latent intent.

The failures suggest that those intent representations are either unstable, overwritten poorly, or coupled too tightly
to early surface forms.

### Causal inference

The experimental design is strong because it isolates the cause of degradation.

By comparing full, concat, and sharded setups on matched content, the paper shows that the conversational structure
causes the drop.

### Robotics and world models

Any long-horizon agent or robot that must update plans from partial human input faces an analogous challenge.

The talk can be read as evidence that current LLM world models of interactive tasks remain brittle under online
revision.

### Steering techniques

The partial success of recap and snowball suggests that better conversational steering may require explicit commitment
control, revision policies, or learned uncertainty-triggered deferral, not just more memory.

## Takeaways

- Multi-turn underspecification causes a large and robust performance drop even in frontier models.
- The main issue is unreliability: models get locked into early wrong assumptions and do not recover well.
- Concat controls show that the problem is the interaction structure, not merely paraphrasing.
- Memory aids help, but only partially.
- This talk is a major warning that conversational benchmark success can mask a deep reliability gap in real human-AI
  interaction.
