---
title: "Capability #2 — Structured Compaction"
cap_number: 2
subsystem: "4.1 Instructions"
status: "implemented"
permalink: /capabilities/02-structured-compaction/
description: "Capability #2 — Structured Compaction — Implemented in POCLI."
---

## What It Is

Summarizes and compresses older conversation turns into structured checkpoints that preserve decisions, constraints, and open items while freeing prompt space.

## Why It Matters

Long engineering sessions inevitably exceed context limits. Naive truncation loses critical decisions; structured compaction preserves state continuity without erasing auditability.

## Implementation Status in POCLI

**Status:** Implemented

Implemented via the `/compact` command and the `context_compactions` table in `PoCliDatabase` (`src/storage/database.ts`). Compaction is **lossless**: historical messages are never deleted—instead they are linked via `compacted_into_id` while the structured summary is injected into Tier 2 of future turns.

### Pending / Roadmap

Automatic background compaction when active turn tokens cross a configurable percentage of the active model's context window.

## References

- [Anthropic — Effective Context Engineering for AI Agents (Compaction)](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — Details structured compaction strategies to preserve architectural decisions across long sessions.
- [Packer et al. — MemGPT: Towards LLMs as Operating Systems (arXiv:2310.08560)](https://arxiv.org/abs/2310.08560) — Foundational paper on virtual context management and paging/summarization out of active context.
- [OpenAI — Conversation State & Compaction Guide](https://platform.openai.com/docs/guides/conversation-state) — Practical patterns for managing long-running multi-turn state within context budgets.
