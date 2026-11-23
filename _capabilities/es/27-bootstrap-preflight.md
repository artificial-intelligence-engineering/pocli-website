---
title: "Capacidad #27 — Bootstrap / Preflight"
lang: es
cap_number: 27
subsystem: "4.5 Session Lifecycle"
status: "implemented"
permalink: /es/capabilities/27-bootstrap-preflight/
description: "Capacidad #27 — Bootstrap / Preflight — Implementada en POCLI."
---

## Qué es

Valida la preparación del entorno —migraciones de base de datos, credenciales, binarios de sandbox, capacidades de GPU/RAM local y estado del workspace— antes de iniciar la ejecución.

## Por qué importa

Fallar rápido durante el preflight evita quemar tokens de LLM en turnos condenados a fallar por claves ausentes, herramientas rotas o sandboxes no disponibles.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada entre `src/cli.ts`, `src/core/auth.ts`, `src/core/lifecycle.ts`, la inicialización de esquema de `PoCliDatabase` y la inspección de hardware/compatibilidad local (`src/local/hardware.ts`, `src/local/compatibility.ts`).

### Pendiente / Hoja de ruta

Un comando dedicado `pocli doctor` que imprima un informe completo de diagnóstico preflight.

## Referencias

- [Anthropic — Effective Harnesses for Long-Running Agents (Initializer Pattern)](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) — Destaca una fase dedicada de inicialización/preflight para asegurar un entorno limpio.
- [Martin Fowler — Fail Fast](https://www.martinfowler.com/ieeeSoftware/failFast.pdf) — Principio clásico de ingeniería que defiende validar de inmediato antes de ejecutar trabajo costoso.
- [Kubernetes — Startup, Liveness, and Readiness Probes](https://kubernetes.io/docs/concepts/configuration/liveness-readiness-startup-probes/) — Modelo estándar de la industria para verificar la disponibilidad del runtime antes de aceptar carga.
