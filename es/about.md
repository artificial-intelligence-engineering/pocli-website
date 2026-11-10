---
title: Arquitectura e Investigación
lang: es
layout: page
permalink: /es/about/
description: "Arquitectura modular en tiempo de ejecución, ensamblado contextual en 3 niveles, system prompts en cascada, ADRs y fundamentos de investigación open-source de POCLI."
bodyClass: page-about
---

POCLI es un entorno nativo Linux TUI/CLI de ingeniería de software construido sobre TypeScript, Ink, Yoga Layout, SQLite nativo de Node.js (`WAL` + `FTS5`) y aislamiento de procesos a nivel de sistema operativo.

## 1. Pipeline de Ejecución y Aislamiento de Procesos

Los harness estáticos por rol (`behavior/system/*.md`, solo **150–250 tokens** por agente) y el estado dinámico del proyecto desde SQLite (`$HOME/.pocli/pocli.sqlite`) se ensamblan en cada turno dentro de una ventana acotada de **600–1,200 tokens** y se despachan por `JSON-RPC 2.0` sobre `stdio` hacia procesos hijo dedicados en Linux:

```text
behavior/system/*.md (150-250 tokens)
        +
Contexto SQLite (Nivel 1 + Nivel 2 Compactación + Nivel 3 DAG)
        │
        ▼  src/runtime/orchestrator.ts
Proceso Hijo Linux (JSON-RPC 2.0 stdio | bwrap / OCI)
```

Esta arquitectura multiproceso garantiza que la inferencia de los agentes nunca bloquee la consola interactiva Ink a pantalla completa ni mezcle estado conversacional entre especialistas.

---

## 2. Módulos Principales (`src/`)

| Módulo | Responsabilidad |
| :--- | :--- |
| `src/core/contracts.ts` y `workflow.ts` | Esquemas de dominio Zod, **máquina de estados SDLC de 8 fases**, `AuthorityGuard` e internacionalización `en`/`es`. |
| `src/storage/database.ts` | Persistencia nativa en `node:sqlite` (`WAL` + `FTS5`), artefactos versionados con hash SHA-256, aprobaciones, informes QA y memoria en 4 capas. |
| `src/runtime/harnesses.ts` | Registro de harnesses por rol con resolución en cascada (`~/.pocli/behavior/system/` > `behavior/system/` del repo > fallback). |
| `src/runtime/notebook-rag.ts` | Knowledge Notebooks en sistema de ficheros, indexado incremental SHA-256, `fs.watch` y recuperación híbrida `BM25 + similitud coseno`. |
| `src/runtime/process-runner.ts` | Lanzamiento de procesos hijo dedicados con modos `LOCAL_PROCESS`, Bubblewrap (`LINUX_BWRAP`) y Podman (`OCI_CONTAINER`). |
| `src/runtime/orchestrator.ts` y `pm-reporter.ts` | Coordinación multi-agente, bucles autónomos `[DEV <-> QA -> ARQ]` y entregables 100% HTML del PM. |
| `src/tui/CommandCenterApp.tsx` | Interfaz Ink a pantalla completa con vista limpia estilo OpenCode, menú `/` interactivo y vista multipanel con `Ctrl+Tab`. |

---

## 3. Registros de Decisiones Arquitectónicas (ADRs)

Las decisiones completas de diseño viven en el repositorio principal [`pocli`](https://github.com/artificial-intelligence-engineering/pocli/tree/main/docs/adr):

- **ADR-000**: Matriz comparativa de referentes Open Source (*OpenCode, Pi, Slipwright, AWS CAO, Open Orchestra, Open Notebook, TinySDLC*).
- **ADR-001**: Arquitectura modular, IPC `JSON-RPC 2.0`, `node:sqlite` + `FTS5`, Notebooks RAG y Sandboxing en Linux.
- **ADR-002**: Desarrollo Agéntico Gobernado, límites de autoridad y validación humana obligatoria.
- **ADR-003**: Estado en vivo de workers en vista multipanel e inspector de contexto/memoria.

---

## 4. Fundamentos de Investigación

POCLI sintetiza patrones probados de la comunidad open-source en lugar de reinventar la rueda:

- **Harness Engineering ([arXiv:2609.00006](https://arxiv.org/abs/2609.00006))**: Base teórica de la filosofía *Minimal Harness*, herramientas acotadas por rol y recuperación determinista frente a frameworks sobrecargados.
- **Pi (`pi-mono`)**: Disciplina minimalista de system prompts, TTFT sub-segundo, árbol de sesiones DAG (`parent_id`) y checkpoints estructurados con `/compact`.
- **OpenCode**: Estética Command Center a pantalla completa en terminal, paleta interactiva `/` y REPL SQLite interactivo `pocli db`.
- **TinySDLC y Slipwright**: Principio estricto de *"No Auto-Revisión"* y puertas deterministas con intervención humana.
- **Citas Verificables ([arXiv:2311.09533](https://arxiv.org/abs/2311.09533))**: Inspiración para citas verificables tipo NotebookLM (`[Notebook | Documento | Sección]`).

