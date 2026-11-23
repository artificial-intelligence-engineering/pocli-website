---
title: "Capability #32 — Cost Tracking"
cap_number: 32
subsystem: "4.6 Pure Operational Runtime Layer"
status: "partial"
permalink: /capabilities/32-cost-tracking/
description: "Capability #32 — Cost Tracking — Partially Implemented in POCLI."
---

## What It Is

Accounts for input/output tokens, cache savings, and monetary spend per turn, role, model, and project.

## Why It Matters

Autonomous multi-turn loops can burn significant API budget unnoticed unless token and cost budgets are tracked transparently.

## Implementation Status in POCLI

**Status:** Partially Implemented

Partially implemented: `PoCliDatabase` computes active and compaction-saved tokens across turns and displays token usage in the TUI.

### Pending / Roadmap

An exact per-model USD cost accounting ledger with configurable per-project budget caps and alerts.

## References

- [Kapoor et al. — AI Agents That Matter (arXiv:2407.01502)](https://arxiv.org/abs/2407.01502) — Emphasizes joint cost-accuracy Pareto frontiers rather than cost-blind accuracy metrics.
- [FinOps Foundation — Cloud & AI Cost Management Framework](https://www.finops.org/framework/) — Industry practices for unit-cost accounting, budgets, and usage attribution.
- [OpenAI Tokenizer & Usage Accounting](https://platform.openai.com/docs/guides/production-best-practices) — Practical guidance on monitoring token budgets and optimizing prompt costs.
