---
title: "Capacidad #14 — State Merge Semantics"
lang: es
cap_number: 14
subsystem: "4.2 State"
status: "implemented"
permalink: /es/capabilities/14-state-merge-semantics/
description: "Capacidad #14 — State Merge Semantics — Implementada en POCLI."
---

## Qué es

Impone reglas deterministas para combinar escrituras concurrentes o secuenciales sobre el estado compartido del proyecto sin sobrescrituras silenciosas ni corrupción.

## Por qué importa

Cuando múltiples workers especialistas operan sobre el mismo proyecto, las escrituras sin sincronizar provocan condiciones de carrera, pérdida de versiones y corrupción del estado.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `PoCliCoordinator` (`src/runtime/coordinator.ts`), que actúa como **Sole Write Owner** serializando las mutaciones en SQLite con claves de idempotencia (`requestId`) y control de concurrencia optimista (`expectedVersion`).

### Pendiente / Hoja de ruta

Políticas de merge semántico a 3 vías para ediciones paralelas de archivos cuando se incorpore el fan-out concurrente de desarrolladores.
