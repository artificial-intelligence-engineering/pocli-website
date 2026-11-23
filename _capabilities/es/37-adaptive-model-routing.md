---
title: "Capacidad #37 — Adaptive Model Routing"
lang: es
cap_number: 37
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "implemented"
permalink: /es/capabilities/37-adaptive-model-routing/
description: "Capacidad #37 — Adaptive Model Routing — Implementada en POCLI."
---

## Qué es

Selecciona dinámicamente el mejor modelo y proveedor para cada tarea según requisitos de capacidad, latencia, margen de cuota y salud reciente.

## Por qué importa

Las tareas de razonamiento complejo necesitan modelos potentes, mientras que iteraciones rápidas o tareas rutinarias se benefician de modelos rápidos o locales.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `LLMRouter` (`src/runtime/llm-router.ts`) con perfiles de enrutamiento (`auto:smart`, `auto:fast`, `auto:reliable`), seguimiento de cuotas RPM/RPD/TPM/TPD en ventana deslizante, puntuación con cooldowns e integración de modelos locales (`src/local/local-manager.ts`).

### Pendiente / Hoja de ruta

Evaluaciones automáticas shadow/canary para ajustar empíricamente la puntuación de candidatos.
