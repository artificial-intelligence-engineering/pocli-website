---
title: "Contexto en 3 Niveles y SQLite DAG"
lang: es
permalink: /es/services/3-tier-context-sqlite/
weight: 2
---

Construido sobre **Node.js Native SQLite (`node:sqlite`)** en modo `WAL + FTS5`, **POCLI** almacena todo el historial de ingeniería en `$HOME/.pocli/pocli.sqlite` sin dependencias de compilación nativa C++.

## Ensamblado Contextual en 3 Niveles

En cada turno de agente, `PoCliOrchestrator` construye un prompt optimizado para caché directamente desde SQLite:

1. **Nivel 1 (Prefijo Normativo Cacheable):** Índice conciso de artefactos autoritativos (`[ARCH-001 v1 | APPROVED]`, `[SPEC-001 v1]`) en lugar de volcar ficheros completos.
2. **Nivel 2 (Memoria en 4 Capas y Checkpoints de Compactación):** Hasta 8 memorias persistentes prioritarias junto al último resumen estructurado generado por `/compact` en `context_compactions`.
3. **Nivel 3 (Ventana Reciente Activa):** Estrictamente los últimos **6 turnos hoja no compactados** del árbol de sesiones DAG (`parent_id`).

## REPL SQLite Interactivo `pocli db`

Consulta tu workspace de ingeniería en cualquier momento desde la terminal o dentro de la TUI con `/db`:

```bash
pocli db path
pocli db ".tables"
pocli db "SELECT code, type, status FROM artifacts;" --format table
```

