---
title: "Capacidad #18 — Harness-Level Evaluation"
lang: es
cap_number: 18
subsystem: "4.3 Verification"
status: "implemented"
permalink: /es/capabilities/18-harness-level-evaluation/
description: "Capacidad #18 — Harness-Level Evaluation — Implementada en POCLI."
---

## Qué es

Evalúa el sistema completo (modelo + ensamblado de contexto + herramientas + sandboxing + handoffs multi-agente + gates de QA) en lugar de puntuaciones aisladas de un prompt.

## Por qué importa

Como argumenta *AI Agents That Matter* (Kapoor et al., 2024), la fiabilidad real depende del harness completo de extremo a extremo, incluyendo coste y rigor de verificación.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada mediante `pocli e2e` (`src/runtime/headless-runner.ts`), `pocli tui-test` y el pipeline autónomo de QA que ejecuta suites aisladas de Robot Framework junto con Mutation Testing (`TC-MUT-001`).

### Pendiente / Hoja de ruta

Publicación de cuadros de mando reproducibles comparando versiones del harness en coste, latencia y tasa de defectos escapados.

## Referencias

- [Kapoor et al. — AI Agents That Matter (arXiv:2407.01502)](https://arxiv.org/abs/2407.01502) — Sostiene que la evaluación debe medir el harness completo y su coste, no solo el modelo base.
- [SWE-bench Verified (OpenAI & Princeton)](https://openai.com/index/introducing-swe-bench-verified/) — Benchmark validado de ingeniería de software end-to-end que evalúa arneses completos de codificación.
- [Robot Framework — Acceptance Testing & RPA](https://robotframework.org/) — Motor externo de pruebas de aceptación de caja negra utilizado por el harness de QA autónomo de POCLI.
