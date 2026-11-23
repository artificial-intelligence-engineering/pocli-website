---
title: "Capability #27 — Bootstrap & Preflight"
cap_number: 27
subsystem: "4.5 Session Lifecycle"
status: "implemented"
permalink: /capabilities/27-bootstrap-preflight/
description: "Capability #27 — Bootstrap & Preflight — Implemented in POCLI."
---

## What It Is

Validates environment readiness—database migrations, credentials, sandbox binaries, local GPU/RAM capabilities, and workspace health—before starting agent execution.

## Why It Matters

Failing fast during preflight avoids burning LLM tokens on turns doomed to fail due to missing keys, broken tools, or unavailable sandboxes.

## Implementation Status in POCLI

**Status:** Implemented

Implemented across `src/cli.ts`, `src/core/auth.ts`, `src/core/lifecycle.ts`, `PoCliDatabase` schema initialization, and local hardware/compatibility inspection (`src/local/hardware.ts`, `src/local/compatibility.ts`).

### Pending / Roadmap

A dedicated `pocli doctor` diagnostic command printing a full preflight readiness checklist.
