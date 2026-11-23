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
