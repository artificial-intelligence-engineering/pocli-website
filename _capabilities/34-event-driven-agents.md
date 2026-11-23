---
title: "Capability #34 — Event-Driven Agents"
cap_number: 34
subsystem: "4.6 Pure Operational Runtime Layer"
status: "not_implemented"
permalink: /capabilities/34-event-driven-agents/
description: "Capability #34 — Event-Driven Agents — Not Yet Implemented in POCLI."
---

## What It Is

Triggers agent workflows reactively in response to external events such as GitHub webhooks, CI failures, filesystem changes, or scheduled timers.

## Why It Matters

Not all engineering tasks start from an interactive terminal prompt; background triage and continuous verification require reactive triggers.

## Implementation Status in POCLI

**Status:** Not Yet Implemented

Not yet implemented. POCLI currently runs interactively through the TUI (`CommandCenterApp.tsx`) or via explicit CLI/headless invocations (`pocli e2e`).

### Pending / Roadmap

A daemon event bus supporting `fs.watch`, cron schedules, and webhook triggers wired into `PoCliOrchestrator`.
