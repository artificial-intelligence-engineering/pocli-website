---
title: "Capacidad #11 — Replay y Recuperación"
lang: es
cap_number: 11
subsystem: "4.2 State"
status: "not_implemented"
permalink: /es/capabilities/11-replay-recovery/
description: "Capacidad #11 — Replay y Recuperación — Todavía no implementada en POCLI."
---

## Qué es

Reconstruye estados pasados de la sesión de forma determinista paso a paso (*time-travel debugging*) y permite retroceder o bifurcar desde un turno anterior.

## Por qué importa

Cuando un agente toma un rumbo equivocado varios pasos atrás, es mucho más fiable retroceder limpiamente que intentar corregir un contexto contaminado.

## Estado e Implementación en POCLI

**Estado:** Todavía no implementada

Todavía no implementada. Aunque `PoCliDatabase` ya conserva el historial completo append-only y `coordinator_audit_log` como base, los comandos de reproducción determinista paso a paso y bifurcación/retroceso de turnos aún no están construidos.

### Pendiente / Hoja de ruta

Implementar `pocli replay` y retroceso/bifurcación desde snapshots inmutables tanto del estado SQLite como de los archivos del workspace.

## Referencias

- [Martin Fowler — Event Sourcing & Temporal Query](https://martinfowler.com/eaaDev/EventSourcing.html) — Explica cómo reconstruir cualquier estado histórico de forma determinista reproduciendo un log de eventos.
- [LangGraph — Time Travel & Rewind](https://langchain-ai.github.io/langgraph/concepts/time-travel/) — Patrón práctico para retroceder y bifurcar la ejecución de agentes desde checkpoints pasados.
- [Temporal — Deterministic Replay](https://docs.temporal.io/encyclopedia/event-history) — Cómo los historiales de eventos permiten reproducción exacta y depuración tras fallos.
