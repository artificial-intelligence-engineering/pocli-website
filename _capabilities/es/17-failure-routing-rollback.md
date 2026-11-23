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
