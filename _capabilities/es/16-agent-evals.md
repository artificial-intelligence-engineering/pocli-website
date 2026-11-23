---
title: "Capacidad #16 — Evals del Agente"
lang: es
cap_number: 16
subsystem: "4.3 Verification"
status: "partial"
permalink: /es/capabilities/16-agent-evals/
description: "Capacidad #16 — Evals del Agente — Implementada parcialmente en POCLI."
---

## Qué es

Benchmarks de evaluación cuantitativa que miden la precisión del modelo y de cada rol, la fiabilidad del tool calling y la calidad de salida en tareas estándar de ingeniería.

## Por qué importa

Cambiar de modelo o editar prompts de sistema sin evaluaciones empíricas impide distinguir mejoras reales de regresiones silenciosas.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: `pocli e2e` (`src/runtime/headless-runner.ts`) y las suites de validación de QA verifican la resolución completa en escenarios reales.

### Pendiente / Hoja de ruta

Arneses de evaluación multimodelo automatizados que midan pass@k, precisión de tool calling, latencia y coste por token sobre un dataset versionado.
