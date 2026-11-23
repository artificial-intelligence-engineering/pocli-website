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

## Referencias

- [OpenTelemetry — Semantic Conventions for Generative AI](https://opentelemetry.io/docs/specs/semconv/gen-ai/) — Estándar emergente para trazar llamadas LLM, consumo de tokens, latencia y spans de agentes.
- [Charity Majors et al. — Observability Engineering (O'Reilly)](https://www.oreilly.com/library/view/observability-engineering/9781492076438/) — Texto fundamental sobre eventos estructurados, logs de alta cardinalidad y trazado distribuido.
- [Anthropic — Demystifying Evals & Tracing for AI Agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) — Explica por qué las trazas completas de turno y la telemetría estructurada son vitales para depurar agentes.
