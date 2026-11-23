---
title: "Capability #30 — Typed Tool Calling"
cap_number: 30
subsystem: "4.6 Pure Operational Runtime Layer"
status: "implemented"
permalink: /capabilities/30-typed-tool-calling/
description: "Capability #30 — Typed Tool Calling — Implemented in POCLI."
---

## What It Is

The deterministic agent ↔ world interface validating tool arguments against strict schemas before executing filesystem, artifact, test, or handoff actions.

## Why It Matters

Parsing unconstrained free-text commands breaks automation and introduces security and reliability bugs.

## Implementation Status in POCLI

**Status:** Implemented

Implemented in `LLMGateway` (`choiceMsg.tool_calls` merged with `extractToolCalls()`), backed by Zod schemas in `src/core/contracts.ts` and dispatched deterministically by `PoCliOrchestrator.executeAgentToolCalls()`.

### Pending / Roadmap

Passing full JSON Schema `tools[]` definitions natively in HTTP payloads for every provider adapter.
