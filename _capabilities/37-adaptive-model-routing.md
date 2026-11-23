---
title: "Capability #37 — Adaptive Model Routing"
cap_number: 37
subsystem: "4.6 Pure Operational Runtime Layer"
status: "implemented"
permalink: /capabilities/37-adaptive-model-routing/
description: "Capability #37 — Adaptive Model Routing — Implemented in POCLI."
---

## What It Is

Dynamically selects the best model and provider per task based on capability requirements, latency, quota headroom, and recent error health.

## Why It Matters

Heavy reasoning tasks need frontier models while routine formatting or fast iterations benefit from low-latency or local models.

## Implementation Status in POCLI

**Status:** Implemented

Implemented in `LLMRouter` (`src/runtime/llm-router.ts`) with routing presets (`auto:smart`, `auto:fast`, `auto:reliable`), RPM/RPD/TPM/TPD sliding-window quota tracking, cooldown scoring, and local model integration (`src/local/local-manager.ts`).

### Pending / Roadmap

Automated shadow/canary routing evaluations to tune candidate scoring empirically.

## References

- [Ong et al. — RouteLLM: Learning to Route LLMs with Preference Data (arXiv:2406.18665)](https://arxiv.org/abs/2406.18665) — Research demonstrating dynamic routing between strong and fast/cheap models to cut cost without losing quality.
- [Chen et al. — FrugalGPT: How to Use Large Language Models While Reducing Cost and Improving Performance (arXiv:2305.05176)](https://arxiv.org/abs/2305.05176) — Introduces LLM cascades and adaptive model selection strategies.
- [Slivkins — Introduction to Multi-Armed Bandits (arXiv:1904.07272)](https://arxiv.org/abs/1904.07272) — Theoretical foundation for bandit-based adaptive routing under latency and reliability uncertainty.
