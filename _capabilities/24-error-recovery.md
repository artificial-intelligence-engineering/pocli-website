---
title: "Capability #24 — Error Recovery"
cap_number: 24
subsystem: "4.5 Session Lifecycle"
status: "implemented"
permalink: /capabilities/24-error-recovery/
description: "Capability #24 — Error Recovery — Implemented in POCLI."
---

## What It Is

Gracefully detects and recovers from transient failures—LLM rate limits (HTTP 429), upstream 503 outages, network timeouts, and stalled workers.

## Why It Matters

External LLM APIs fail frequently under load; without automated recovery, multi-step engineering sessions abort abruptly.

## Implementation Status in POCLI

**Status:** Implemented

Implemented in `LLMRouter` (`src/runtime/llm-router.ts`) with sliding-window quota tracking, provider cooldown timers, and automatic HTTP 429/503/timeout cascade failover, paired with 120s per-turn worker timeouts in `PersistentAgentRuntime`.

### Pending / Roadmap

Per-error exponential backoff with jitter prior to failover and semantic stuck-loop detection.
