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

## Referencias

- [Yao et al. — ReAct: Synergizing Reasoning and Acting in Language Models (arXiv:2210.03629)](https://arxiv.org/abs/2210.03629) — Paper fundacional que formaliza el bucle pensamiento → acción → observación de los agentes.
- [Anthropic — Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) — Define el bucle canónico de LLM aumentado con herramientas y retroalimentación del entorno.
- [Wang et al. — A Survey on LLM-based Autonomous Agents (arXiv:2308.11432)](https://arxiv.org/abs/2308.11432) — Revisión académica exhaustiva de bucles de control y arquitecturas de agentes autónomos.
