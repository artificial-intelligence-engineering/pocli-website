---
title: "Capability #17 — Failure Routing & Rollback"
cap_number: 17
subsystem: "4.3 Verification"
status: "partial"
permalink: /capabilities/17-failure-routing-rollback/
description: "Capability #17 — Failure Routing & Rollback — Partially Implemented in POCLI."
---

## What It Is

Defines deterministic recovery paths when tests, linters, or QA gates fail—either routing structured diagnostics back for targeted repair or rolling back unsafe changes.

## Why It Matters

Unchecked failures either stall the workflow or let broken code advance to downstream phases.

## Implementation Status in POCLI

**Status:** Partially Implemented

Partially implemented: `PoCliOrchestrator` (`src/runtime/orchestrator.ts`) routes failed QA verifications back to the Developer in bounded autonomous correction loops (`MAX_QA_CORRECTION_CYCLES = 3`) before escalating to the Product Owner.

### Pending / Roadmap

Automatic workspace snapshot/git rollback when a verification gate fails catastrophically or exhausts its retry budget.

## References

- [Anthropic — Building Effective Agents (Evaluator-Optimizer Loop)](https://www.anthropic.com/engineering/building-effective-agents) — Describes bounded feedback loops routing verification failures back to the generator.
- [Michael Nygard — Release It! (Circuit Breakers & Stability Patterns)](https://pragprog.com/titles/mnee2/release-it-second-edition/) — Classic stability patterns for bounding retries, isolating failures, and failing safely.
- [Git — Reset, Revert & Checkout Recovery](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified) — Reference on deterministic workspace rollback primitives in Git.
