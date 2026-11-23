---
title: "Capability #29 — Model Gateway"
cap_number: 29
subsystem: "4.6 Pure Operational Runtime Layer"
status: "implemented"
permalink: /capabilities/29-model-gateway/
description: "Capability #29 — Model Gateway — Implemented in POCLI."
---

## What It Is

A unified provider abstraction normalizing request payloads, response parsing, reasoning-tag sanitization, and credentials across cloud and local LLM backends.

## Why It Matters

Hardcoding a single LLM vendor creates lock-in and exposes workflows to vendor outages, pricing shifts, and incompatible API dialects.

## Implementation Status in POCLI

**Status:** Implemented

Implemented in `LLMGateway` (`src/runtime/llm-gateway.ts`) and `src/local/adapters/llamacpp.ts`, unifying OpenRouter, Groq, Cerebras, Gemini, Pollinations, Ollama, llama.cpp, Anthropic, and OpenAI with `cleanModelOutput()` sanitization.

### Pending / Roadmap

Unified native structured-output (`response_format`) enforcement across all supported adapters.
