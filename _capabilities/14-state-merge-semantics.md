---
title: "Capability #14 — State Merge Semantics"
cap_number: 14
subsystem: "4.2 State"
status: "implemented"
permalink: /capabilities/14-state-merge-semantics/
description: "Capability #14 — State Merge Semantics — Implemented in POCLI."
---

## What It Is

Enforces deterministic rules for combining concurrent or sequential writes to shared project state without silent overwrites or corruption.

## Why It Matters

When multiple specialist workers operate on the same project, unsynchronized writes cause race conditions, lost artifact versions, and corrupted SQLite state.

## Implementation Status in POCLI

**Status:** Implemented

Implemented in `PoCliCoordinator` (`src/runtime/coordinator.ts`), which acts as the **Sole Write Owner** serializing SQLite mutations with idempotency keys (`requestId`) and optimistic concurrency checks (`expectedVersion`).

### Pending / Roadmap

Semantic 3-way merge policies for parallel workspace file edits once concurrent developer fan-out is added.
