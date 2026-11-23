---
title: "Capacidad #4 — Plugins y Skills"
lang: es
cap_number: 4
subsystem: "4.1 Instructions"
status: "partial"
permalink: /es/capabilities/04-plugins-skills/
description: "Capacidad #4 — Plugins y Skills — Implementada parcialmente en POCLI."
---

## Qué es

Puntos de extensión declarativos que empaquetan instrucciones reutilizables, flujos por rol, hooks de ciclo de vida e integraciones externas sin modificar el núcleo del harness.

## Por qué importa

Los equipos necesitan adaptar estándares de código, guías de dominio e integraciones sin tener que hacer un fork del runtime del harness.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: `McpRegistry` (`src/runtime/mcp-client.ts`) conecta servidores MCP externos sobre JSON-RPC 2.0 stdio con ACLs por rol, y `src/runtime/harnesses.ts` carga personalizaciones de comportamiento desde `$HOME/.pocli/behavior/system/<role>.md`.

### Pendiente / Hoja de ruta

Cargador declarativo de paquetes de plugins, registro dinámico de skills (`SKILL.md` con hooks de ciclo de vida) y transporte MCP remoto HTTP/SSE.
