---
title: "Capacidad #21 — Routing"
lang: es
cap_number: 21
subsystem: "4.4 Scope"
status: "implemented"
permalink: /es/capabilities/21-routing/
description: "Capacidad #21 — Routing — Implementada en POCLI."
---

## Qué es

Lógica determinista de control de flujo que decide qué fase, rol especialista o ruta de ejecución está permitida a continuación y bloquea transiciones inválidas.

## Por qué importa

Dejar el enrutamiento del flujo al LLM permite que los agentes se salten la revisión de arquitectura, pasen directo al código o eviten la verificación de QA.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `src/core/workflow.ts` (máquina de estados SDLC de 8 fases + `AuthorityGuard`) y `PoCliOrchestrator` (`src/runtime/orchestrator.ts`), que imponen deterministamente las transiciones válidas y el enrutamiento entre roles.

### Pendiente / Hoja de ruta

Definiciones configurables del grafo de flujo para que los equipos puedan personalizar o extender las 8 fases SDLC por defecto.
