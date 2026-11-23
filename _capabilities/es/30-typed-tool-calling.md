---
title: "Capacidad #30 — Tool Calling Tipado"
lang: es
cap_number: 30
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "implemented"
permalink: /es/capabilities/30-typed-tool-calling/
description: "Capacidad #30 — Tool Calling Tipado — Implementada en POCLI."
---

## Qué es

La interfaz determinista agente ↔ mundo que valida los argumentos de cada herramienta contra esquemas estrictos antes de ejecutar acciones sobre archivos, artefactos, tests o handoffs.

## Por qué importa

Parsear comandos en texto libre rompe la automatización e introduce fallos de seguridad y fiabilidad.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `LLMGateway` (`choiceMsg.tool_calls` combinado con `extractToolCalls()`), respaldada por esquemas Zod en `src/core/contracts.ts` y despachada deterministamente por `PoCliOrchestrator.executeAgentToolCalls()`.

### Pendiente / Hoja de ruta

Envío nativo de definiciones completas JSON Schema `tools[]` en los payloads HTTP de todos los adaptadores.
