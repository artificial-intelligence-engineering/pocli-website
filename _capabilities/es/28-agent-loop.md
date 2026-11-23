---
title: "Capacidad #28 — Agent Loop"
lang: es
cap_number: 28
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "implemented"
permalink: /es/capabilities/28-agent-loop/
description: "Capacidad #28 — Agent Loop — Implementada en POCLI."
---

## Qué es

El ciclo central de ejecución que impulsa cada turno del agente: ensamblar contexto → invocar LLM → parsear llamadas a herramientas → ejecutarlas → observar resultados → iterar o finalizar.

## Por qué importa

Sin un bucle acotado que devuelva las observaciones de ejecución al modelo, un LLM no puede autocorregirse ni completar tareas de ingeniería multipaso.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `PoCliOrchestrator` (`src/runtime/orchestrator.ts`) y `src/runtime/agent-worker.ts`, comunicándose sobre JSON-RPC 2.0 stdio con ciclos de corrección acotados y timeouts por turno.

### Pendiente / Hoja de ruta

Detección semántica de bucles atascados para abortar automáticamente cuando un agente repite llamadas fallidas idénticas.
