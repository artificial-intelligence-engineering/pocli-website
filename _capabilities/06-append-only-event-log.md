---
title: "Capability #6 — Append-Only Event Log"
cap_number: 6
subsystem: "4.1 Instructions"
status: "implemented"
permalink: /capabilities/06-append-only-event-log/
description: "Capability #6 — Append-Only Event Log — Implemented in POCLI."
---

## What It Is

Maintains an immutable, chronological record of all instructions, tool invocations, and state transitions received during a session.

## Why It Matters

Mutable histories destroy forensic visibility. An append-only log guarantees full auditability for compliance, debugging, and post-mortem analysis.

## Implementation Status in POCLI

**Status:** Implemented

Implemented in `PoCliDatabase` (`src/storage/database.ts`) and `PoCliCoordinator` (`src/runtime/coordinator.ts`). Conversation turns are stored append-only (compaction sets `compacted_into_id` without deleting rows), and `coordinator_audit_log` records every state mutation with `requestId`, role, action, and timestamp.

### Pending / Roadmap

Exporting the append-only event stream in standardized JSONL / OpenTelemetry event formats for external audit pipelines.
