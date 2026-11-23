---
title: "Capability #23 — Scope Control"
cap_number: 23
subsystem: "4.4 Scope"
status: "implemented"
permalink: /capabilities/23-scope-control/
description: "Capability #23 — Scope Control — Implemented in POCLI."
---

## What It Is

Strictly bounds which files, tools, and artifacts an agent may touch and constrains task size to prevent uncontrolled scope creep.

## Why It Matters

Without hard scope boundaries, coding agents refactor unrelated files, modify tests to pass falsely, or overwrite architectural specifications.

## Implementation Status in POCLI

**Status:** Implemented

Implemented through per-role `allowedTools` in `src/runtime/harnesses.ts`, workspace-scoped filesystem paths in `PoCliOrchestrator.executeAgentToolCalls()`, and strict artifact write ownership enforced by `AuthorityGuard` (`src/core/workflow.ts`).

### Pending / Roadmap

Declarative per-task file-glob write allowlists and diff-size circuit breakers.
