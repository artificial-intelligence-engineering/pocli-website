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

## References

- [Martin Fowler — Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html) — Classic architectural pattern capturing all state changes as an immutable append-only sequence of events.
- [Jay Kreps — The Log: What Every Software Engineer Should Know About Real-Time Data's Unifying Abstraction](https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying) — Deep dive into append-only logs as the foundation for durability, auditing, and replication.
- [SQLite Write-Ahead Logging (WAL)](https://www.sqlite.org/wal.html) — Technical documentation on SQLite WAL mode for concurrent reads and durable append-only transactions.
