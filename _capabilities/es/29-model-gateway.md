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
