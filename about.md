---
title: Architecture & Research
layout: page
description: "What a harness is, de facto references, neuro-symbolic foundations, the 5 fundamental subsystems, and how POCLI implements them."
bodyClass: page-about
---

POCLI is a harness. In this section, we examine what a harness is and how POCLI implements it.

---

## 1. What Is Harness Engineering?

### 1.1 Preface

**"Harness engineering"** as a named discipline does not yet have a single canonical paper or formal standard. It is an emerging engineering term (2024–2026) that currently lives primarily in engineering blogs, field reports, and open-source repositories rather than consolidated academic literature.

### 1.2 De Facto Industry & Academic References

1. **Anthropic — ["Building Effective Agents"](https://www.anthropic.com/engineering/building-effective-agents)** (Erik Schluntz & Barry Zhang, Dec 19, 2024): Engineering blog post (not a PDF) — the most widely cited practical reference in the field.
2. **Anthropic — ["Effective Context Engineering for AI Agents"](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)** (Anthropic Engineering, 2025): Key reference on curating bounded, high-signal context per turn.
3. **OpenAI — ["A Practical Guide to Building Agents"](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf)** (Official PDF, 2025; also available via [openai.com](https://openai.com/) → Business → Guides).
4. **Kapoor et al. — ["AI Agents That Matter"](https://arxiv.org/abs/2407.01502)** ([PDF](https://arxiv.org/pdf/2407.01502), Princeton, July 2024 — Sayash Kapoor, Benedikt Stroebl, Zachary S. Siegel, Nitya Nadgir, András Vécsey, Daniel Chen, Arvind Narayanan): The most cited academic paper on rigorous agent evaluation, critiquing benchmark flaws and cost-blind comparisons — the closest thing to an official paper on evaluating the *entire system* rather than just the model.
5. **Chip Huyen — ["AI Engineering"](https://www.oreilly.com/library/view/ai-engineering/9781098166298/)** (O'Reilly, Jan 2025; related free articles on [huyenchip.com](https://huyenchip.com/)): The most consolidated book covering evals, RAG, agents, and fine-tuning with production engineering rigor — covering the "system around the model" even when not using the term *harness*.
6. **Cognition — ["Don't Build Multi-Agents"](https://cognition.ai/blog/dont-build-multi-agents)** (Walden Yan, 2025): Articulated the *"share full context / don't fragment agents"* principle — the most cited counter-argument to naive multi-agent designs.
7. **Anthropic — ["How We Built Our Multi-Agent Research System"](https://www.anthropic.com/engineering/built-multi-agent-research-system)** (2025): The ideal counterpart to Cognition's post, showing when multi-agent coordination *is* worth the complexity.
8. **LLM Agent Academic Surveys:** *"A Survey on LLM-based Autonomous Agents"* (Wang et al., 2023) and *"Understanding the Planning of LLM Agents"* (Huang et al.) provide foundational academic taxonomies predating the *harness* wave.

---

## 2. Agent vs. Harness: Stochastic Core & Deterministic Envelope

- **`Agent`** ≈ the **stochastic** core (LLM + reasoning loop + tool selection).
- **`Harness`** ≈ the **deterministic** envelope that wraps, feeds, constrains, and verifies it.

What does *stochastic* mean here?

| Behavior | Definition |
| :--- | :--- |
| **Deterministic** | Always produces **1 predictable output** for a given input. |
| **Non-deterministic** | Multiple possible outputs **without assigned probabilities** (free branching, automata non-determinism: *"any of these paths may occur"*). |
| **Stochastic** | Multiple possible outputs, **each with a probability distribution** (a die, a Markov chain, an LLM sampling tokens from a distribution — *"random with a distribution"*). |

---

## 3. The Harness as Practical Neuro-Symbolic AI

Building on [Gary Marcus's](https://en.wikipedia.org/wiki/Gary_Marcus) framing of **neuro-symbolic AI**, a harness is, architecturally, an *ad hoc* neuro-symbolic system combining two historically rival AI paradigms:

```text
Symbolic AI (GOFAI, 1970s–90s)          Sub-symbolic / Neural AI (2010+)
───────────────────────────────────     ───────────────────────────────────
Explicit rules, logic, knowledge        Neural networks learning patterns
trees, ontologies, Prolog,              from massive datasets (LLMs, CNNs,
deductive reasoning                     transformers)
                 └──────────────┬──────────────┘
                                ▼
                       NEURO-SYMBOLIC AI
               Neural to PERCEIVE + Symbolic to REASON
```

- **The core insight:** Neural networks excel at *perception* (extracting signal and patterns) but fail at strict logic (hallucinations, no formal guarantees). Symbolic rules excel at *reasoning and verification* but are brittle at raw perception (one malformed symbol breaks the rule). Hybridization lets each side do what it does best.

### 3.1 Hybridization Patterns & Real-World Examples

1. **Neural → Symbols → Reason:** The LLM extracts structure; a deterministic engine checks rules.
2. **Symbols guide the network:** Formal grammars or schemas constrain generation (e.g., *constrained decoding*).
3. **Internal neuro-symbolic architectures:** Differentiable symbolic modules embedded inside neural networks.

| Real-World Example | Neural (Perception / Proposal) | Symbolic (Reason / Verification) |
| :--- | :--- | :--- |
| **AlphaGo / AlphaZero** | Neural net evaluates board positions | MCTS algorithmic search explores the move tree |
| **LLM + Prolog / SMT** | LLM translates problem to formal logic | Z3 / Prolog solver proves & returns guaranteed answer |
| **Grammar-constrained decoding** | LLM proposes next tokens | Formal grammar (GBNF, JSON Schema) constrains output |
| **Tool calling + verifier** | Agent proposes code edits | Compiler, type-checker & test suite verify deterministically |
| **RAG + Knowledge Base** | Model retrieves and synthesizes passages | Grounded facts come from a queryable symbolic structure |
| **CodeQL + LLM** | LLM reasons over vulnerability context | Static analyzer performs formal dataflow analysis |
| **VSA / Neuro-Vector-Symbolic** | High-dimensional vector representations | Algebraic symbol composition (active research) |

**Side-by-side correspondence between Neuro-Symbolic AI and an Agent Harness:**

| Neuro-Symbolic Concept | Practical Agent Harness (`POCLI`) |
| :--- | :--- |
| Neural component *"perceives"* | The LLM generates, decides, and proposes (`REQ`, `ARCH`, `CODE`) |
| Symbolic component *"reasons / verifies"* | Deterministic gates (`AuthorityGuard`), tests, linters, tool calls |
| Architecture decides the boundary | Pipeline design: file selection, call graphs, phase gates |
| Failure mode: bad symbol extraction breaks rules | Failure mode: a buggy filter (e.g., `is_source_file`) drops the real file |
{: .table-comparison}

### 3.2 Gary Marcus's Position on Claude Code

Marcus has argued for years (notably in his 2019 book *Rebooting AI*) that pure deep learning hits a wall because LLMs are fundamentally probabilistic token predictors with no intrinsic notion of truth, formal logic, or safety boundaries.

When the internal architecture of Claude Code was examined, Marcus argued that the tool's qualitative leap **is not due to a larger standalone language model**, but rather because **it is not a pure LLM**: it is a hybrid system wrapping the neural network in traditional software engineering and deterministic symbolic components.

### 3.3 The Harness as the Symbolic Component

In modern agent design, the industry and analysts adopted the metaphor of the room and the harness:

- **The neural component:** The LLM acts as a probabilistic expert inside a box, proposing intents, code, and reasoning in natural language.
- **The Harness:** The deterministic software scaffolding (written in classical languages such as TypeScript or Python) operating outside the box. The harness:
  1. **Controls flow with deterministic logic:** Implements explicit decision trees (`IF-THEN` rules, routers, execution policies).
  2. **Mediates formally with the environment:** Parses abstract syntax trees (ASTs), compiles code, runs deterministic unit tests (`pytest`, `npm test`), and validates outputs before committing changes.
  3. **Enforces boundaries and guardrails:** Blocks dangerous commands, mandates safety checks, and governs what contextual information the model may read.

For Marcus, this *harness* of formal rules, grammars, and deterministic tools is precisely the **practical embodiment of the symbolic subsystem**, compensating for the neural model's lack of logical rigor with the precision of deterministic software.

---

## 4. The 5 Fundamental Subsystems & Capability Mapping

A governed harness can be organized into **five fundamental subsystems**. Mapping all **40 harness capabilities** (from POCLI's [Capabilities & Coverage Matrix](/services/#harness-matrix)) onto these five pillars separates what belongs to the governed envelope from the pure operational runtime:

### 4.1 Instructions
*Rules, conventions, architecture, and steps the agent must follow (beyond `AGENTS.md` — everything telling the model what is true and what to do).*

- **Capability #1 — Context management:** what enters the prompt and how it is assembled.
- **Capability #2 — Structured compaction:** rules to preserve essential state across turns.
- **Capability #3 — Tool discovery & JIT loading:** on-demand capability catalog.
- **Capability #4 — Plugins & skills:** declarative instruction extensions.
- **Capability #5 — Context provenance:** documented origin of every injected item.
- **Capability #6 — Append-only event log:** immutable record of instructions received.

### 4.2 State
*Progress, decisions, modified files, and cross-session handoffs.*

- **Capability #7 — Session persistence:** durable conversation storage.
- **Capability #8 — Layered memory:** working, short-term, long-term, and episodic memory.
- **Capability #9 — Checkpoints & durable execution:** resumable execution points.
- **Capability #10 — Typed handoffs:** cross-session continuity contracts.
- **Capability #11 — Replay & recovery:** deterministic state reconstruction.
- **Capability #12 — Episodic / observational memory:** historical behavioral tracking.
- **Capability #13 — Feature state tracking:** `feature_list.json` / artifact state as a primitive.
- **Capability #14 — State merge semantics:** deterministic write-combination rules.

### 4.3 Verification
*Tests, lint, type-checking, smoke tests, and empirical validation.*

- **Capability #15 — Runtime self-tests:** the harness tests itself.
- **Capability #16 — Agent evals:** measuring model quality.
- **Capability #17 — Failure routing / rollback:** what happens when verification fails.
- **Capability #18 — Harness-level evaluation:** measuring the complete system.

### 4.4 Scope
*Boundaries on what the agent may touch and task sizing.*

- **Capability #19 — Safe execution / sandboxing:** OS-level boundaries on what can run.
- **Capability #20 — Approvals & permissions:** gates requiring explicit Product Owner sign-off.
- **Capability #21 — Routing:** which execution path is taken and which is blocked.
- **Capability #22 — Worktrees:** physical workspace isolation.
- **Capability #23 — Scope control:** strict bounds on task size and editable files.

### 4.5 Session Lifecycle
*Initialization, execution, cleanup, persistence, and resumption.*

- **Capability #24 — Error recovery:** graceful handling of transient failures.
- **Capability #25 — Streaming & cancellation:** in-flight output lifecycle.
- **Capability #26 — Session lifecycle:** start, pause, resume, and teardown.
- **Capability #27 — Bootstrap / preflight:** the `initialize` phase.

### 4.6 Pure Operational Runtime Layer (Outside the 5 Pillars)
*The underlying **"service layer"** assumed by the 5-pillar governance model:*

- **Capability #28 — Agent loop:** the core execution mechanism itself.
- **Capability #29 — Model gateway:** LLM provider abstraction.
- **Capability #30 — Typed tool calling:** the agent ↔ world interface.
- **Capability #31 — Observability:** cross-cutting telemetry and logs.
- **Capability #32 — Cost tracking:** token and spend accounting.
- **Capability #33 — Multi-agent orchestration:** coordinating multiple specialized agents.
- **Capability #34 — Event-driven agents:** reactive event handling.
- **Capability #35 — Sub-agent delegation:** spawning focused sub-tasks.
- **Capability #36 — Per-role snapshots:** role-specific state inspection.
- **Capability #37 — Adaptive model routing:** dynamic model selection per task.
- **Capability #38 — Productivity metrics:** delivery throughput measurement.
- **Capability #39 — Capability seams:** provider architecture rather than a functional pillar.
