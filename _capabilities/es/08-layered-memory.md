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

## Referencias

- [Sumers et al. — Cognitive Architectures for Language Agents (CoALA, arXiv:2309.02427)](https://arxiv.org/abs/2309.02427) — Taxonomía formal que separa la memoria de trabajo, episódica, semántica y procedimental en agentes LLM.
- [Packer et al. — MemGPT: Towards LLMs as Operating Systems (arXiv:2310.08560)](https://arxiv.org/abs/2310.08560) — Introduce niveles jerárquicos de memoria entre ventanas de prompt limitadas y almacenamiento persistente.
- [Park et al. — Generative Agents: Interactive Simulacra of Human Behavior (arXiv:2304.03442)](https://arxiv.org/abs/2304.03442) — Demuestra flujos de memoria estructurada, puntuación de recuperación y reflexión.
