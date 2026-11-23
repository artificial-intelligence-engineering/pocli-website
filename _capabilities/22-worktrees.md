---
title: "Capability #22 — Worktrees"
cap_number: 22
subsystem: "4.4 Scope"
status: "not_implemented"
permalink: /capabilities/22-worktrees/
description: "Capability #22 — Worktrees — Not Yet Implemented in POCLI."
---

## What It Is

Physical Git workspace isolation (`git worktree`) giving each agent task or parallel worker its own independent checkout without colliding on uncommitted files.

## Why It Matters

Parallel agents editing the same working directory corrupt each other's builds, git index, and test runs.

## Implementation Status in POCLI

**Status:** Not Yet Implemented

Not yet implemented. POCLI currently isolates projects by workspace directory and OS-level process sandboxing (`LinuxAgentProcessRunner`), operating on a single active checkout per project.

### Pending / Roadmap

Automated `git worktree` provisioning, branch lifecycle management, and cleanup to support concurrent parallel developer workers.
