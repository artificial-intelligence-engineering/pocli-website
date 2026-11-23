---
title: "Capability #8 — Layered Memory"
cap_number: 8
subsystem: "4.2 State"
status: "implemented"
permalink: /capabilities/08-layered-memory/
description: "Capability #8 — Layered Memory — Implemented in POCLI."
---

## What It Is

Separates agent memory into distinct scopes and lifetimes (conversational, working, project-wide, and agent-specific) rather than dumping everything into one flat transcript.

## Why It Matters

Short-lived debugging notes should not pollute permanent architectural constraints, while project conventions must survive across sessions and roles.

## Implementation Status in POCLI

**Status:** Implemented

Implemented in `PoCliDatabase` (`src/storage/database.ts`) with a **4-layer memory architecture** (`CONVERSATIONAL`, `WORKING`, `PROJECT`, `AGENT`) persisted in SQLite and selectively assembled into Tier 2 of each role's context window.

### Pending / Roadmap

Automated memory decay/pruning policies for stale `WORKING` entries.
