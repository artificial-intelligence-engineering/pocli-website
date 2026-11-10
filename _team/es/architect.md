---
title: "Software Architect"
lang: es
permalink: /es/team/architect/
image: "images/team/architect.svg"
jobtitle: "Interlocutor Técnico Principal · Rol: architect"
promoted: true
weight: 1
---

Interlocutor técnico principal con el **Product Owner** humano. Debate la visión del sistema, los compromisos técnicos y la selección tecnológica antes de emitir contratos de gobierno.

### Responsabilidades y Herramientas
- Mantiene dos contratos autoritativos versionados bajo `contracts/`:
  - **Arquitectura de Referencia (`ARCH-*`)**: Límites de diseño, topología del sistema y postura de seguridad.
  - **Especificación Técnica (`SPEC-*`)**: Modelos de datos, APIs REST/CLI y repositorio Git destino en `repos/<project>.git`.
- Nunca aprueba una arquitectura unilateralmente: invoca `request_po_approval` y `handoff_to_developer` solo tras la autorización explícita del Product Owner.
- Resuelve consultas formales escaladas por el Developer (`consult_architect`) y recibe las tablas empíricas de resultados desde QA (`[QA -> ARQ]`).

