---
title: "Capacidad #8 — Memoria por Capas"
lang: es
cap_number: 8
subsystem: "4.2 State"
status: "implemented"
permalink: /es/capabilities/08-layered-memory/
description: "Capacidad #8 — Memoria por Capas — Implementada en POCLI."
---

## Qué es

Separa la memoria del agente en ámbitos y ciclos de vida diferenciados (conversacional, de trabajo, de proyecto y específica de agente) en lugar de volcarlo todo en un único historial plano.

## Por qué importa

Las notas temporales de depuración no deben contaminar las restricciones arquitectónicas permanentes, mientras que las convenciones del proyecto deben sobrevivir entre sesiones y roles.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `PoCliDatabase` (`src/storage/database.ts`) con una **arquitectura de memoria en 4 capas** (`CONVERSATIONAL`, `WORKING`, `PROJECT`, `AGENT`) persistida en SQLite e inyectada selectivamente en el Nivel 2 de la ventana de contexto de cada rol.

### Pendiente / Hoja de ruta

Políticas automáticas de expiración/limpieza para entradas obsoletas de memoria `WORKING`.
