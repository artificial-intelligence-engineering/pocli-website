---
title: "Capacidad #1 — Gestión de Contexto"
lang: es
cap_number: 1
subsystem: "4.1 Instructions"
status: "implemented"
permalink: /es/capabilities/01-context-management/
description: "Capacidad #1 — Gestión de Contexto — Implementada en POCLI."
---

## Qué es

Controla de forma determinista qué entra en el prompt del LLM en cada turno y en qué orden: instrucciones de sistema, artefactos normativos del proyecto, memoria por capas, checkpoints de compactación, turnos activos y pasajes recuperados.

## Por qué importa

Los historiales sin acotar provocan degradación del contexto (*lost in the middle*), hacen que el modelo olvide decisiones de arquitectura y disparan el consumo de tokens con salidas obsoletas.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `PoCliDatabase.assembleAgentContextWindow()` (`src/storage/database.ts`), que construye una **ventana de contexto en 3 niveles**: (T1) prefijo cacheable de artefactos normativos (`REQ`, `ARCH`, etc.), (T2) memoria en 4 capas más el último checkpoint de compactación y (T3) turnos activos sin compactar. `NotebookRagEngine` (`src/runtime/notebook-rag.ts`) inyecta citas fundamentadas de la documentación del proyecto bajo demanda.

### Pendiente / Hoja de ruta

Compactación automática basada en umbrales del proveedor antes de saturar la ventana sin requerir `/compact` manual.
