---
title: "Capacidad #26 — Session Lifecycle"
lang: es
cap_number: 26
subsystem: "4.5 Session Lifecycle"
status: "implemented"
permalink: /es/capabilities/26-session-lifecycle/
description: "Capacidad #26 — Session Lifecycle — Implementada en POCLI."
---

## Qué es

Gestiona el ciclo de vida operativo completo de una sesión de agente: inicialización, ejecución activa, pausa, reanudación entre reinicios y cierre limpio de workers.

## Por qué importa

Una gestión limpia del ciclo de vida evita procesos worker zombis, fugas de descriptores y bloqueos inconsistentes de sesión.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `src/core/lifecycle.ts` y `PersistentAgentRuntime` (`src/runtime/persistent-runtime.ts`), coordinando el arranque de workers persistentes por rol, reanudación desde SQLite, manejo de señales y apagado limpio.

### Pendiente / Hoja de ruta

Temporizadores de hibernación de workers inactivos para liberar memoria automáticamente en pausas largas.
