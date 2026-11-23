---
title: "Capability #12 — Episodic / Observational Memory"
cap_number: 12
subsystem: "4.2 State"
status: "partial"
permalink: /capabilities/12-episodic-observational-memory/
description: "Capability #12 — Episodic / Observational Memory — Partially Implemented in POCLI."
---

## What It Is

Captures recurring behavioral observations, lessons learned, and historical failure/success episodes across sessions so agents improve over time.

## Why It Matters

Without episodic memory, agents repeatedly hit the same environment quirks, build flags, or project-specific pitfalls in every new session.

## Implementation Status in POCLI

**Status:** Partially Implemented

Partially implemented: the `AGENT` and `PROJECT` memory layers in `PoCliDatabase` (`src/storage/database.ts`) persist cross-session observations and project notes.

### Pending / Roadmap

Automated post-session reflection pipelines that distill recurring errors and verified fixes into structured episodic entries.
