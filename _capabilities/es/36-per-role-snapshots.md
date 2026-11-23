---
title: "Capacidad #36 — Snapshots por Rol"
lang: es
cap_number: 36
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "partial"
permalink: /es/capabilities/36-per-role-snapshots/
description: "Capacidad #36 — Snapshots por Rol — Implementada parcialmente en POCLI."
---

## Qué es

Captura e inspecciona la vista exacta de contexto, memoria y artefactos que posee cada rol especialista en cualquier punto del proyecto.

## Por qué importa

Depurar handoffs multi-agente exige ver exactamente qué contexto tenía el Architect, Developer o QA en un turno concreto.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: cada rol mantiene flujos de conversación y capas de memoria aisladas en SQLite (`database.ts`), inspeccionables mediante `pocli db` (`db-repl.ts`).

### Pendiente / Hoja de ruta

Snapshots inmutables por rol en instantes concretos con comparación de diferencias e inspección directa en la TUI.
