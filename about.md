---
title: Architecture & Research
layout: page
description: "Modular runtime architecture, 3-tier context assembly, cascading system prompts, ADRs, and open-source research foundations behind POCLI."
bodyClass: page-about
---

POCLI is a native Linux TUI/CLI software engineering environment built on TypeScript, Ink, Yoga Layout, native Node.js SQLite (`WAL` + `FTS5`), and OS-level process sandboxing.

## 1. Execution Pipeline & Process Isolation

Static role harnesses (`behavior/system/*.md`, only **150–250 tokens** per agent) and dynamic project state from SQLite (`$HOME/.pocli/pocli.sqlite`) are assembled per turn into a bounded **600–1,200 token** context window and dispatched over `JSON-RPC 2.0` stdio to dedicated Linux child processes:

```text
behavior/system/*.md (150-250 tokens)
        +
SQLite Context (Tier 1 + Tier 2 Compaction + Tier 3 DAG)
        │
        ▼  src/runtime/orchestrator.ts
Linux Child Process (JSON-RPC 2.0 stdio | bwrap / OCI)
```

This multi-process design guarantees that agent inference never blocks the interactive fullscreen Ink Command Center and never leaks conversational state across roles.

---

## 2. Core Modules (`src/`)

| Module | Responsibility |
| :--- | :--- |
| `src/core/contracts.ts` & `workflow.ts` | Zod domain schemas, **8-phase SDLC state machine**, `AuthorityGuard`, and `en`/`es` i18n. |
| `src/storage/database.ts` | Native `node:sqlite` (`WAL` + `FTS5`), versioned artifacts with SHA-256 hashes, approvals, QA reports, and 4-layer memory. |
| `src/runtime/harnesses.ts` | Role harness registry with cascading resolution (`~/.pocli/behavior/system/` > repo `behavior/system/` > fallback). |
| `src/runtime/notebook-rag.ts` | Filesystem Knowledge Notebooks, incremental SHA-256 indexing, `fs.watch`, and hybrid `BM25 + vector cosine` retrieval. |
| `src/runtime/process-runner.ts` | Dedicated Linux child process spawning with `LOCAL_PROCESS`, Bubblewrap (`LINUX_BWRAP`), and Podman (`OCI_CONTAINER`). |
| `src/runtime/orchestrator.ts` & `pm-reporter.ts` | Multi-agent coordination, autonomous `[DEV <-> QA -> ARQ]` loops, and PM 100% HTML deliverables. |
| `src/tui/CommandCenterApp.tsx` | Fullscreen Ink UI with clean OpenCode-inspired startup view, `/` slash overlay, and `Ctrl+Tab` multipanel view. |

---

## 3. Architectural Decision Records (ADRs)

Full design decisions live in the main [`pocli`](https://github.com/artificial-intelligence-engineering/pocli/tree/main/docs/adr) repository:

- **ADR-000**: Open-Source Reference Benchmark Matrix (*OpenCode, Pi, Slipwright, AWS CAO, Open Orchestra, Open Notebook, TinySDLC*).
- **ADR-001**: Modular Architecture, `JSON-RPC 2.0` IPC, `node:sqlite` + `FTS5`, RAG Notebooks & Linux Sandboxing.
- **ADR-002**: Governed Agentic Development, Authority Boundaries & Non-Bypassable Human Gating.
- **ADR-003**: Multipanel Worker Runtime Status & Context/Memory Inspector.

---

## 4. Research Foundations

POCLI synthesizes proven engineering patterns rather than reinventing the wheel:

- **Harness Engineering ([arXiv:2609.00006](https://arxiv.org/abs/2609.00006))**: Theoretical basis for POCLI's minimal harness philosophy, role-scoped tools, and deterministic retrieval over bloated multi-agent frameworks.
- **Pi (`pi-mono`)**: Minimalist system prompt discipline, sub-second TTFT, Session Tree DAG (`parent_id`), and structured `/compact` checkpoints.
- **OpenCode**: Fullscreen terminal Command Center aesthetics, `/` command palette, and interactive `pocli db` SQLite REPL.
- **TinySDLC & Slipwright**: Strict *"No Self-Review"* enforcement and deterministic human-in-the-loop phase gating.
- **Grounded Citations ([arXiv:2311.09533](https://arxiv.org/abs/2311.09533))**: Inspiration for verifiable NotebookLM-style source citations (`[Notebook | Document | Section]`).
