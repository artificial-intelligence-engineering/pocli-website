---
title: "Capacidad #20 — Aprobaciones y Permisos"
lang: es
cap_number: 20
subsystem: "4.4 Scope"
status: "implemented"
permalink: /es/capabilities/20-approvals-permissions/
description: "Capacidad #20 — Aprobaciones y Permisos — Implementada en POCLI."
---

## Qué es

Fronteras estrictas de autoridad y gates Human-in-the-Loop (HITL) que exigen aprobación explícita del humano antes de transiciones o mutaciones de alto impacto.

## Por qué importa

Los agentes autónomos deben proponer, analizar y probar, pero el Product Owner humano debe conservar la autoridad soberana sobre requisitos, arquitectura y entrega final.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada mediante `AuthorityGuard` (`src/core/workflow.ts`), que valida deterministamente permisos por rol y propiedad de artefactos, combinada con los gates obligatorios del Product Owner (`/approve` y `/accept`).

### Pendiente / Hoja de ruta

Confirmaciones interactivas por nivel de riesgo para operaciones destructivas puntuales en shell.

## Referencias

- [OWASP Top 10 for Large Language Model Applications (LLM06: Excessive Agency)](https://genai.owasp.org/llmrisk/llm06-excessive-agency/) — Taxonomía de seguridad que destaca el principio de mínimo privilegio y los gates de aprobación humana.
- [OpenAI — A Practical Guide to Building Agents (Guardrails & Human Intervention)](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf) — Define guardrails por niveles de riesgo y puntos de control obligatorios Human-in-the-Loop.
- [NIST AI Risk Management Framework (AI RMF 1.0)](https://www.nist.gov/itl/ai-risk-management-framework) — Marco de gobernanza para supervisión humana, rendición de cuentas y autonomía controlada.
