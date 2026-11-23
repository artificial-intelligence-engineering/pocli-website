---
title: "Capacidad #35 — Delegación a Sub-Agentes"
lang: es
cap_number: 35
subsystem: "4.6 Capa de Runtime Operativo Puro"
status: "partial"
permalink: /es/capabilities/35-sub-agent-delegation/
description: "Capacidad #35 — Delegación a Sub-Agentes — Implementada parcialmente en POCLI."
---

## Qué es

Lanza sub-agentes enfocados con contexto acotado para resolver subtareas concretas (investigación, módulos independientes, pruebas) y devolver resúmenes concisos.

## Por qué importa

Delegar exploración ruidosa o trabajo paralelo en módulos mantiene limpio el contexto principal y acelera la entrega.

## Estado e Implementación en POCLI

**Estado:** Implementada parcialmente

Implementada parcialmente: `PoCliOrchestrator` delega fases del SDLC entre workers especialistas persistentes (`architect`, `developer`, `qa`, `pm`) con ventanas de contexto aisladas.

### Pendiente / Hoja de ruta

Lanzamiento dinámico de sub-agentes efímeros en paralelo (fan-out / fan-in) sobre partes disjuntas del código.
