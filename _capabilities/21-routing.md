---
title: "Capability #21 — Routing"
cap_number: 21
subsystem: "4.4 Scope"
status: "implemented"
permalink: /capabilities/21-routing/
description: "Capability #21 — Routing — Implemented in POCLI."
---

## What It Is

Deterministic control-flow logic that decides which workflow phase, specialist role, or execution path is permitted next—and blocks invalid transitions.

## Why It Matters

Leaving workflow routing entirely to the LLM lets agents skip architecture review, jump straight to coding, or bypass QA verification.

## Implementation Status in POCLI

**Status:** Implemented

Implemented in `src/core/workflow.ts` (8-phase SDLC state machine + `AuthorityGuard`) and `PoCliOrchestrator` (`src/runtime/orchestrator.ts`), which enforce valid phase transitions and role routing deterministically.

### Pending / Roadmap

Configurable workflow graph definitions allowing teams to customize or extend the default 8-phase SDLC.
