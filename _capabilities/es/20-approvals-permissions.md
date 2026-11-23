---
title: "Capacidad #20 — Aprobaciones y Permisos"
lang: es
cap_number: 20
subsystem: "4.4 Scope"
status: "implemented"
permalink: /es/capabilities/20-approvals-permissions/
description: "Capacidad #20 — Aprobaciones y Permisos — Implementada en POCLI."
---

## Qué es

Fronteras estrictas de autoridad y gates Human-in-the-Loop (HITL) que exigen aprobación explícita del humano antes de transiciones o mutaciones de alto impacto.

## Por qué importa

Los agentes autónomos deben proponer, analizar y probar, pero el Product Owner humano debe conservar la autoridad soberana sobre requisitos, arquitectura y entrega final.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada mediante `AuthorityGuard` (`src/core/workflow.ts`), que valida deterministamente permisos por rol y propiedad de artefactos, combinada con los gates obligatorios del Product Owner (`/approve` y `/accept`).

### Pendiente / Hoja de ruta

Confirmaciones interactivas por nivel de riesgo para operaciones destructivas puntuales en shell.
