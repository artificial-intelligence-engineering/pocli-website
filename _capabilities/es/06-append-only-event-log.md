---
title: "Capacidad #6 — Append-Only Event Log"
lang: es
cap_number: 6
subsystem: "4.1 Instructions"
status: "implemented"
permalink: /es/capabilities/06-append-only-event-log/
description: "Capacidad #6 — Append-Only Event Log — Implementada en POCLI."
---

## Qué es

Mantiene un registro cronológico e inmutable de todas las instrucciones, llamadas a herramientas y transiciones de estado ocurridas durante una sesión.

## Por qué importa

Los historiales mutables destruyen la visibilidad forense. Un registro append-only garantiza auditoría completa para cumplimiento, depuración y análisis post-mortem.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `PoCliDatabase` (`src/storage/database.ts`) y `PoCliCoordinator` (`src/runtime/coordinator.ts`). Los turnos de conversación se almacenan en modo append-only (la compactación marca `compacted_into_id` sin borrar filas) y `coordinator_audit_log` registra cada mutación de estado con `requestId`, rol, acción y marca temporal.

### Pendiente / Hoja de ruta

Exportación del flujo de eventos append-only en formatos estándar JSONL / OpenTelemetry para pipelines externos de auditoría.

## Referencias

- [Martin Fowler — Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html) — Patrón arquitectónico clásico que captura todos los cambios de estado como una secuencia inmutable de eventos.
- [Jay Kreps — The Log: What Every Software Engineer Should Know About Real-Time Data's Unifying Abstraction](https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying) — Análisis en profundidad de los logs append-only como base de durabilidad, auditoría y replicación.
- [SQLite Write-Ahead Logging (WAL)](https://www.sqlite.org/wal.html) — Documentación técnica del modo WAL de SQLite para lecturas concurrentes y transacciones durables.
