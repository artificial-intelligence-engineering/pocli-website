---
title: "Capacidad #13 — Feature State Tracking"
lang: es
cap_number: 13
subsystem: "4.2 State"
status: "implemented"
permalink: /es/capabilities/13-feature-state-tracking/
description: "Capacidad #13 — Feature State Tracking — Implementada en POCLI."
---

## Qué es

Trata el progreso de funcionalidades, las fases del ciclo de vida y el estado de los artefactos entregables como primitivas estructuradas de primer orden, no como prosa enterrada en el chat.

## Por qué importa

Tanto el Product Owner humano como los agentes autónomos necesitan una única fuente de verdad determinista sobre qué está especificado, implementado, verificado y aceptado.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada mediante la máquina de estados SDLC de 8 fases (`src/core/workflow.ts`), artefactos normativos versionados (`REQ`, `ARCH`, `CODE`, `QA`, `DELIVERY`) en `PoCliDatabase` e informes ejecutivos HTML generados por `PmReporter` (`src/runtime/pm-reporter.ts`).

### Pendiente / Hoja de ruta

Seguimiento granular por requisito individual (`REQ-001` → matriz de tests) enlazado directamente a commits de git.
