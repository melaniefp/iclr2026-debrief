---
title: "Workshop: Navigating and Addressing Data Problems For Foundation Models (DATA-FM) — Key Takeaways"
type: "article"
tags:
  - iclr-2026
  - workshop
  - data-fm
  - data-quality
  - foundation-models
  - evaluation
related:
  - "raw/iclr-2026-workshop-data-fm.md"
  - "wiki/summaries/iclr-2026-workshop-data-fm.md"
  - "wiki/concepts/llm-evaluation.md"
  - "wiki/concepts/open-source-ai.md"
sources:
  - "raw/iclr-2026-workshop-data-fm.md"
  - "raw/iclr-2026-workshop-data-fm-talk/"
---

# Workshop: Navigating and Addressing Data Problems For Foundation Models (DATA-FM) — Key Takeaways

## Overview

The [DATA-FM workshop](../../raw/iclr-2026-workshop-data-fm.md) makes a strong claim that data remains the decisive design variable in foundation-model development.
That claim is more ambitious than the usual “garbage in, garbage out” slogan.
Here, data is not only pretraining fuel.
It is also the substrate for post-training, evaluation, privacy protection, multimodal alignment, and agent benchmarking.

The workshop description is notable for how many frontiers it connects.
It links RLVR and reasoning traces.
It links multimodality and aligned corpora.
It links agent systems and interaction logs.
It links evaluation quality to benchmark construction.
And it links all of that to copyright, privacy, and fairness constraints.
The result is a very broad but surprisingly coherent data-centric agenda.

The transcript reinforces this by focusing early on what counts as good reasoning data, what kinds of data mixtures make models stronger, and what kinds of evaluations actually reflect model capability.
Across the invited talks, the repeated message is that performance gains increasingly come from better selection, better structure, and better measurement of data.
That has obvious implications for interpretability, feedback loops, uncertainty, concept learning, and world models.

### Program signal

- The workshop description explicitly treats data as central to reasoning, multimodality, and evaluation.
- The opening remarks mention hallucinated citations in submissions, which is itself a data-quality warning sign.
- Baharan Mirzasoleiman's talk frames post-training data curation as an optimization problem.
- Sewon Min's talk reframes data fragmentation as a training-architecture problem.
- Juan Carlos Niebles pushes the discussion toward physical-world multimodal data.
- Fred Sala emphasizes benchmark design as data design for evaluation.
- The oral papers on mixtures, memorization, anchored decoding, and annotation systems extend the same thread.

## Key Invited Talks

### 1. Baharan Mirzasoleiman — Post-training data curation for reasoning models

The workshop page does not expose a formal title for Mirzasoleiman's talk, but the transcript is explicit about its subject: which post-training data actually helps reasoning models.
The talk is one of the clearest efforts to separate intuitions about SFT, RL, and test-time scaling.

Key takeaways from Mirzasoleiman's segment:

- Reasoning models differ from ordinary instruction-tuned models because they produce much longer trajectories.
- For supervised fine-tuning, harder and more diverse examples can be more valuable than larger quantities of generic data.
- For RL-style post-training, the optimal data difficulty is different: not trivial, but also not too hard.
- Test-time scaling only helps reliably when the model already knows something about the task family.
- When a model lacks the relevant knowledge, extra thinking can worsen performance through overthinking.
- Pretraining and post-training data quality interact; you cannot reason about one in isolation.
- Data curation should therefore be adaptive to the current model, not only to some external label of quality.
- The proposed filtering methods suggest data quality can sometimes be inferred cheaply from early prefixes and perturbed checkpoints.

### 2. Sewon Min — Fragmented data and modular distributed training

The workshop page lists only Sewon Min's slot, but the transcript reveals a focused talk on fragmented data.
This is a useful contribution because it reframes the “data is running out” story.
The problem is not only scarcity.
It is that valuable data is scattered across organizations that will not share it.

Key takeaways from Min's segment:

- Valuable FM data is often private, specialized, and institutionally fragmented.
- Standard centralized training implicitly assumes access patterns that no longer hold.
- Mixture-of-experts architectures provide a promising substrate for modular distributed training.
- The proposed FlexOLMO-style recipe keeps local data private while still allowing contribution through expert parameters.
- Modular training makes opt-in and opt-out easier than conventional centralized pipelines.
- This turns data ownership and governance into model-architecture questions.
- The resulting system retains much of the performance of fully joint training while preserving data locality.
- For research on open models, this is a concrete path toward incorporating private expertise without raw-data release.

### 3. Juan Carlos Niebles — Agentic Ambient Intelligence: Perception, Reasoning & Action

Niebles' talk, publicly titled **Agentic Ambient Intelligence: Perception, Reasoning & Action**, is the workshop's strongest bridge to robotics, multimodality, and world models.
Instead of focusing on web agents, he asks what data pipelines are needed for AI systems that support people in physical space.

Key takeaways from Niebles's segment:

- The next data bottleneck is not only more text but better multimodal grounding in the physical world.
- Smart-glasses and robot-assistant scenarios require space-time references, cross-modal reasoning, long-video understanding, and predictive action.
- High-value capabilities often fail because the needed training data is missing, not because the architecture is fundamentally incapable.
- Automatic data generation pipelines can synthesize supervision for space-time referencing tasks.
- Cross-modal reasoning benchmarks can be bootstrapped from single-modality datasets using language as a bridge.
- Long-horizon perception requires active rather than passive video understanding.
- The broader lesson is that ambient intelligence will depend on deliberately engineered data rather than hoping web-scale corpora cover physical-world tasks.
- This is especially relevant to interests in robotics and world models.

### 4. Fred Sala — The Art & Science of Benchmarking Agents

Sala's talk is the workshop's cleanest argument that evaluation is itself a data problem.
He treats benchmarks as artifacts whose quality depends on both scientific rigor and a clear thesis about what future capability matters.

Key takeaways from Sala's segment:

- Open benchmarks still shape the field, even if benchmaxing remains a risk.
- High-quality evaluation requires correctness, diversity, difficulty, and robust scoring methodology.
- Great benchmarks also require a forward-looking thesis about where the field is going.
- Agent benchmarks should be characterized by environment complexity, autonomy horizon, and output complexity.
- Tool use and long iterative tasks are especially important for realistic agent evaluation.
- Benchmark design should include frictionless interfaces so researchers can actually use the benchmark.
- The proposed “slopcode” direction is interesting because it evaluates iterative degradation, not just single-turn success.
- This is directly relevant to DATA-FM because benchmark construction determines what the community thinks progress looks like.

## Themes & Takeaways

### Interpretability

Interpretability in DATA-FM appears first as dataset transparency.

- Mirzasoleiman asks which examples are actually teaching the model something new.
- Min asks which pieces of knowledge live in which data silos.
- Sala asks whether benchmark items really measure what they claim to measure.
- Niebles asks whether a system can identify which modality contains the answer.
- In all four cases, interpretability is about tracing capability back to data design choices.
- This is less mechanistic interpretability and more pipeline interpretability.
- That perspective is valuable because it makes upstream design choices legible.

### Human-AI feedback loops

Human feedback shows up in both training and evaluation.

- Mirzasoleiman's framing of post-training implies richer supervision than simple next-token prediction.
- RL and SFT respond differently to difficulty and data volume, so feedback design matters.
- Min's fragmentation story implies organizations may contribute model updates instead of raw data.
- Niebles uses human-in-the-loop collection and curation to build targeted multimodal datasets.
- Sala emphasizes that benchmarks are social coordination tools, not only measurement tools.
- The overall message is that human judgment enters through curation, verification, and benchmark design.

### Uncertainty estimation

Uncertainty is not always explicit, but it sits under several talks.

- Mirzasoleiman's warning about overthinking is effectively a warning about miscalibrated confidence.
- Better data should help models know what they know and what they do not.
- Benchmark construction also depends on uncertainty: ambiguous questions degrade evaluation quality.
- In multimodal settings, selecting the right modality is partly an uncertainty-routing problem.
- Privacy and copyright risks are also uncertainty problems, since developers often do not know what exactly a model memorized.
- DATA-FM suggests that uncertainty work should connect more directly to data selection and filtering.

### Concept representation learning

Several talks suggest that higher-level structure in data matters more than raw scale.

- Mirzasoleiman focuses on hard, diverse reasoning traces rather than indiscriminate volume.
- Min's router-embedding story is about keeping domain knowledge modular and compositional.
- Niebles's synthetic pipelines build task-relevant structures such as space-time references.
- Sala's benchmark taxonomy also depends on structured task decomposition.
- The workshop therefore points toward concept-oriented curation rather than purely scalar quality scores.
- That is a useful direction for anyone interested in representation learning grounded in human-meaningful distinctions.

### Causal inference

The workshop is not centrally about causal inference, but causal questions emerge naturally.

- Mirzasoleiman distinguishes what happens when you intervene at training time versus test time.
- Min asks what training architectures preserve or remove the effect of specific data owners.
- Niebles's physical-world framing is explicitly about action, consequences, and environmental context.
- Sala's benchmark philosophy asks which interventions on task design will actually expose capability gaps.
- More broadly, DATA-FM treats data as an intervention lever rather than as passive input.

### Robotics

Robotics mainly enters through Niebles, but it changes the whole workshop's texture.

- It grounds the idea that future FM data may come from sensors rather than documents.
- It raises stronger requirements for multimodal alignment and temporal grounding.
- It makes active perception and long-horizon memory immediate necessities.
- It also highlights that web-trained agent evaluations may miss the hardest physical-world problems.
- For colleagues working on robotics, DATA-FM is a reminder that data pipelines are as strategic as model architectures.

### World models

World-model ideas show up as demands on data, not just on model classes.

- Niebles argues that physical-world intelligence needs data that supports state tracking, temporal reference, and predictive action.
- Long-video reasoning and active perception are proto-world-model capabilities.
- Mirzasoleiman's discussion of reasoning traces suggests internal “thinking” data may shape how a model simulates futures.
- Even benchmark construction in Sala's talk implicitly asks how well an agent represents environment dynamics over long horizons.
- DATA-FM therefore complements world-model research by asking what supervision those systems require.

### Steering techniques

Steering appears through data choices rather than only prompt tricks.

- Mirzasoleiman steers model behavior by selecting the right kind of post-training data.
- Min steers which knowledge is active through MOE routing and modularity.
- Niebles steers capability emergence by generating targeted supervision for specific multimodal skills.
- Sala steers community effort by creating benchmarks that reward the right behaviors.
- This is a useful broadening of the steering concept: data curation is itself a steering mechanism.

## Connections to PAI Research

DATA-FM matters because it shows that many core research interests are now data-engineering questions as much as modeling questions.

### For the core agenda

- Interpretability work can benefit from better provenance over which data teaches which behavior.
- Human-AI feedback research can gain from more deliberate post-training data construction.
- Uncertainty estimation should be linked to data ambiguity, benchmark validity, and overthinking failure modes.
- Concept learning appears in the move from scalar data scores to structured property annotations and domain modules.
- Causal inference becomes concrete when we treat curation, mixture, and routing as interventions.

### For robotics, world models, and steering

- Niebles makes a strong case that robotics progress depends on generating the right multimodal supervision.
- Long-video perception and cross-modal alignment are immediate prerequisites for embodied assistants.
- Min shows a promising route for combining fragmented specialist data without centralizing it.
- Mirzasoleiman highlights that data for reasoning should be matched to the current model, not chosen once and for all.
- Sala reminds us that evaluation datasets steer research directions just as strongly as training data.

### Practical opportunities

- Build evaluation sets that expose overthinking rather than only average accuracy.
- Study domain-specific modular experts as a vehicle for safe collaboration across data silos.
- Generate targeted multimodal supervision for embodied assistants.
- Connect data-property annotations to uncertainty, safety, and calibration metrics.
- Treat benchmark creation as part of the research pipeline, not only as downstream reporting.

## Signals from Contributed Talks and Posters

The workshop's oral and poster program made the invited-talk themes more concrete.
It also revealed which data problems the community currently sees as most urgent.

### Contributed talks that reinforce the main agenda

- **Olmix** treats data mixing as a dynamic engineering problem rather than a one-shot optimization.
- **The Capability Frontier** argues that single-model, single-run evaluations drastically understate achievable performance.
- **Cram Less to Fit More** shows that pruning data can improve factual memorization rather than only reduce cost.
- **Anchored Decoding** turns copyright mitigation into an inference-time data-distribution problem.
- **MaD-Mix** extends mixture design into multimodal settings where manual tuning is even less viable.
- **propella-1** argues for multidimensional annotation instead of single scalar “quality” scores.

### Poster-level signals worth tracking

- Many posters focus on synthetic data verification rather than synthetic data generation alone.
- Several contributions study dataset coverage, domain splitting, and relational benchmarks, suggesting that data structure matters as much as scale.
- Privacy, copyright, and unlearning appear repeatedly, reinforcing that “better data” is often legally constrained data.
- Agent-evaluation datasets appear throughout the poster list, showing that data-centric work is now inseparable from agentic evaluation.
- Multiple papers revisit memorization, fact retention, and long-tail knowledge, suggesting that factuality is still partly a data-distribution problem.
- The poster list also contains work on instruction tuning, active learning, and online reweighting, which together suggest a move toward adaptive curation loops.
- There is a noticeable shift away from universal quality scores toward compositional, property-based data analysis.
- Overall, the broader program makes DATA-FM feel less like a niche “dataset workshop” and more like a systems workshop about the information pipeline of modern AI.

## Why this workshop matters now

- Post-training has made data quality visible again after a period where model scale dominated the conversation.
- Agents and multimodal systems create new data requirements that public web text does not satisfy.
- Evaluation crises are increasingly data crises: ambiguous or stale benchmarks distort perceived progress.
- Private, fragmented data is becoming strategically important for both research and product development.
- Data engineering is no longer downstream support work; it is becoming one of the main levers of capability and safety.

## Reading the workshop as a whole

Another useful way to read DATA-FM is as a map of where foundation-model progress is likely to become bottlenecked next.

- Pretraining alone no longer dominates the conversation.
- Post-training data is becoming highly strategic.
- Multimodal systems expose supervision gaps that text-only pipelines can hide.
- Private and proprietary corpora are moving from edge cases to central resources.
- Benchmarks increasingly need the same care as training datasets.
- The most promising methods often combine selection, mixture design, and targeted synthetic generation.
- Data provenance and controllability are becoming capability issues, not only governance issues.
- In that sense, DATA-FM is really about the operating system of modern model development.

## One-sentence synthesis

DATA-FM argues that the next leap in foundation models will come less from blindly adding parameters and more from making data pipelines more selective, modular, lawful, and evaluation-aware.

- The workshop is therefore about how data pipelines shape capability, safety, and measurement at once.
- That broader systems view is what makes the program unusually timely.

## Open Questions

- How should we choose post-training data as models become stronger and their failure modes shift?
- Can modular training on fragmented private data become a standard recipe for open-model development?
- What is the best way to measure whether a model actually uses multimodal evidence rather than language shortcuts?
- When does more reasoning data improve generalization, and when does it induce overthinking?
- How should benchmarks evolve fast enough to remain unsaturated without becoming arbitrary?
- Can synthetic multimodal pipelines produce the kinds of data needed for robotics-scale assistants?
- What data properties matter most for steering, safety, and personalization in agent systems?
- How should copyright and privacy constraints reshape the next generation of FM training pipelines?

## Sources

- [Workshop page](../../raw/iclr-2026-workshop-data-fm.md) — workshop description, invited slots, oral-paper abstracts, and benchmark/data curation themes.
- [Workshop recording capture](../../raw/iclr-2026-workshop-data-fm-talk/README.md) — metadata for the recorded livestream.
- [Workshop transcript](../../raw/iclr-2026-workshop-data-fm-talk/transcript.md) — Baharan Mirzasoleiman, Sewon Min, Juan Carlos Niebles, and Fred Sala segments used in this synthesis.
