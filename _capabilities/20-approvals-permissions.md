---
title: "Capability #20 — Approvals & Permissions"
cap_number: 20
subsystem: "4.4 Scope"
status: "implemented"
permalink: /capabilities/20-approvals-permissions/
description: "Capability #20 — Approvals & Permissions — Implemented in POCLI."
---

## What It Is

Hard authority boundaries and Human-in-the-Loop (HITL) approval gates requiring explicit human sign-off before high-impact transitions or mutations.

## Why It Matters

Autonomous agents should draft, analyze, and test—but the human Product Owner must retain sovereign approval over requirements, architecture, and final delivery.

## Implementation Status in POCLI

**Status:** Implemented

Implemented via `AuthorityGuard` (`src/core/workflow.ts`), which deterministically validates role permissions and artifact ownership, combined with mandatory Product Owner HITL gates (`/approve` and `/accept`).

### Pending / Roadmap

Per-command interactive risk-tiered approval prompts for ad-hoc destructive shell operations.
