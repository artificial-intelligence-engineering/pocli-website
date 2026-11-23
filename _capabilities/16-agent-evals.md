---
title: "Capability #16 — Agent Evals"
cap_number: 16
subsystem: "4.3 Verification"
status: "partial"
permalink: /capabilities/16-agent-evals/
description: "Capability #16 — Agent Evals — Partially Implemented in POCLI."
---

## What It Is

Quantitative evaluation benchmarks measuring model and role accuracy, tool-calling reliability, and output quality across standardized engineering tasks.

## Why It Matters

Swapping models or editing system prompts without empirical evals makes it impossible to distinguish genuine improvements from regressions.

## Implementation Status in POCLI

**Status:** Partially Implemented

Partially implemented: `pocli e2e` (`src/runtime/headless-runner.ts`) and QA validation suites verify task completion end to end on real scenarios.

### Pending / Roadmap

Automated multi-model eval harnesses scoring pass@k, tool-call precision, latency, and token cost across a versioned task dataset.
