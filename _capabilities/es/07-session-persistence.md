---
title: "Capacidad #7 — Persistencia de Sesiones"
lang: es
cap_number: 7
subsystem: "4.2 State"
status: "implemented"
permalink: /es/capabilities/07-session-persistence/
description: "Capacidad #7 — Persistencia de Sesiones — Implementada en POCLI."
---

## Qué es

Almacenamiento durable y tolerante a fallos de conversaciones multisesión, metadatos de proyecto, artefactos y estado de ejecución en disco.

## Por qué importa

El estado en memoria RAM desaparece al cerrar la terminal o ante un fallo del proceso, impidiendo flujos de ingeniería de varios días.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `PoCliDatabase` (`src/storage/database.ts`) sobre SQLite nativo de Node.js (`node:sqlite`) en modo WAL en `$HOME/.pocli/pocli.sqlite`. Incluye consola SQL interactiva (`pocli db` en `src/storage/db-repl.ts`).

### Pendiente / Hoja de ruta

Paquetes opcionales de copia de seguridad/exportación cifrada para migrar sesiones entre máquinas.

## Referencias

- [SQLite Write-Ahead Logging (WAL)](https://www.sqlite.org/wal.html) — Cómo SQLite WAL proporciona durabilidad ACID y recuperación ante fallos en bases de datos embebidas.
- [Node.js Built-in `node:sqlite` Module Documentation](https://nodejs.org/api/sqlite.html) — API oficial de Node.js para persistencia SQLite nativa sin dependencias externas.
- [Anthropic — Effective Harnesses for Long-Running Agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) — Analiza cómo persistir el progreso de sesión y artefactos entre múltiples ventanas de contexto.
