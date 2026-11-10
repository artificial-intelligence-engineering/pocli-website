---
title: "Autonomous QA & Robot Framework"
weight: 3
---

Following the strict **"No Self-Review"** engineering principle, the Senior Developer never validates their own code. Once unit tests are 100% green and `DEV-GHERKIN-*` contracts are written, work flows autonomously to the **Independent QA Engineer**.

## 7-Phase Empirical QA Workflow

1. **Isolated Discovery:** Clones `repos/<repo>.git` cleanly into `scripts/qa-env/<repo>` without touching Developer source files.
2. **Behavioral & Adversarial Contracts:** Authors `REQ-GHERKIN-*`, adversarial `QA-GHERKIN-*`, and regression `REG-GHERKIN-*` features under `contracts/qa/`.
3. **Autonomous Tool Provisioning (`install_qa_tool`):** Automatically creates `scripts/.venv/` and installs `robotframework` or `pytest` on demand inside the isolated QA workspace.
4. **Real Suite Execution:** Executes suites via `run_qa_test_suite`, generating genuine Robot Framework artifacts: `output.xml`, `log.html`, and `report.html` in `scripts/qa-logs/`.
5. **Adversarial Mutation Testing (`run_mutation_check`):** Injects faults into a disposable copy in `scripts/qa-mutation/` to compute real `mutationScore`.
6. **Bidirectional Correction (`QA <-> DEV -> ARQ`):** Returns reproducible defects (`DEF-*`) to the Developer on `FAIL`, or delivers a verified Summary Table directly to the Architect on `PASS`.

