---
title: "Capability #10 — Typed Handoffs"
cap_number: 10
subsystem: "4.2 State"
status: "implemented"
permalink: /capabilities/10-typed-handoffs/
description: "Capability #10 — Typed Handoffs — Implemented in POCLI."
---

## What It Is

Defines explicit, schema-validated continuity contracts when transferring work from one specialist agent or session to another.

## Why It Matters

Unstructured free-text handoffs drop acceptance criteria, file paths, or failure diagnostics when crossing role boundaries.

## Implementation Status in POCLI

**Status:** Implemented

Implemented via Zod schemas in `src/core/contracts.ts` and orchestrated by `PoCliOrchestrator` (`src/runtime/orchestrator.ts`) using typed inter-role handoffs (`[ARQ->DEV]`, `[DEV->QA]`, `[QA->ARQ]`) backed by versioned artifacts.

### Pending / Roadmap

User-customizable handoff templates for domain-specific specialist roles.

## References

- [OpenAI — A Practical Guide to Building Agents (PDF)](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf) — Covers structured handoffs and manager/decentralized orchestration patterns.
- [Cognition — Don't Build Multi-Agents](https://cognition.ai/blog/dont-build-multi-agents) — Analyzes why naive, lossy inter-agent handoffs fail and how full-context contracts mitigate drift.
- [Zod — TypeScript-First Schema Validation](https://zod.dev/) — Runtime schema validation library used to enforce typed handoff contracts.
