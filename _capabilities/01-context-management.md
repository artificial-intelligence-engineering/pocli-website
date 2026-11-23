---
title: "Capability #1 — Context Management"
cap_number: 1
subsystem: "4.1 Instructions"
status: "implemented"
permalink: /capabilities/01-context-management/
description: "Capability #1 — Context Management — Implemented in POCLI."
---

## What It Is

Deterministically controls what enters the LLM prompt on every turn and in what order: system instructions, normative project artifacts, layered memory, compaction checkpoints, active turns, and grounded retrieval passages.

## Why It Matters

Unbounded chat transcripts cause context rot (*lost in the middle*), silently drop architectural constraints, and waste token budget on stale or irrelevant tool output.

## Implementation Status in POCLI

**Status:** Implemented

Implemented in `PoCliDatabase.assembleAgentContextWindow()` (`src/storage/database.ts`), which builds a **3-tier context window**: (T1) a cache-friendly normative artifacts prefix (`REQ`, `ARCH`, etc.), (T2) 4-layer memory plus the latest compaction checkpoint, and (T3) active uncompacted conversation turns. `NotebookRagEngine` (`src/runtime/notebook-rag.ts`) injects grounded workspace documentation citations on demand.

### Pending / Roadmap

Automatic provider-threshold compaction triggered transparently before context saturation without requiring manual `/compact`.
