---
title: "Summary: Marin — Open Development of Frontier AI (ICLR 2026 Invited Talk)"
type: summary
tags:
  - invited-talk
  - open-source
  - frontier-models
  - scaling-laws
  - reproducibility
related:
  - "wiki/concepts/open-source-ai.md"
  - "wiki/concepts/marin-project.md"
  - "wiki/concepts/neural-scaling-laws.md"
sources:
  - "raw/iclr-2026-invited-talk-marin-open-development-frontier-ai-talk/"
---

# Summary: Marin — Open Development of Frontier AI

Percy Liang's ICLR 2026 invited talk introduces Marin, an openly-developed language model project that makes every experiment, decision, and result public on GitHub — going beyond open-source to what he calls "open development."

Liang frames the core challenge around **algorithmic efficiency**: the goal of ML researchers is not just to build bigger models, but to create better learning algorithms that squeeze more performance out of a given compute budget. He reports that algorithmic efficiency has been doubling every eight months, and argues that the community can accelerate this further through three principles: open development, scaling laws, and predictability (preregistration).

The talk details Marin's journey from "YOLO expeditions" — ad-hoc training runs of 8B and 32B parameter models plagued by loss spikes, shuffling bugs, and numeric instability — to a disciplined **scaling recipe** approach. Key technical contributions include: (1) a "hyperball optimizer" that normalizes weight updates onto a hypersphere, yielding 20–30% speedups and stable hyperparameters across scales; (2) a principled scaling recipe where learning rate decreases with token count (proportional to $n^{-0.3}$); and (3) validated isoflop-based scaling laws that predicted final loss within 0.005 nats at 300× extrapolation from smaller models.

Liang advocates for **preregistration** of ML experiments — publicly predicting outcomes before runs complete — and demonstrates this with Marin's publicly posted loss predictions on GitHub. The project has expanded to mixture-of-experts architectures (achieving 3.76× speedups over dense models), audio modeling, and DNA sequence modeling, all using the same scaling infrastructure. The data strategy relies on community-curated datasets (18T tokens accumulated so far) rather than proprietary data.

The talk closes with a call to the ML community: think in terms of scaling recipes rather than individual runs, embrace open development as the natural evolution of open-source AI, and challenge yourself to preregister results. Liang draws a parallel between AI in 2026 and software in 1999 — at the inflection point where truly open models may become viable infrastructure.
