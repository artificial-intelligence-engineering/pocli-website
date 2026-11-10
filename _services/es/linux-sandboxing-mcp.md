---
title: "Sandboxing Linux y Router Multi-Modelo"
lang: es
permalink: /es/services/linux-sandboxing-mcp/
weight: 6
---

Cada especialista virtual se ejecuta en un **proceso hijo independiente en Linux** comunicándose por **`JSON-RPC 2.0` sobre `stdio`** delimitado por saltos de línea, manteniendo fluida la interfaz terminal Ink/React.

## Aislamiento OS y Protocolo MCP

- **Modos de Ejecución:** Soporta `LOCAL_PROCESS`, aislamiento por namespaces Linux sin privilegios con **Bubblewrap (`LINUX_BWRAP`)** y contenedores rootless **Podman (`OCI_CONTAINER`)**.
- **Model Context Protocol (MCP):** Cliente MCP sobre `JSON-RPC 2.0` con permisos granulares por rol para herramientas externas seguras.
- **Enrutamiento Multi-Modelo por Agente (`/models`):** Asigna proveedores y modelos distintos de forma independiente a `architect`, `developer`, `qa` y `pm`—compatibles con OpenCode Zen (`gemini-3.8-flash`), Google Gemini, Anthropic, OpenAI y **Ollama / `llama.cpp`** locales, respaldados por failover inteligente (`LLMRouter`).

