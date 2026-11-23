---
title: "Capacidad #33 — Orquestación Multi-Agente"
lang: es
cap_number: 33
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "implemented"
permalink: /es/capabilities/33-multi-agent-orchestration/
description: "Capacidad #33 — Orquestación Multi-Agente — Implementada en POCLI."
---

## Qué es

Coordina múltiples agentes especialistas aislados con roles, listas de herramientas y responsabilidades de verificación diferenciadas sobre un flujo compartido.

## Por qué importa

Un único agente generalista tiende a autoevaluar su propio código y contaminar su contexto; la separación por roles impone verificación independiente.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada mediante `PersistentAgentRuntime` (`src/runtime/persistent-runtime.ts`) y `PoCliOrchestrator` (`src/runtime/orchestrator.ts`), coordinando workers aislados de `architect`, `developer`, `qa` y `pm` sobre JSON-RPC 2.0 con handoffs tipados y sin ruido cruzado.

### Pendiente / Hoja de ruta

Orquestación concurrente fan-out / fan-in con múltiples workers de desarrollo en paralelo.

## Referencias

- [Anthropic — How We Built Our Multi-Agent Research System](https://www.anthropic.com/engineering/built-multi-agent-research-system) — Reporte real de ingeniería detallando cuándo y cómo compensa la orquestación multi-agente.
- [Cognition — Don't Build Multi-Agents](https://cognition.ai/blog/dont-build-multi-agents) — Contrapunto esencial que advierte contra la fragmentación del contexto y la mala coordinación.
- [Hong et al. — MetaGPT: Meta Programming for a Multi-Agent Collaborative Framework (arXiv:2308.00352)](https://arxiv.org/abs/2308.00352) — Codifica procedimientos estándar (SOPs) entre roles de Product Manager, Arquitecto, Ingeniero y QA.
