---
title: "Capacidad #12 — Memoria Episódica / Observacional"
lang: es
cap_number: 12
subsystem: "4.2 State"
status: "partial"
permalink: /es/capabilities/12-episodic-observational-memory/
description: "Capacidad #12 — Memoria Episódica / Observacional — Implementada parcialmente en POCLI."
---

## Qué es

Captura observaciones recurrentes de comportamiento, lecciones aprendidas y episodios históricos de éxito o fallo entre sesiones para que los agentes mejoren con el tiempo.

## Por qué importa

Sin memoria episódica, los agentes tropiezan repetidamente con las mismas particularidades del entorno, flags de compilación o errores típicos en cada nueva sesión.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: las capas de memoria `AGENT` y `PROJECT` en `PoCliDatabase` (`src/storage/database.ts`) persisten observaciones entre sesiones y notas del proyecto.

### Pendiente / Hoja de ruta

Pipelines automáticos de reflexión post-sesión que destilen errores recurrentes y soluciones verificadas en entradas episódicas estructuradas.

## Referencias

- [Shinn et al. — Reflexion: Language Agents with Verbal Reinforcement Learning (arXiv:2303.11366)](https://arxiv.org/abs/2303.11366) — Demuestra cómo almacenar reflexiones episódicas verbales de fallos para mejorar intentos futuros.
- [Sumers et al. — Cognitive Architectures for Language Agents (CoALA, arXiv:2309.02427)](https://arxiv.org/abs/2309.02427) — Define la memoria episódica como secuencias de eventos pasados que informan la planificación futura.
- [Park et al. — Generative Agents (arXiv:2304.03442)](https://arxiv.org/abs/2304.03442) — Introduce flujos de memoria observacional y síntesis periódica de reflexiones.
