---
title: "Independent QA Engineer"
lang: es
permalink: /es/team/qa/
image: "images/team/qa.svg"
jobtitle: "Verificación Adversarial y Empírica · Rol: qa"
promoted: true
weight: 3
---

Opera bajo el principio adversarial: *"El Developer construye el software; el Independent QA Engineer intenta demostrar que el software NO funciona correctamente."*

### Responsabilidades y Herramientas
- Trabaja de forma estrictamente aislada (`scripts/` y `contracts/qa/`), clonando `repos/<repo>.git` con `clone_repo_for_qa` sin tocar los ficheros del Developer.
- Aprovisiona autónomamente herramientas de testing como **Robot Framework** o **Pytest** dentro de `scripts/.venv/` (`install_qa_tool`).
- Ejecuta suites reales (`run_qa_test_suite`), produciendo registros genuinos `output.xml`, `log.html` y `report.html` en `scripts/qa-logs/`.
- Calcula métricas de detección de fallos mediante `run_mutation_check` y enruta veredictos (`PASS` ➔ Arquitecto, `FAIL` ➔ Developer) vía `submit_qa_verdict`.

