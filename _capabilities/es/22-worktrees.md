---
title: "Capacidad #22 — Worktrees"
lang: es
cap_number: 22
subsystem: "4.4 Scope"
status: "not_implemented"
permalink: /es/capabilities/22-worktrees/
description: "Capacidad #22 — Worktrees — Todavía no implementada en POCLI."
---

## Qué es

Aislamiento físico del repositorio mediante `git worktree`, asignando a cada tarea o worker paralelo su propia copia de trabajo sin colisionar en archivos sin confirmar.

## Por qué importa

Agentes paralelos editando el mismo directorio de trabajo corrompen mutuamente compilaciones, el índice de git y las ejecuciones de tests.

## Estado e Implementación en POCLI

**Estado:** Todavía no implementada

Todavía no implementada. POCLI aísla actualmente los proyectos por directorio de workspace y sandboxing a nivel de sistema operativo (`LinuxAgentProcessRunner`), operando sobre un único checkout activo por proyecto.

### Pendiente / Hoja de ruta

Aprovisionamiento automático de `git worktree`, gestión del ciclo de vida de ramas y limpieza para soportar workers de desarrollo en paralelo.

## Referencias

- [Git Official Documentation — `git-worktree`](https://git-scm.com/docs/git-worktree) — Referencia oficial para gestionar múltiples árboles de trabajo aislados ligados a un mismo repositorio.
- [Anthropic — Claude Code Best Practices (Parallel Worktrees)](https://www.anthropic.com/engineering/claude-code-best-practices) — Flujo práctico para ejecutar múltiples agentes de código en paralelo usando Git worktrees.
- [Pro Git Book — Branching & Repository Internals](https://git-scm.com/book/en/v2) — Referencia fundamental sobre el modelo de objetos de Git que permite checkouts paralelos sin duplicar historial.
