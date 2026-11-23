---
title: "Capability #39 — Capability Seams"
cap_number: 39
subsystem: "4.6 Pure Operational Runtime Layer"
status: "implemented"
permalink: /capabilities/39-capability-seams/
description: "Capability #39 — Capability Seams — Implemented in POCLI."
---

## What It Is

Clean architectural boundaries (interfaces and adapters) decoupling LLM providers, sandboxes, storage engines, and external tool registries from core orchestration logic.

## Why It Matters

AI tooling evolves rapidly; clean seams allow swapping models, runtimes, or isolation backends without rewriting the harness.

## Implementation Status in POCLI

**Status:** Implemented

Implemented throughout POCLI's modular architecture: `LLMGateway` / `LLMRouter` (model seam), `src/local/adapters/llamacpp.ts` (local inference seam), `LinuxAgentProcessRunner` (Bubblewrap/Podman sandbox seam), `McpRegistry` (MCP tool seam), and `PoCliDatabase` (SQLite persistence seam).

### Pending / Roadmap

Publishing formal TypeScript plugin SDK interfaces so third-party adapters can be loaded dynamically out-of-tree.
