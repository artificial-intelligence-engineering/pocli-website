---
title: "PM Agent & 100% HTML Reports"
weight: 4
---

The **Project Manager (PM)** provides unified visibility across all virtual engineering specialists without ever interfering with technical contracts or code.

## Comprehensive `deliveries/` HTML Deliverable

Invoked via natural chat with PM, the `/report` slash command, or `pocli report [project]`, the PM produces a **100% self-contained HTML report** in `deliveries/project-status-report.html`:

- **Live Construction Status Banner:** Detects whether agents are actively working / phases are incomplete (`🚧 PROYECTO EN CONSTRUCCIÓN`) vs finished and PO-accepted (`✅ PROYECTO FINALIZADO`).
- **End-to-End Engineering Summary:** Consolidates Reference Architectures (`ARCH-*`), Specifications (`SPEC-*`), Developer Repositories & Logbooks (`IMP-*`), Unit Tests (100% green metrics), `DEV-GHERKIN-*`, and QA verdicts.
- **SQLite Quantitative Metrics:** Full **inter-agent communication matrix** (`from_role -> to_role`), message counts, estimated tokens, artifact breakdown, and elapsed execution times.
- **Direct File Links:** Clickable links to all `.md` and `.feature` artifacts, mirrored System Prompts (`deliveries/system-prompts/*.md`), and **Robot Framework** reports (`log.html`, `report.html`, `output.xml`).

