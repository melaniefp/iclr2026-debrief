---
title: "Affective Computing"
type: concept
tags:
  - affective-computing
  - human-robot-interaction
  - personalization
related:
  - "wiki/concepts/human-robot-interaction.md"
  - "wiki/concepts/socially-assistive-robotics.md"
  - "wiki/articles/materic-robotics-keynote.md"
sources:
  - "raw/challenges-human-centered-ai-robotics-talk"
---

# Affective Computing

Affective computing is the study and development of systems that can recognize, interpret, process, and simulate human affects (emotions, moods, personality). It bridges AI, psychology, and cognitive science to enable machines to understand and respond to the socio-emotional dimensions of human behavior.

## Key ideas

- Real-time affect recognition remains a hard problem — specialized deep models (OpenFace, OpenSmile, OpenPose) still outperform foundation models for personalized affect recognition
- Low-level features (lip position, facial landmarks) are detectable by most models, but mapping these to high-level features (intent, emotional state) requires contextual reasoning that large models still struggle with
- Subtle interaction cues (mother-infant smile patterns, prosodic interruption patterns) can predict mental health states and developmental outcomes with high accuracy
- Personality modeling using psychometrically grounded methods (Big Five) produces more stable and predictive agent behavior than shallow prompting of LLMs
- Model-based personality simulation does not fully replicate human personality dynamics — e.g., neuroticism predicts dispute outcomes in humans, while extraversion and agreeableness are better predictors for models
- The sparse, noisy, high-variance nature of behavioral data makes this domain particularly challenging for ML — individual-level fine-tuning with small personal datasets often outperforms population-level models

## Sources

- [Matarić ICLR 2026 keynote](../../raw/challenges-human-centered-ai-robotics-talk/README.md) — Affect recognition limitations, personality modeling for agents, and real-world behavioral data challenges

## Related concepts

- [Human-Robot Interaction](human-robot-interaction.md)
- [Socially Assistive Robotics](socially-assistive-robotics.md)
