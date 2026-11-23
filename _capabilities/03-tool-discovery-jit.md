---
title: "Capability #3 — Tool Discovery & JIT Loading"
cap_number: 3
subsystem: "4.1 Instructions"
status: "partial"
permalink: /capabilities/03-tool-discovery-jit/
description: "Capability #3 — Tool Discovery & JIT Loading — Partially Implemented in POCLI."
---

## What It Is

Exposes a curated catalog of tools to the agent and loads full tool schemas Just-In-Time (JIT) only when needed for the current role or task.

## Why It Matters

Injecting dozens of unused tool schemas into every prompt wastes thousands of tokens and degrades tool-selection accuracy.

## Implementation Status in POCLI

**Status:** Partially Implemented

Partially implemented: `src/runtime/harnesses.ts` restricts exposed tools per role via `allowedTools` (`architect`, `developer`, `qa`, `pm`), and `McpRegistry` (`src/runtime/mcp-client.ts`) discovers external MCP tools filtered by `allowedRoles`.

### Pending / Roadmap

True deferred / Just-In-Time (JIT) schema loading for large tool catalogs so unused MCP or internal tool definitions are fetched only on demand.

## References

- [Anthropic — Writing Effective Tools for AI Agents](https://www.anthropic.com/engineering/writing-tools-for-agents) — Best practices for concise tool catalogs, namespacing, and avoiding tool-bloat.
- [Model Context Protocol (MCP) — Tools Specification](https://modelcontextprotocol.io/docs/concepts/tools) — Standard protocol for dynamic tool discovery (`tools/list`) and typed invocation.
- [Anthropic — Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) — Covers Agent-Computer Interface (ACI) design and curated tool surfaces.
