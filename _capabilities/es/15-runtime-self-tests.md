---
title: "Capacidad #15 — Tests del Runtime"
lang: es
cap_number: 15
subsystem: "4.3 Verification"
status: "implemented"
permalink: /es/capabilities/15-runtime-self-tests/
description: "Capacidad #15 — Tests del Runtime — Implementada en POCLI."
---

## Qué es

Suites de verificación automatizada que testean el propio harness: su máquina de estados, persistencia SQLite, despacho de herramientas, sandboxing y renderizado TUI.

## Por qué importa

Si la envolvente determinista tiene errores (por ejemplo, un filtro de archivos o un gate de permisos roto), ni el LLM más capaz puede compensar un harness defectuoso.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada con suites unitarias y de integración en Vitest, verificación end-to-end headless (`pocli e2e` mediante `src/runtime/headless-runner.ts`) y pruebas automatizadas de TUI virtual (`pocli tui-test`).

### Pendiente / Hoja de ruta

Pruebas continuas de regresión sobre todos los backends de sandbox Linux soportados (Bubblewrap y Podman) en CI.
