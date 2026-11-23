---
title: "Capacidad #35 — Delegación a Sub-Agentes"
lang: es
cap_number: 35
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "partial"
permalink: /es/capabilities/35-sub-agent-delegation/
description: "Capacidad #35 — Delegación a Sub-Agentes — Implementada parcialmente en POCLI."
---

## Qué es

Lanza sub-agentes enfocados con contexto acotado para resolver subtareas concretas (investigación, módulos independientes, pruebas) y devolver resúmenes concisos.

## Por qué importa

Delegar exploración ruidosa o trabajo paralelo en módulos mantiene limpio el contexto principal y acelera la entrega.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: `PoCliOrchestrator` delega fases del SDLC entre workers especialistas persistentes (`architect`, `developer`, `qa`, `pm`) con ventanas de contexto aisladas.

### Pendiente / Hoja de ruta

Lanzamiento dinámico de sub-agentes efímeros en paralelo (fan-out / fan-in) sobre partes disjuntas del código.

## Referencias

- [Anthropic — How We Built Our Multi-Agent Research System](https://www.anthropic.com/engineering/built-multi-agent-research-system) — Detalla la delegación orquestador-worker con contextos acotados y resúmenes comprimidos de retorno.
- [OpenAI — A Practical Guide to Building Agents (Manager Pattern)](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf) — Describe cómo delegar subtareas especializadas a sub-agentes acotados.
- [Anthropic — Building Effective Agents (Orchestrator-Workers)](https://www.anthropic.com/engineering/building-effective-agents) — Referencia canónica sobre descomposición dinámica de tareas y síntesis de workers en paralelo.
