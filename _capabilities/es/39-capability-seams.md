---
title: "Capacidad #39 — Capability Seams"
lang: es
cap_number: 39
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "implemented"
permalink: /es/capabilities/39-capability-seams/
description: "Capacidad #39 — Capability Seams — Implementada en POCLI."
---

## Qué es

Fronteras arquitectónicas limpias (interfaces y adaptadores) que desacoplan proveedores LLM, sandboxes, motores de almacenamiento y registros de herramientas externas de la lógica de orquestación.

## Por qué importa

El ecosistema de IA evoluciona rápido; unas costuras limpias permiten sustituir modelos, runtimes o backends de aislamiento sin reescribir el harness.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en toda la arquitectura modular de POCLI: `LLMGateway` / `LLMRouter` (capa de modelos), `src/local/adapters/llamacpp.ts` (inferencia local), `LinuxAgentProcessRunner` (sandbox Bubblewrap/Podman), `McpRegistry` (herramientas MCP) y `PoCliDatabase` (persistencia SQLite).

### Pendiente / Hoja de ruta

Publicar interfaces formales de SDK en TypeScript para cargar adaptadores de terceros dinámicamente fuera del repositorio principal.

## Referencias

- [Michael Feathers — Working Effectively with Legacy Code (Seams)](https://www.oreilly.com/library/view/working-effectively-with/0131177052/) — Origen del concepto de *seam* (costura): un punto donde cambiar comportamiento sin editar el núcleo.
- [Alistair Cockburn — Hexagonal Architecture (Ports and Adapters)](https://alistair.cockburn.us/hexagonal-architecture/) — Patrón arquitectónico que aísla la orquestación del dominio de proveedores, bases de datos y herramientas.
- [Martin Fowler — Inversion of Control Containers and the Dependency Injection Pattern](https://martinfowler.com/articles/injection.html) — Guía fundamental para desacoplar adaptadores intercambiables detrás de interfaces limpias.
