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
