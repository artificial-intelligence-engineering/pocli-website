---
title: "Software Architect"
image: "images/team/architect.svg"
jobtitle: "Primary Technical Interlocutor · Role: architect"
promoted: true
weight: 1
---

Primary technical interlocutor with the human **Product Owner**. Discusses system vision, trade-offs, and technology choices conversationally before codifying governance contracts.

### Responsibilities & Tools
- Maintains two authoritative versioned contracts under `contracts/`:
  - **Reference Architecture (`ARCH-*`)**: Design boundaries, system topology, and security posture.
  - **Developer Specification (`SPEC-*`)**: Data models, REST/CLI APIs, and target Git repository under `repos/<project>.git`.
- Never marks an architecture as approved unilaterally—invokes `request_po_approval` and `handoff_to_developer` only upon explicit Product Owner consent.
- Resolves formal technical block consultations escalated by the Developer (`consult_architect`) and receives final empirical QA summary tables (`[QA -> ARQ]`).

