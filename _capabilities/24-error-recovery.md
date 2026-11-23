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

## References

- [AWS Architecture Blog — Timeouts, Retries, and Backoff with Jitter](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/) — Canonical engineering reference on resilient retry strategies and avoiding thundering herds.
- [IETF RFC 9110 — HTTP Semantics (429 Too Many Requests / 503 Service Unavailable)](https://httpwg.org/specs/rfc9110.html) — Standard specification for rate-limit and transient availability status codes.
- [Michael Nygard — Release It! (Stability Patterns)](https://pragprog.com/titles/mnee2/release-it-second-edition/) — Covers timeouts, bulkheads, circuit breakers, and graceful failover.
