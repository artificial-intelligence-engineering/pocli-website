---
title: "Linux Sandboxing & Multi-Model Router"
weight: 6
---

Every virtual specialist executes in an independent **Linux child process** communicating via newline-delimited **`JSON-RPC 2.0` over `stdio`**, keeping the React/Ink terminal UI responsive at 60 FPS.

## OS-Level Process Sandboxing & MCP

- **Execution Modes:** Supports `LOCAL_PROCESS`, unprivileged Linux namespace isolation via **Bubblewrap (`LINUX_BWRAP`)**, and rootless **Podman (`OCI_CONTAINER`)**.
- **Model Context Protocol (MCP):** Role-scoped MCP client over `JSON-RPC 2.0` for safe external tool integration.
- **Per-Agent Multi-Model Routing (`/models`):** Assign distinct providers and models to `architect`, `developer`, `qa`, and `pm` independently—spanning OpenCode Zen (`gemini-3.8-flash`), Google Gemini, Anthropic, OpenAI, and local **Ollama / `llama.cpp`**, backed by smart bandit failover (`LLMRouter`).

