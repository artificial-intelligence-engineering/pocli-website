---
title: "Capability #25 — Streaming & Cancellation"
cap_number: 25
subsystem: "4.5 Session Lifecycle"
status: "partial"
permalink: /capabilities/25-streaming-cancellation/
description: "Capability #25 — Streaming & Cancellation — Partially Implemented in POCLI."
---

## What It Is

Streams live incremental model output and tool progress to the user interface while allowing immediate, clean cancellation of in-flight turns.

## Why It Matters

Blocking UIs hide whether an agent is reasoning or hung, and forced kills (`Ctrl+C`) risk leaving orphaned subprocesses or half-written state.

## Implementation Status in POCLI

**Status:** Partially Implemented

Partially implemented: `PersistentAgentRuntime` streams incremental updates via JSON-RPC `agent.streamChunk` to `CommandCenterApp.tsx`, with per-turn timeout enforcement.

### Pending / Roadmap

Universal native HTTP SSE token-by-token streaming across every provider adapter and graceful mid-stream cooperative cancellation from the TUI.
