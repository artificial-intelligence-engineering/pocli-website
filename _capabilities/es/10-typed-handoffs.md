---
title: "Capacidad #10 — Handoffs Tipados"
lang: es
cap_number: 10
subsystem: "4.2 State"
status: "implemented"
permalink: /es/capabilities/10-typed-handoffs/
description: "Capacidad #10 — Handoffs Tipados — Implementada en POCLI."
---

## Qué es

Define contratos explícitos y validados por esquema al transferir trabajo de un agente especialista o sesión a otro.

## Por qué importa

Las transferencias en texto libre pierden criterios de aceptación, rutas de archivos o diagnósticos de fallo al cruzar fronteras entre roles.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada mediante esquemas Zod en `src/core/contracts.ts` y orquestada por `PoCliOrchestrator` (`src/runtime/orchestrator.ts`) usando handoffs tipados entre roles (`[ARQ->DEV]`, `[DEV->QA]`, `[QA->ARQ]`) respaldados por artefactos versionados.

### Pendiente / Hoja de ruta

Plantillas de handoff personalizables por el usuario para roles especialistas de dominio.

## Referencias

- [OpenAI — A Practical Guide to Building Agents (PDF)](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf) — Cubre handoffs estructurados y patrones de orquestación centralizada y descentralizada.
- [Cognition — Don't Build Multi-Agents](https://cognition.ai/blog/dont-build-multi-agents) — Analiza por qué fallan los handoffs con pérdida y cómo los contratos explícitos mitigan la deriva.
- [Zod — TypeScript-First Schema Validation](https://zod.dev/) — Biblioteca de validación de esquemas en tiempo de ejecución usada para imponer contratos tipados.
