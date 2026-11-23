---
title: "Capacidad #31 — Observabilidad"
lang: es
cap_number: 31
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "partial"
permalink: /es/capabilities/31-observability/
description: "Capacidad #31 — Observabilidad — Implementada parcialmente en POCLI."
---

## Qué es

Logs estructurados transversales, métricas de latencia y trazas de ejecución que dan visibilidad completa sobre cada turno, herramienta y llamada a proveedor.

## Por qué importa

Sin observabilidad estructurada, diagnosticar picos de latencia, errores de proveedores o comportamientos inesperados del agente se convierte en adivinación.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: `Logger` (`src/core/logger.ts`) escribe logs rotativos con búfer circular en `$HOME/.pocli/logs/pocli.log` (inspeccionables con `pocli logs`) y `LLMRouter` registra `latencyMs` por proveedor.

### Pendiente / Hoja de ruta

Telemetría granular de Time-To-First-Token (TTFT) en la TUI y exportación de spans OpenTelemetry (OTLP).
