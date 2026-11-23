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

## Referencias

- [Ong et al. — RouteLLM: Learning to Route LLMs with Preference Data (arXiv:2406.18665)](https://arxiv.org/abs/2406.18665) — Investigación que demuestra el enrutamiento dinámico entre modelos potentes y rápidos para reducir costes.
- [Chen et al. — FrugalGPT: How to Use Large Language Models While Reducing Cost and Improving Performance (arXiv:2305.05176)](https://arxiv.org/abs/2305.05176) — Introduce cascadas de LLMs y estrategias adaptativas de selección de modelos.
- [Slivkins — Introduction to Multi-Armed Bandits (arXiv:1904.07272)](https://arxiv.org/abs/1904.07272) — Fundamento teórico del enrutamiento adaptativo basado en bandits bajo incertidumbre de latencia y fiabilidad.
