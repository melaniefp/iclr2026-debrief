---
title: "Open-Source AI"
type: concept
tags:
  - open-source
  - frontier-models
  - reproducibility
  - ai-policy
related:
  - "wiki/concepts/marin-project.md"
  - "wiki/concepts/neural-scaling-laws.md"
  - "wiki/articles/marin-open-development-frontier-ai.md"
sources:
  - "raw/iclr-2026-invited-talk-marin-open-development-frontier-ai-talk/"
---

# Open-Source AI

Open-source AI refers to the practice of making the full stack of an AI system — model weights, training code, data recipes, and development process — publicly available. The term exists on a spectrum from closed APIs, through open-weight releases (e.g., Llama), to true open-source (code + data, e.g., OLMo, Nemotron), to open development where the entire research process is conducted in public.

## Key ideas

- **Taxonomy of openness**: Closed → open-weight → open-source → open development. Each level increases transparency and reproducibility but also exposes more of the development process.
- **Open-weight ≠ open-source**: Models like Llama release weights but not training code or data, analogous to distributing a binary executable without source code.
- **Open development**: Goes beyond releasing artifacts by making the entire research process visible — experiments, failures, design rationales, and community contributions happen in the open (e.g., Marin on GitHub).
- **Historical parallel**: Percy Liang draws a parallel between AI in 2026 and software in 1999, at the inflection point where open-source began to dominate. AI followed a similar arc: open in early research, closed during commercialization, and now potentially reopening.
- **Community leverage**: Open datasets are "renewable resources" — they can be reused across many training runs, whereas compute is consumed. This makes data curation a high-leverage community activity.

## Sources

- [Marin invited talk (transcript + slides)](../../raw/iclr-2026-invited-talk-marin-open-development-frontier-ai-talk/README.md) — Liang's ICLR 2026 keynote; introduces the taxonomy and argues for open development

## Related concepts

- [Marin Project](marin-project.md)
- [Neural Scaling Laws](neural-scaling-laws.md)
