---
title: "Capability #36 — Per-Role Snapshots"
cap_number: 36
subsystem: "4.6 Pure Operational Runtime Layer"
status: "partial"
permalink: /capabilities/36-per-role-snapshots/
description: "Capability #36 — Per-Role Snapshots — Partially Implemented in POCLI."
---

## What It Is

Captures and inspects the exact context, memory, and artifact view held by each specialist role at any point in a project.

## Why It Matters

Debugging multi-agent handoffs requires seeing precisely what the Architect, Developer, or QA agent actually saw at a given turn.

## Implementation Status in POCLI

**Status:** Partially Implemented

Partially implemented: each role maintains isolated conversation streams and memory layers in SQLite (`database.ts`), inspectable via `pocli db` (`db-repl.ts`).

### Pending / Roadmap

Immutable point-in-time per-role snapshot diffs and visual inspection commands in the TUI.
