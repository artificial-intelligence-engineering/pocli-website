---
title: "Senior Developer"
image: "images/team/developer.svg"
jobtitle: "Implementation & Unit Testing · Role: developer"
promoted: true
weight: 2
---

Constructs clean, modular software strictly adhering to approved normative contracts (`ARCH-*` and `SPEC-*`), never silently altering architectural boundaries.

### Responsibilities & Tools
- Initializes and writes code cleanly inside Git repositories under `repos/<repo>.git` (`init_repository`, `write_source_file`).
- Writes comprehensive unit test suites and executes `run_unit_tests` until **100% green** before any handoff.
- Authors **Developer Gherkin** behavioral scenarios (`contracts/qa/DEV-GHERKIN-*.feature`) and technical logbooks (`contracts/implementation/IMP-*.md`).
- Escalates architectural ambiguities to the Architect via `consult_architect` and triggers QA autonomously via `submit_for_qa`, resolving any reported regressions in `[QA <-> DEV]` correction loops.

