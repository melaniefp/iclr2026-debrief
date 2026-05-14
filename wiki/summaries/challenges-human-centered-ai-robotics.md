---
title: "Summary: The Challenges of Human-Centered AI and Robotics"
type: summary
tags:
  - human-robot-interaction
  - socially-assistive-robotics
  - human-centered-ai
  - affective-computing
  - invited-talk
related:
  - "wiki/concepts/socially-assistive-robotics.md"
  - "wiki/concepts/human-robot-interaction.md"
  - "wiki/concepts/affective-computing.md"
sources:
  - "raw/challenges-human-centered-ai-robotics-talk"
---

# Summary: The Challenges of Human-Centered AI and Robotics

Maja Matarić's ICLR 2026 keynote argues that physical AI and robotics cannot succeed without addressing the social and socio-emotional dimensions of human-machine interaction — a component largely missing from current massive investments in humanoid robotics.

## Key arguments

Matarić contends that human intelligence evolved in the context of embodied, socially situated agents, and that AGI cannot be truly "general" without grounding in embodiment and socio-emotional understanding. She critiques the current focus on functional humanoid behavior (perception, locomotion, manipulation) while human-robot interaction (HRI) research remains an afterthought. Drawing on 25+ years of HRI research, she presents evidence that people do not simply accept robots because they are functional — expectations, personality matching, embodiment form, and social dynamics all profoundly shape outcomes.

## Socially assistive robotics

The core of Matarić's research program is **socially assistive robotics (SAR)**: robots that help people help themselves through social interaction rather than physical task completion. Key findings include: (1) physically co-present robots produce higher engagement, enjoyment, learning, and retention than screen-based interactions, supported by 50+ years of neuroscience evidence on embodied cognition; (2) low-cost, non-humanoid robots (sub-$300) are more scalable, less threatening, and create fewer unmet expectations than humanoids; and (3) personality matching between robot and user significantly increases exercise duration in stroke patients and engagement across populations.

## Real-world deployments and ML challenges

Matarić presented results from some of the largest real-world HRI studies, spanning infant motor development (using robot-sized "coaches" that babies can imitate), autism intervention in children's homes, dementia screening via natural conversation (published in Nature), and an NIH clinical trial placing 120+ robots in USC dorms for anxiety/depression support using cognitive behavioral therapy. A recurring ML theme is that foundation models remain poor at personalized affect recognition, real-time engagement prediction, and handling the sparse, noisy, high-variance data characteristic of behavioral health populations. Small specialized deep models consistently outperform large foundation models for these tasks, and individual-level fine-tuning with small amounts of personal data outperforms population-level transfer.

## Implications for the field

Matarić urged the ICLR audience to consider augmentation over replacement, emphasizing that therapist-client alignment — not the specific therapy modality — is the strongest predictor of therapeutic outcomes, and that chatbots do not achieve the same alignment as physically embodied agents. She called for more research on small-model/large-model interaction, real-time multimodal behavioral data collection, and embodied social AI as prerequisites for meaningful progress toward AGI and beneficial AI deployment.
