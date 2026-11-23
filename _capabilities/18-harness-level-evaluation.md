---
title: "Capability #18 — Harness-Level Evaluation"
cap_number: 18
subsystem: "4.3 Verification"
status: "implemented"
permalink: /capabilities/18-harness-level-evaluation/
description: "Capability #18 — Harness-Level Evaluation — Implemented in POCLI."
---

## What It Is

Evaluates the complete system (model + context assembly + tools + sandboxing + multi-agent handoffs + QA gates) rather than isolated single-prompt model scores.

## Why It Matters

As argued in *AI Agents That Matter* (Kapoor et al., 2024), real-world reliability depends on the full end-to-end harness, including cost and verification rigor.

## Implementation Status in POCLI

**Status:** Implemented

Implemented via `pocli e2e` (`src/runtime/headless-runner.ts`), `pocli tui-test`, and the autonomous QA pipeline running isolated Robot Framework suites plus Mutation Testing (`TC-MUT-001`).

### Pending / Roadmap

Publishing reproducible longitudinal scorecards comparing harness releases across cost, latency, and defect-escape rates.

## References

- [Kapoor et al. — AI Agents That Matter (arXiv:2407.01502)](https://arxiv.org/abs/2407.01502) — Argues that evaluation must measure the entire agent harness and its cost, not just the base LLM.
- [SWE-bench Verified (OpenAI & Princeton)](https://openai.com/index/introducing-swe-bench-verified/) — Human-validated end-to-end software engineering benchmark testing complete coding harnesses.
- [Robot Framework — Acceptance Testing & RPA](https://robotframework.org/) — External black-box acceptance testing engine used by POCLI's autonomous QA harness.
