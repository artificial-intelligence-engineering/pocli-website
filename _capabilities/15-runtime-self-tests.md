---
title: "Capability #15 — Runtime Self-Tests"
cap_number: 15
subsystem: "4.3 Verification"
status: "implemented"
permalink: /capabilities/15-runtime-self-tests/
description: "Capability #15 — Runtime Self-Tests — Implemented in POCLI."
---

## What It Is

Automated verification suites that test the harness itself—its state machine, SQLite persistence, tool dispatch, sandboxing, and TUI rendering.

## Why It Matters

If the deterministic envelope has bugs (e.g., a broken file filter or permission gate), even the smartest LLM cannot compensate for a faulty harness.

## Implementation Status in POCLI

**Status:** Implemented

Implemented with Vitest unit and integration suites, automated headless end-to-end verification (`pocli e2e` via `src/runtime/headless-runner.ts`), and Virtual TUI automated testing (`pocli tui-test`).

### Pending / Roadmap

Continuous regression benchmarking across every supported Linux sandbox backend (Bubblewrap and Podman) in CI.
