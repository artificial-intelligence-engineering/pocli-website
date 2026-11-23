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

## References

- [Michael Feathers — Working Effectively with Legacy Code (Seams)](https://www.oreilly.com/library/view/working-effectively-with/0131177052/) — Origin of the *seam* concept: a place where behavior can be swapped without editing core code.
- [Alistair Cockburn — Hexagonal Architecture (Ports and Adapters)](https://alistair.cockburn.us/hexagonal-architecture/) — Architectural pattern isolating domain orchestration from external providers, databases, and tools.
- [Martin Fowler — Inversion of Control Containers and the Dependency Injection Pattern](https://martinfowler.com/articles/injection.html) — Foundational guide to decoupling swappable adapters behind clean interfaces.
