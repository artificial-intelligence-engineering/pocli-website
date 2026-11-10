---
title: "Knowledge Notebooks & Hybrid RAG"
weight: 5
---

POCLI adapts grounded citation research (`arXiv:2311.09533`) and the **NotebookLM / Open Notebook** paradigm directly onto your local Linux filesystem.

## Hybrid Retrieval with Verifiable Citations

- **Directory-Backed Notebooks:** Map local Markdown, architecture specs, ADRs, or domain docs into role-scoped Knowledge Notebooks.
- **Incremental SHA-256 Indexing:** Live Linux filesystem watching (`fs.watch`) only re-indexes modified documents.
- **Hybrid Scoring:** Combines **SQLite FTS5 BM25** lexical ranking with vector cosine similarity.
- **Mandatory Traceability:** Agent responses attach verifiable inline source citations (`[Notebook | Document | Section (Lines)]`), keeping grounding crisp and auditable.

