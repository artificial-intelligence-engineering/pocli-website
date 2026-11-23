---
title: "Capability #28 — Agent Loop"
cap_number: 28
subsystem: "4.6 Pure Operational Runtime Layer"
status: "implemented"
permalink: /capabilities/28-agent-loop/
description: "Capability #28 — Agent Loop — Implemented in POCLI."
---

## What It Is

The core execution cycle driving each agent turn: assemble context → call LLM → parse tool calls → execute tools → observe results → iterate or complete.

## Why It Matters

Without a bounded loop feeding execution observations back to the model, an LLM cannot self-correct or complete multi-step engineering tasks.

## Implementation Status in POCLI

**Status:** Implemented

Implemented in `PoCliOrchestrator` (`src/runtime/orchestrator.ts`) and `src/runtime/agent-worker.ts`, communicating over JSON-RPC 2.0 stdio with bounded correction cycles and per-turn timeouts.

### Pending / Roadmap

Semantic stuck-loop detection to abort automatically when an agent repeats identical failing tool calls.

## References

- [Yao et al. — ReAct: Synergizing Reasoning and Acting in Language Models (arXiv:2210.03629)](https://arxiv.org/abs/2210.03629) — Seminal paper formalizing the interleaved thought → action → observation agent loop.
- [Anthropic — Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) — Defines the canonical augmented-LLM loop with tools and environmental feedback.
- [Wang et al. — A Survey on LLM-based Autonomous Agents (arXiv:2308.11432)](https://arxiv.org/abs/2308.11432) — Comprehensive academic survey of autonomous agent control loops and architectures.
