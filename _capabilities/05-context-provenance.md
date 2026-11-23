---
title: "Capability #5 — Context Provenance"
cap_number: 5
subsystem: "4.1 Instructions"
status: "partial"
permalink: /capabilities/05-context-provenance/
description: "Capability #5 — Context Provenance — Partially Implemented in POCLI."
---

## What It Is

Tracks the exact origin, version, and hash of every piece of context injected into an agent turn so decisions can be audited back to authoritative sources.

## Why It Matters

When an agent makes an incorrect assumption, engineers need to know whether it came from a stale artifact, a user message, a RAG document, or model hallucination.

## Implementation Status in POCLI

**Status:** Partially Implemented

Partially implemented: normative artifacts are strictly versioned in SQLite (`database.ts`), and `NotebookRagEngine` (`src/runtime/notebook-rag.ts`) tracks SHA-256 content hashes and source citations for indexed workspace documents.

### Pending / Roadmap

A unified per-turn provenance manifest recording the exact source IDs, byte ranges, and token counts of every block injected into the prompt.
