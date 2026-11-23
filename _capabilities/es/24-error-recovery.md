---
title: "Capacidad #24 — Recuperación de Errores"
lang: es
cap_number: 24
subsystem: "4.5 Session Lifecycle"
status: "implemented"
permalink: /es/capabilities/24-error-recovery/
description: "Capacidad #24 — Recuperación de Errores — Implementada en POCLI."
---

## Qué es

Detecta y se recupera de forma resiliente ante fallos transitorios: límites de cuota LLM (HTTP 429), caídas 503, timeouts de red y workers bloqueados.

## Por qué importa

Las APIs externas de LLM fallan con frecuencia bajo carga; sin recuperación automática, las sesiones largas se abortan bruscamente.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `LLMRouter` (`src/runtime/llm-router.ts`) con control de cuotas en ventana deslizante, temporizadores de cooldown y failover automático en cascada ante HTTP 429/503/timeouts, junto con timeouts de 120s por turno en `PersistentAgentRuntime`.

### Pendiente / Hoja de ruta

Backoff exponencial con jitter por error antes del failover y detección semántica de bucles atascados.
