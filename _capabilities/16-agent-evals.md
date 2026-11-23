---
title: "Capability #16 — Agent Evals"
cap_number: 16
subsystem: "4.3 Verification"
status: "partial"
permalink: /capabilities/16-agent-evals/
description: "Capability #16 — Agent Evals — Partially Implemented in POCLI."
---

## What It Is

Quantitative evaluation benchmarks measuring model and role accuracy, tool-calling reliability, and output quality across standardized engineering tasks.

## Why It Matters

Swapping models or editing system prompts without empirical evals makes it impossible to distinguish genuine improvements from regressions.

## Implementation Status in POCLI

**Status:** Partially Implemented

Partially implemented: `pocli e2e` (`src/runtime/headless-runner.ts`) and QA validation suites verify task completion end to end on real scenarios.

### Pending / Roadmap

Automated multi-model eval harnesses scoring pass@k, tool-call precision, latency, and token cost across a versioned task dataset.

## References

- [Kapoor et al. — AI Agents That Matter (arXiv:2407.01502)](https://arxiv.org/abs/2407.01502) — Rigorous academic critique of agent benchmarks, cost-blind metrics, and evaluation methodology.
- [Anthropic — Demystifying Evals for AI Agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) — Practical guide to designing automated evals, graders, and regression suites for agents.
- [Chip Huyen — AI Engineering (O'Reilly, 2025)](https://www.oreilly.com/library/view/ai-engineering/9781098166298/) — Comprehensive engineering treatment of evaluation pipelines, rubrics, and LLM-as-a-judge tradeoffs.
