---
title: "Capacidad #3 — Tool Discovery y Carga JIT"
lang: es
cap_number: 3
subsystem: "4.1 Instructions"
status: "partial"
permalink: /es/capabilities/03-tool-discovery-jit/
description: "Capacidad #3 — Tool Discovery y Carga JIT — Implementada parcialmente en POCLI."
---

## Qué es

Expone un catálogo acotado de herramientas al agente y carga sus esquemas completos bajo demanda (JIT) únicamente cuando son necesarios para el rol o la tarea actual.

## Por qué importa

Inyectar decenas de esquemas de herramientas no utilizadas en cada prompt desperdicia miles de tokens y degrada la precisión de selección de herramientas.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: `src/runtime/harnesses.ts` restringe las herramientas expuestas por rol mediante `allowedTools` (`architect`, `developer`, `qa`, `pm`) y `McpRegistry` (`src/runtime/mcp-client.ts`) descubre herramientas MCP externas filtradas por `allowedRoles`.

### Pendiente / Hoja de ruta

Carga diferida real (JIT) para catálogos grandes de herramientas, de modo que las definiciones no usadas solo se carguen bajo demanda.

## Referencias

- [Anthropic — Writing Effective Tools for AI Agents](https://www.anthropic.com/engineering/writing-tools-for-agents) — Buenas prácticas para catálogos concisos de herramientas, namespaces y prevención del tool-bloat.
- [Model Context Protocol (MCP) — Tools Specification](https://modelcontextprotocol.io/docs/concepts/tools) — Protocolo estándar para descubrimiento dinámico de herramientas (`tools/list`) e invocación tipada.
- [Anthropic — Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) — Cubre el diseño de la interfaz agente-computador (ACI) y superficies de herramientas acotadas.
