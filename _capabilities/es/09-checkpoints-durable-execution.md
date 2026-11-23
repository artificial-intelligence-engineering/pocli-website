---
title: "Capacidad #9 — Checkpoints y Durable Execution"
lang: es
cap_number: 9
subsystem: "4.2 State"
status: "partial"
permalink: /es/capabilities/09-checkpoints-durable-execution/
description: "Capacidad #9 — Checkpoints y Durable Execution — Implementada parcialmente en POCLI."
---

## Qué es

Persiste puntos de control reanudables para que los flujos largos de agentes puedan pausarse, sobrevivir a caídas y reanudarse sin repetir trabajo ya completado.

## Por qué importa

Los flujos de desarrollo y QA abarcan decenas de llamadas a herramientas; reiniciar desde cero tras un fallo transitorio desperdicia tiempo y tokens.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: `PoCliDatabase` persiste de forma ACID el estado de turnos, la fase SDLC y los checkpoints de `context_compactions` para reanudar proyectos desde el último turno completado.

### Pendiente / Hoja de ruta

Ejecución durable intra-turno capaz de reanudar un turno interrumpido exactamente en la frontera de la última llamada a herramienta.

## Referencias

- [Temporal — What Is Durable Execution?](https://docs.temporal.io/evaluate/understanding-temporal#durable-execution) — Referencia de la industria sobre ejecución durable, estado con checkpoints y reanudación tolerante a fallos.
- [LangGraph — Persistence & Checkpointing Concepts](https://langchain-ai.github.io/langgraph/concepts/persistence/) — Explica los checkpoints a nivel de grafo para pausar, reanudar y recuperar flujos de agentes.
- [Anthropic — Effective Harnesses for Long-Running Agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) — Patrones de ingeniería para guardar checkpoints seguros en tareas de programación multisesión.
