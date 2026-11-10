---
title: "3-Tier Context & SQLite DAG"
weight: 2
---

Built on **Node.js Native SQLite (`node:sqlite`)** in `WAL + FTS5` mode, **POCLI** stores the entire engineering history in `$HOME/.pocli/pocli.sqlite` with zero C++ native build dependencies.

## 3-Tier Prompt Context Assembly

On every agent turn, `PoCliOrchestrator` assembles a cache-friendly prompt directly from SQLite:

1. **Tier 1 (Cacheable Normative Prefix):** Concise index of authoritative artifacts (`[ARCH-001 v1 | APPROVED]`, `[SPEC-001 v1]`) rather than full file dumps.
2. **Tier 2 (4-Layer Memory & Compaction Checkpoints):** Up to 8 persistent priority memories plus the latest structured `/compact` summary from `context_compactions`.
3. **Tier 3 (Active Recent Window):** Strictly the last **6 uncompacted leaf turns** from the Session Tree DAG (`parent_id` lineage).

## Interactive `pocli db` SQLite REPL

Query your engineering workspace at any time from the terminal or directly inside the TUI with `/db`:

```bash
pocli db path
pocli db ".tables"
pocli db "SELECT code, type, status FROM artifacts;" --format table
```

