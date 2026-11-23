---
title: "Capacidad #5 — Context Provenance"
lang: es
cap_number: 5
subsystem: "4.1 Instructions"
status: "partial"
permalink: /es/capabilities/05-context-provenance/
description: "Capacidad #5 — Context Provenance — Implementada parcialmente en POCLI."
---

## Qué es

Registra el origen exacto, la versión y el hash de cada fragmento de contexto inyectado en un turno del agente para poder auditar decisiones hasta sus fuentes autoritativas.

## Por qué importa

Cuando un agente toma una decisión incorrecta, es necesario saber si provino de un artefacto obsoleto, un mensaje del usuario, un documento RAG o una alucinación del modelo.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: los artefactos normativos están versionados en SQLite (`database.ts`) y `NotebookRagEngine` (`src/runtime/notebook-rag.ts`) registra hashes SHA-256 y citas de origen para los documentos indexados.

### Pendiente / Hoja de ruta

Un manifiesto unificado de procedencia por turno que registre los IDs de fuente, rangos y conteo de tokens de cada bloque inyectado en el prompt.
