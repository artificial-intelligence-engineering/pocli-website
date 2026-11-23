---
title: "Capability #31 — Observability"
cap_number: 31
subsystem: "4.6 Pure Operational Runtime Layer"
status: "partial"
permalink: /capabilities/31-observability/
description: "Capability #31 — Observability — Partially Implemented in POCLI."
---

## What It Is

Cross-cutting structured logs, latency metrics, and execution traces giving operators full visibility into every turn, tool call, and provider request.

## Why It Matters

Without structured observability, diagnosing silent latency spikes, provider errors, or unexpected agent behavior is guesswork.

## Implementation Status in POCLI

**Status:** Partially Implemented

Partially implemented: `Logger` (`src/core/logger.ts`) writes ring-buffered rotating logs to `$HOME/.pocli/logs/pocli.log` (inspectable via `pocli logs`), and `LLMRouter` records per-provider `latencyMs`.

### Pending / Roadmap

Granular Time-To-First-Token (TTFT) TUI telemetry and OpenTelemetry (OTLP) span export.
