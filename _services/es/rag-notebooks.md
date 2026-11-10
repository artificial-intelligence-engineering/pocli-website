---
title: "Knowledge Notebooks y RAG Híbrido"
lang: es
permalink: /es/services/rag-notebooks/
weight: 5
---

POCLI adapta las investigaciones sobre citas verificables (`arXiv:2311.09533`) y el paradigma **NotebookLM / Open Notebook** directamente sobre tu sistema de ficheros Linux local.

## Recuperación Híbrida con Citas Trazables

- **Notebooks Respaldados por Directorios:** Mapea documentación Markdown local, especificaciones, ADRs o guías de dominio en Knowledge Notebooks acotados por rol.
- **Indexado Incremental SHA-256:** Vigilancia de archivos en vivo en Linux (`fs.watch`) que únicamente reindexa documentos modificados.
- **Puntuación Híbrida:** Combina ranking léxico **SQLite FTS5 BM25** con similitud vectorial coseno.
- **Trazabilidad Obligatoria:** Las respuestas de los agentes adjuntan citas verificables en línea (`[Notebook | Documento | Sección (Líneas)]`), manteniendo respuestas auditables y precisas.

