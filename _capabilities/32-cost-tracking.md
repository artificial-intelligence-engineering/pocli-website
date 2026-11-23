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
