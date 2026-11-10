---
title: "QA Autónoma y Robot Framework"
lang: es
permalink: /es/services/autonomous-qa-robot/
weight: 3
---

Siguiendo el principio estricto de **"No Auto-Revisión"**, el Senior Developer jamás valida su propio código. Cuando las pruebas unitarias están al 100% en verde y los contratos `DEV-GHERKIN-*` quedan listos, el flujo pasa automáticamente al **Independent QA Engineer**.

## Flujo Empírico de QA en 7 Fases

1. **Descubrimiento Aislado:** Clona limpiamente `repos/<repo>.git` en `scripts/qa-env/<repo>` sin alterar los archivos del Developer.
2. **Contratos Conductuales y Adversariales:** Redacta features `REQ-GHERKIN-*`, adversariales `QA-GHERKIN-*` y de regresión `REG-GHERKIN-*` en `contracts/qa/`.
3. **Aprovisionamiento Autónomo de Herramientas (`install_qa_tool`):** Crea automáticamente `scripts/.venv/` e instala `robotframework` o `pytest` bajo demanda en el entorno aislado de QA.
4. **Ejecución Real de Suites:** Ejecuta pruebas reales mediante `run_qa_test_suite`, generando informes genuinos de Robot Framework: `output.xml`, `log.html` y `report.html` en `scripts/qa-logs/`.
5. **Testing de Mutación Adversarial (`run_mutation_check`):** Inyecta fallos controlados sobre una copia desechable en `scripts/qa-mutation/` para medir el `mutationScore` real.
6. **Bucle de Corrección Bidireccional (`QA <-> DEV -> ARQ`):** Devuelve defectos reproducibles (`DEF-*`) al Developer en caso de `FAIL`, o remite la tabla resumen verificada directamente al Arquitecto si resulta `PASS`.

