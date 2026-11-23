---
title: "Capability #19 — Safe Execution & Sandboxing"
cap_number: 19
subsystem: "4.4 Scope"
status: "implemented"
permalink: /capabilities/19-safe-execution-sandboxing/
description: "Capability #19 — Safe Execution & Sandboxing — Implemented in POCLI."
---

## What It Is

Enforces OS-level process, filesystem, and namespace isolation around agent-executed commands so untrusted or buggy code cannot damage the host system.

## Why It Matters

Prompt instructions alone cannot stop a hallucinated shell command from deleting files or leaking credentials outside the project workspace.

## Implementation Status in POCLI

**Status:** Implemented

Implemented in `LinuxAgentProcessRunner` (`src/runtime/process-runner.ts`), isolating agent workers with Linux Bubblewrap (`/usr/bin/bwrap --unshare-pid`) or Podman OCI containers, plus isolated Python `.venv` environments for QA execution.

### Pending / Roadmap

Mandatory default `seccomp` filters and fine-grained per-tool network-deny policies even in lightweight local mode.
