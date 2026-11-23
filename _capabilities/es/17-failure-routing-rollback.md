---
title: "Capacidad #17 — Failure Routing / Rollback"
lang: es
cap_number: 17
subsystem: "4.3 Verification"
status: "partial"
permalink: /es/capabilities/17-failure-routing-rollback/
description: "Capacidad #17 — Failure Routing / Rollback — Implementada parcialmente en POCLI."
---

## Qué es

Define rutas deterministas de recuperación cuando fallan tests, linters o gates de QA: reenviando diagnósticos estructurados para reparación acotada o revirtiendo cambios inseguros.

## Por qué importa

Los fallos sin gestionar bloquean el flujo o permiten que código defectuoso avance hacia fases posteriores.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: `PoCliOrchestrator` (`src/runtime/orchestrator.ts`) redirige las verificaciones fallidas de QA de vuelta al Developer en ciclos autónomos acotados (`MAX_QA_CORRECTION_CYCLES = 3`) antes de escalar al Product Owner.

### Pendiente / Hoja de ruta

Rollback automático de snapshots/git del workspace cuando un gate de verificación falla de forma crítica o agota su presupuesto de reintentos.

## Referencias

- [Anthropic — Building Effective Agents (Evaluator-Optimizer Loop)](https://www.anthropic.com/engineering/building-effective-agents) — Describe bucles acotados de retroalimentación que devuelven fallos de verificación al generador.
- [Michael Nygard — Release It! (Circuit Breakers & Stability Patterns)](https://pragprog.com/titles/mnee2/release-it-second-edition/) — Patrones clásicos de estabilidad para acotar reintentos, aislar fallos y degradar de forma segura.
- [Git — Reset, Revert & Checkout Recovery](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified) — Referencia sobre primitivas deterministas de rollback del espacio de trabajo en Git.
