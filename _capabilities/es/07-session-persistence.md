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
