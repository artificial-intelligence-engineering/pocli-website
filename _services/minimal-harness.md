---
title: "Minimal Harness & Token Efficiency"
weight: 1
---

Inspired by **Pi (`pi-mono`)** and empirical findings from *Harness Engineering* (`arXiv:2609.00006`), **POCLI** replaces monolithic 15,000+ token prompts with role-scoped harnesses of **150–250 tokens**.

## Why Prompt Size Matters

Every token in a system prompt is re-processed on every conversational turn, multiplying API cost and Time-To-First-Token (TTFT)—especially on local LLMs (`Ollama`, `llama.cpp`) or free API tiers.

| Environment | System Prompt Overhead | Design Approach |
| :--- | :--- | :--- |
| **Claude Code** | ~25,000 tokens | Monolithic tool manuals and style rules |
| **OpenCode / Codex** | 10,000 – 15,000 tokens | Heavy multi-tool JSON schemas |
| **Pi Agent** | 500 – 900 tokens | Minimalist core guidelines |
| **POCLI** | **150 – 250 tokens** | **Ultra-concise, role-scoped harnesses** |

## Preserving 90–95% of Your Context Window

- Each agent receives only the tools required for its role (`Architect`: ~140 tokens, `Developer`: ~105 tokens, `QA`: ~70 tokens, `PM`: ~130 tokens).
- Total turn payload averages **600–1,200 tokens**, yielding **sub-second TTFT** while leaving **90–95% of context capacity** for source code, diffs, and RAG citations.
- Prompts reside cleanly in `behavior/system/*.md` and support user-level overrides in `$HOME/.pocli/behavior/system/`.

