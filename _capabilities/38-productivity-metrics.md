---
title: "Capability #38 — Productivity Metrics"
cap_number: 38
subsystem: "4.6 Pure Operational Runtime Layer"
status: "partial"
permalink: /capabilities/38-productivity-metrics/
description: "Capability #38 — Productivity Metrics — Partially Implemented in POCLI."
---

## What It Is

Measures delivery throughput, QA rework cycles, defect rates, and phase completion times across engineering projects.

## Why It Matters

Engineering leaders need objective delivery metrics—not just raw token counts—to verify that AI agents accelerate quality software delivery.

## Implementation Status in POCLI

**Status:** Partially Implemented

Partially implemented: `PmReporter` (`src/runtime/pm-reporter.ts`) generates self-contained HTML delivery reports in `deliveries/` summarizing phase milestones, artifacts, and QA verification results.

### Pending / Roadmap

Longitudinal cycle-time, first-pass QA rate, and throughput analytics aggregated across multiple projects.
