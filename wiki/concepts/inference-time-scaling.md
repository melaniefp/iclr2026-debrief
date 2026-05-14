---
title: "Inference-Time Scaling"
type: "concept"
tags: [inference-time-scaling, search, reasoning, alignment]
related:
  - "wiki/concepts/reward-hacking.md"
  - "wiki/concepts/uncertainty-in-llms.md"
  - "wiki/articles/icbinb-llms-workshop.md"
  - "wiki/articles/scale-ai-eval-rl-talk.md"
  - "wiki/papers/uncertainty-aware-tree-search.md"
sources:
  - "raw/uncertainty-tree-openreview.md"
  - "raw/iclr-2026-workshop-icbinb-llms.md"
  - "raw/iclr-2026-workshop-icbinb-llms-talk/transcript.md"
  - "raw/scale-ai-new-frontier-eval-rl-expo-talk.md"
---

# Inference-Time Scaling

## Definition

Inference-time scaling is the strategy of spending extra computation at test time
— through sampling, search, tool use, verification, or deliberation — to improve
model outputs without retraining the base model. It has become a major paradigm
for reasoning systems because it promises capability gains on demand.

ICLR 2026 also highlighted the limits of that promise. The
[uncertainty-aware tree search paper](../papers/uncertainty-aware-tree-search.md)
shows that search can drift into regions where reward and uncertainty models are
poorly calibrated, while the [ICBINB workshop article](../articles/icbinb-llms-workshop.md)
summarizes Adam Block's argument that best-of-N alignment can optimize the
wrong proxy more effectively as compute increases.

Inference-time scaling is therefore not just a capability technique. It is also
a problem in oversight, uncertainty, and evaluation design.

## Key Ideas

- **Extra compute can buy better reasoning**: sampling and search can uncover
  better trajectories than greedy decoding.
- **Proxy quality is the bottleneck**: process reward models and judges must stay
  reliable under the states induced by deeper search.
- **Search changes the distribution**: the branches explored at large budgets are
  often unlike the data used to train the scorer.
- **Uncertainty should guide exploration**: in principle, high-uncertainty nodes
  deserve different search behavior than low-uncertainty ones.
- **More compute is not monotonic**: ICLR 2026 repeatedly showed regimes where
  larger search budgets worsen true performance.
- **Evaluation becomes part of the algorithm**: rubrics, verifiers, and judges
  are not external diagnostics once they control search.

## Related Work at ICLR 2026

- [Challenges in Inference-Time Scaling with Uncertainty-Aware Tree Search](../papers/uncertainty-aware-tree-search.md)
  is a clear negative result on uncertainty-guided search under distribution
  shift.
- [Workshop: I Can't Believe It's Not Better](../articles/icbinb-llms-workshop.md)
  frames inference-time alignment as a balance between coverage, reward-model
  quality, and reward hacking risk.
- [Scale AI on Evaluation and RL Frontiers](../articles/scale-ai-eval-rl-talk.md)
  argues that long-horizon progress is bottlenecked by verification asymmetry and
  richer evaluative environments.
- [Reward Hacking](reward-hacking.md) captures the main failure mode when search
  exploits misaligned scorers instead of solving the intended task.

## Open Questions

- When does more inference-time compute improve the true objective rather than
  only the proxy objective?
- Which uncertainty models stay valid under the distribution shift induced by
  search itself?
- How should benchmark papers report the cost-quality trade-off of search-based
  methods?
- Can inference-time scaling be made reliably corrigible when the verifier is
  imperfect?
