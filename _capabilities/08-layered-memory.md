---
title: "Capability #8 — Layered Memory"
cap_number: 8
subsystem: "4.2 State"
status: "implemented"
permalink: /capabilities/08-layered-memory/
description: "Capability #8 — Layered Memory — Implemented in POCLI."
---

## What It Is

Separates agent memory into distinct scopes and lifetimes (conversational, working, project-wide, and agent-specific) rather than dumping everything into one flat transcript.

## Why It Matters

Short-lived debugging notes should not pollute permanent architectural constraints, while project conventions must survive across sessions and roles.

## Implementation Status in POCLI

**Status:** Implemented

Implemented in `PoCliDatabase` (`src/storage/database.ts`) with a **4-layer memory architecture** (`CONVERSATIONAL`, `WORKING`, `PROJECT`, `AGENT`) persisted in SQLite and selectively assembled into Tier 2 of each role's context window.

### Pending / Roadmap

Automated memory decay/pruning policies for stale `WORKING` entries.

## References

- [Sumers et al. — Cognitive Architectures for Language Agents (CoALA, arXiv:2309.02427)](https://arxiv.org/abs/2309.02427) — Formal taxonomy separating working, episodic, semantic, and procedural memory in LLM agents.
- [Packer et al. — MemGPT: Towards LLMs as Operating Systems (arXiv:2310.08560)](https://arxiv.org/abs/2310.08560) — Introduces hierarchical memory tiers bridging limited prompt windows and persistent storage.
- [Park et al. — Generative Agents: Interactive Simulacra of Human Behavior (arXiv:2304.03442)](https://arxiv.org/abs/2304.03442) — Demonstrates structured memory streams, retrieval scoring, and reflection.
