---
title: "Capacidad #32 — Cost Tracking"
lang: es
cap_number: 32
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "partial"
permalink: /es/capabilities/32-cost-tracking/
description: "Capacidad #32 — Cost Tracking — Implementada parcialmente en POCLI."
---

## Qué es

Contabiliza tokens de entrada/salida, ahorro por caché/compactación y gasto monetario por turno, rol, modelo y proyecto.

## Por qué importa

Los bucles autónomos multiturno pueden consumir un presupuesto elevado sin aviso si no se contabilizan tokens y costes de forma transparente.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: `PoCliDatabase` calcula tokens activos y ahorrados tras compactación a lo largo de los turnos y los muestra en la TUI.

### Pendiente / Hoja de ruta

Un libro mayor exacto de costes en USD por modelo con límites configurables de presupuesto y alertas por proyecto.
