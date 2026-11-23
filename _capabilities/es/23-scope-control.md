---
title: "Capacidad #23 — Scope Control"
lang: es
cap_number: 23
subsystem: "4.4 Scope"
status: "implemented"
permalink: /es/capabilities/23-scope-control/
description: "Capacidad #23 — Scope Control — Implementada en POCLI."
---

## Qué es

Acota estrictamente qué archivos, herramientas y artefactos puede tocar un agente y limita el alcance de cada tarea para evitar deriva incontrolada.

## Por qué importa

Sin límites estrictos de alcance, los agentes refactorizan archivos no relacionados, alteran tests para forzar falsos positivos o sobrescriben especificaciones de arquitectura.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada mediante `allowedTools` por rol en `src/runtime/harnesses.ts`, rutas de sistema de archivos acotadas al workspace en `PoCliOrchestrator.executeAgentToolCalls()` y propiedad estricta de escritura de artefactos en `AuthorityGuard` (`src/core/workflow.ts`).

### Pendiente / Hoja de ruta

Listas blancas declarativas de patrones glob editables por tarea y cortacircuitos de tamaño máximo de diff.
