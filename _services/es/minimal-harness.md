---
title: "Minimal Harness y Eficiencia de Tokens"
lang: es
permalink: /es/services/minimal-harness/
weight: 1
---

Inspirado en **Pi (`pi-mono`)** y en los hallazgos empíricos de *Harness Engineering* (`arXiv:2609.00006`), **POCLI** sustituye prompts monolíticos de más de 15,000 tokens por harnesses específicos por rol de **150–250 tokens**.

## Por Qué Importa el Tamaño del System Prompt

Cada token del system prompt se re-procesa en cada turno conversacional, multiplicando costes de API y el *Time-To-First-Token* (TTFT)—especialmente en modelos locales (`Ollama`, `llama.cpp`) o niveles gratuitos con límites de cuota.

| Entorno | Sobrecarga del System Prompt | Enfoque de Diseño |
| :--- | :--- | :--- |
| **Claude Code** | ~25,000 tokens | Manuales extensos de herramientas y reglas de estilo monolíticas |
| **OpenCode / Codex** | 10,000 – 15,000 tokens | Esquemas JSON pesados de múltiples herramientas |
| **Pi Agent** | 500 – 900 tokens | Directrices mínimas esenciales |
| **POCLI** | **150 – 250 tokens** | **Harnesses ultra-concisos acotados por rol** |

## Preservando el 90–95% de la Ventana de Contexto

- Cada agente recibe únicamente las herramientas necesarias para su rol (`Architect`: ~140 tokens, `Developer`: ~105 tokens, `QA`: ~70 tokens, `PM`: ~130 tokens).
- La carga media por turno es de **600–1,200 tokens**, logrando **TTFT sub-segundo** y dejando libre entre un **90% y un 95% de contexto** para código fuente real, diffs y citas RAG.
- Los prompts residen limpiamente en `behavior/system/*.md` y admiten overrides personales en `$HOME/.pocli/behavior/system/`.

