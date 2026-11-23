---
title: "Capacidad #34 — Event-Driven Agents"
lang: es
cap_number: 34
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "not_implemented"
permalink: /es/capabilities/34-event-driven-agents/
description: "Capacidad #34 — Event-Driven Agents — Todavía no implementada en POCLI."
---

## Qué es

Dispara flujos de agentes de forma reactiva ante eventos externos como webhooks de GitHub, fallos de CI, cambios en el sistema de archivos o temporizadores programados.

## Por qué importa

No todas las tareas de ingeniería nacen de un prompt interactivo; el triaje en segundo plano y la verificación continua requieren disparadores reactivos.

## Estado e Implementación en POCLI

**Estado:** Todavía no implementada

Todavía no implementada. POCLI se ejecuta actualmente de forma interactiva desde la TUI (`CommandCenterApp.tsx`) o mediante invocaciones explícitas de CLI/headless (`pocli e2e`).

### Pendiente / Hoja de ruta

Un bus de eventos en modo daemon con soporte para `fs.watch`, cron y webhooks conectado a `PoCliOrchestrator`.
