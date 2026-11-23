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

## References

- [OWASP Top 10 for Large Language Model Applications (LLM06: Excessive Agency)](https://genai.owasp.org/llmrisk/llm06-excessive-agency/) — Security taxonomy highlighting least-privilege permissions and human approval gates.
- [OpenAI — A Practical Guide to Building Agents (Guardrails & Human Intervention)](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf) — Defines tiered risk guardrails and mandatory human-in-the-loop checkpoints.
- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — Governance framework for human oversight, accountability, and controlled AI autonomy.
