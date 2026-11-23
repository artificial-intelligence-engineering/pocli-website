---
title: "Capacidad #19 — Ejecución Segura / Sandbox"
lang: es
cap_number: 19
subsystem: "4.4 Scope"
status: "implemented"
permalink: /es/capabilities/19-safe-execution-sandboxing/
description: "Capacidad #19 — Ejecución Segura / Sandbox — Implementada en POCLI."
---

## Qué es

Impone aislamiento a nivel de sistema operativo (procesos, sistema de archivos y namespaces) sobre los comandos ejecutados por el agente para que código defectuoso o inseguro no dañe el host.

## Por qué importa

Las instrucciones en el prompt no bastan para impedir que un comando alucinado borre archivos o filtre credenciales fuera del workspace.

## Estado e Implementación en POCLI

**Estado:** Implementada

Implementada en `LinuxAgentProcessRunner` (`src/runtime/process-runner.ts`), aislando los workers mediante Linux Bubblewrap (`/usr/bin/bwrap --unshare-pid`) o contenedores OCI Podman, además de entornos Python `.venv` aislados para QA.

### Pendiente / Hoja de ruta

Filtros `seccomp` obligatorios por defecto y políticas granulares de bloqueo de red por herramienta incluso en modo local ligero.

## Referencias

- [Bubblewrap (`bwrap`) — Unprivileged Linux Sandboxing](https://github.com/containers/bubblewrap) — Sandbox ligero basado en namespaces de Linux (`--unshare-pid`, aislamiento de montajes) usado por POCLI.
- [Podman — Rootless OCI Containers](https://podman.io/) — Motor de contenedores OCI sin demonio y sin root que aporta aislamiento fuerte para agentes.
- [Linux Kernel Documentation — Namespaces & Seccomp BPF](https://www.kernel.org/doc/html/latest/userspace-api/seccomp_filter.html) — Primitivas del kernel Linux para restringir llamadas al sistema y visibilidad de procesos.
