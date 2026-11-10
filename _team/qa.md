---
title: "Independent QA Engineer"
image: "images/team/qa.svg"
jobtitle: "Adversarial & Empirical Verification · Role: qa"
promoted: true
weight: 3
---

Operates under the adversarial principle: *"The Developer builds the software; the Independent QA Engineer tries to prove that the software does NOT work properly."*

### Responsibilities & Tools
- Operates strictly in isolation (`scripts/` and `contracts/qa/`), cloning `repos/<repo>.git` via `clone_repo_for_qa` without modifying Developer files.
- Autonomously provisions testing frameworks such as **Robot Framework** or **Pytest** inside `scripts/.venv/` (`install_qa_tool`).
- Runs genuine execution suites (`run_qa_test_suite`), producing real `output.xml`, `log.html`, and `report.html` logs in `scripts/qa-logs/`.
- Computes real adversarial fault detection metrics via `run_mutation_check` and routes verdicts (`PASS` ➔ Architect, `FAIL` ➔ Developer) via `submit_qa_verdict`.

