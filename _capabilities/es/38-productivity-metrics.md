---
title: "Capacidad #38 — Métricas de Productividad"
lang: es
cap_number: 38
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "partial"
permalink: /es/capabilities/38-productivity-metrics/
description: "Capacidad #38 — Métricas de Productividad — Implementada parcialmente en POCLI."
---

## Qué es

Mide el rendimiento de entrega, ciclos de retrabajo en QA, tasas de defectos y tiempos de completado por fase en los proyectos de ingeniería.

## Por qué importa

Los responsables técnicos necesitan métricas objetivas de entrega —no solo conteos de tokens— para verificar que los agentes aceleran la entrega con calidad.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: `PmReporter` (`src/runtime/pm-reporter.ts`) genera informes ejecutivos HTML autocontenidos en `deliveries/` resumiendo hitos de fase, artefactos y resultados de QA.

### Pendiente / Hoja de ruta

Analítica longitudinal de tiempo de ciclo, tasa de aprobación en primera pasada de QA y throughput agregado entre proyectos.
