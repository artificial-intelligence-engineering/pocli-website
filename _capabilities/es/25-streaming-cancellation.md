---
title: "Capacidad #25 — Streaming y Cancelación"
lang: es
cap_number: 25
subsystem: "4.5 Session Lifecycle"
status: "partial"
permalink: /es/capabilities/25-streaming-cancellation/
description: "Capacidad #25 — Streaming y Cancelación — Implementada parcialmente en POCLI."
---

## Qué es

Transmite en tiempo real la salida incremental del modelo y el progreso de herramientas a la interfaz, permitiendo cancelar limpiamente turnos en curso.

## Por qué importa

Las interfaces bloqueantes ocultan si el agente está razonando o colgado, y los cortes bruscos (`Ctrl+C`) pueden dejar subprocesos huérfanos o estado corrupto.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: `PersistentAgentRuntime` envía actualizaciones incrementales mediante JSON-RPC `agent.streamChunk` a `CommandCenterApp.tsx`, con control de timeouts por turno.

### Pendiente / Hoja de ruta

Streaming HTTP SSE nativo token a token en todos los adaptadores de proveedores y cancelación cooperativa limpia en mitad del streaming desde la TUI.
