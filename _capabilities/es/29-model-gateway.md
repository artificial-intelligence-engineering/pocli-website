---
title: "Capacidad #29 — Model Gateway"
lang: es
cap_number: 29
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "implemented"
permalink: /es/capabilities/29-model-gateway/
description: "Capacidad #29 — Model Gateway — Implementada en POCLI."
---

## Qué es

Una abstracción unificada de proveedores que normaliza peticiones, parseo de respuestas, limpieza de etiquetas de razonamiento y credenciales entre backends cloud y locales.

## Por qué importa

Acoplarse a un único proveedor LLM genera dependencia y expone los flujos a caídas, cambios de precios y dialectos incompatibles de API.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `LLMGateway` (`src/runtime/llm-gateway.ts`) y `src/local/adapters/llamacpp.ts`, unificando OpenRouter, Groq, Cerebras, Gemini, Pollinations, Ollama, llama.cpp, Anthropic y OpenAI con saneamiento `cleanModelOutput()`.

### Pendiente / Hoja de ruta

Soporte unificado de salida estructurada nativa (`response_format`) en todos los adaptadores.

## Referencias

- [Chip Huyen — AI Engineering (Model Integration & Gateways)](https://www.oreilly.com/library/view/ai-engineering/9781098166298/) — Cubre pasarelas LLM unificadas, normalización, fallback y abstracción de proveedores en producción.
- [OpenRouter API Documentation](https://openrouter.ai/docs) — Referencia para enrutamiento y normalización multiproveedor compatible con OpenAI.
- [llama.cpp — Local LLM Inference Engine](https://github.com/ggml-org/llama.cpp) — Motor open-source de inferencia local GGUF integrado en el adaptador local de POCLI.
