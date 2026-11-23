---
title: "Capability #4 — Plugins & Skills"
cap_number: 4
subsystem: "4.1 Instructions"
status: "partial"
permalink: /capabilities/04-plugins-skills/
description: "Capability #4 — Plugins & Skills — Partially Implemented in POCLI."
---

## What It Is

Declarative extension points that package reusable instructions, role workflows, lifecycle hooks, and external integrations without modifying core harness code.

## Why It Matters

Teams need to adapt coding standards, domain playbooks, and tool integrations without forking the harness runtime.

## Implementation Status in POCLI

**Status:** Partially Implemented

Partially implemented: `McpRegistry` (`src/runtime/mcp-client.ts`) attaches external MCP servers over JSON-RPC 2.0 stdio with per-role ACLs, and `src/runtime/harnesses.ts` loads custom user prompt overrides from `$HOME/.pocli/behavior/system/<role>.md`.

### Pending / Roadmap

Declarative plugin package loader, dynamic `SKILL.md` skill registry with lifecycle hooks, and remote HTTP/SSE MCP server transport.

## References

- [Model Context Protocol (MCP) — Architecture Overview](https://modelcontextprotocol.io/docs/concepts/architecture) — Open standard for decoupling external tool and resource servers from agent runtimes.
- [Anthropic — Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) — Discusses composable workflows and declarative extensions over monolithic frameworks.
- [AGENTS.md Open Format](https://agents.md/) — Emerging convention for repository-level declarative agent instructions and project rules.
