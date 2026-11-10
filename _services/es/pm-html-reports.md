---
title: "Agente PM e Informes 100% HTML"
lang: es
permalink: /es/services/pm-html-reports/
weight: 4
---

El **Project Manager (PM)** ofrece visibilidad unificada de todos los especialistas virtuales sin interferir nunca en contratos técnicos ni código fuente.

## Entregable Integral HTML en `deliveries/`

Invocado por chat natural con el PM, con el comando `/report` o mediante `pocli report [proyecto]`, el PM genera un **informe 100% HTML autónomo** en `deliveries/project-status-report.html`:

- **Banner de Estado de Construcción en Vivo:** Detecta si hay agentes trabajando o fases abiertas (`🚧 PROYECTO EN CONSTRUCCIÓN`) frente a entregas completadas y aceptadas por el PO (`✅ PROYECTO FINALIZADO`).
- **Resumen Técnico Completo:** Consolida Arquitecturas (`ARCH-*`), Especificaciones (`SPEC-*`), Repositorios Git y Bitácoras (`IMP-*`), Pruebas Unitarias (métrica 100% green), `DEV-GHERKIN-*` y veredictos de QA.
- **Métricas Cuantitativas desde SQLite:** **Matriz completa de interacción entre agentes** (`from_role -> to_role`), conteo de mensajes, tokens estimados, desglose de artefactos y tiempos de ejecución.
- **Enlaces Directos:** Accesos directos a todos los `.md` y `.feature`, copias de los System Prompts (`deliveries/system-prompts/*.md`) e informes HTML/XML de **Robot Framework** (`log.html`, `report.html`, `output.xml`).

