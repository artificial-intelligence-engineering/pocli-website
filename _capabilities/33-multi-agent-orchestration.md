---
title: "Capability #33 — Multi-Agent Orchestration"
cap_number: 33
subsystem: "4.6 Pure Operational Runtime Layer"
status: "implemented"
permalink: /capabilities/33-multi-agent-orchestration/
description: "Capability #33 — Multi-Agent Orchestration — Implemented in POCLI."
---

## What It Is

Coordinates multiple isolated specialist agents with distinct personas, tool allowlists, and verification responsibilities across a shared workflow.

## Why It Matters

A single generalist agent tends to grade its own homework and pollute its context with cross-role noise; role separation enforces independent verification.

## Implementation Status in POCLI

**Status:** Implemented

Implemented via `PersistentAgentRuntime` (`src/runtime/persistent-runtime.ts`) and `PoCliOrchestrator` (`src/runtime/orchestrator.ts`), coordinating isolated `architect`, `developer`, `qa`, and `pm` workers over JSON-RPC 2.0 with typed handoffs and zero cross-chat bloat.

### Pending / Roadmap

Concurrent fan-out / fan-in orchestration across multiple parallel developer workers.

## References

- [Anthropic — How We Built Our Multi-Agent Research System](https://www.anthropic.com/engineering/built-multi-agent-research-system) — Real-world engineering report detailing when and how multi-agent orchestration pays off.
- [Cognition — Don't Build Multi-Agents](https://cognition.ai/blog/dont-build-multi-agents) — Essential counterpoint warning against context fragmentation and poorly coordinated sub-agents.
- [Hong et al. — MetaGPT: Meta Programming for a Multi-Agent Collaborative Framework (arXiv:2308.00352)](https://arxiv.org/abs/2308.00352) — Encodes standard operating procedures (SOPs) across Product Manager, Architect, Engineer, and QA roles.
