---
title: "Capacidad #2 — Compactación Estructurada"
lang: es
cap_number: 2
subsystem: "4.1 Instructions"
status: "implemented"
permalink: /es/capabilities/02-structured-compaction/
description: "Capacidad #2 — Compactación Estructurada — Implementada en POCLI."
---

## Qué es

Resume y comprime turnos antiguos de conversación en checkpoints estructurados que preservan decisiones, restricciones y pendientes mientras liberan espacio en el prompt.

## Por qué importa

Las sesiones largas de ingeniería superan inevitablemente la ventana de contexto. El truncado ingenuo pierde decisiones críticas; la compactación estructurada preserva la continuidad sin destruir la trazabilidad.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada mediante el comando `/compact` y la tabla `context_compactions` en `PoCliDatabase` (`src/storage/database.ts`). La compactación es **sin pérdida**: los mensajes históricos nunca se borran, sino que se vinculan con `compacted_into_id` mientras el resumen estructurado se inyecta en el Nivel 2 de los turnos siguientes.

### Pendiente / Hoja de ruta

Disparo automático de la compactación cuando los tokens activos superen un umbral configurable de la ventana del modelo.

## Referencias

- [Anthropic — Effective Context Engineering for AI Agents (Compaction)](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — Detalla estrategias de compactación estructurada para preservar decisiones arquitectónicas en sesiones largas.
- [Packer et al. — MemGPT: Towards LLMs as Operating Systems (arXiv:2310.08560)](https://arxiv.org/abs/2310.08560) — Paper fundacional sobre gestión virtual de contexto y paginación/resumen fuera de la ventana activa.
- [OpenAI — Conversation State & Compaction Guide](https://platform.openai.com/docs/guides/conversation-state) — Patrones prácticos para gestionar el estado de conversaciones largas dentro del presupuesto de contexto.
