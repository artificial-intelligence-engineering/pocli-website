---
title: Inicio Rápido
lang: es
layout: page
permalink: /es/quickstart/
description: "Instala, configura modelos, lanza el Command Center TUI de POCLI, consulta SQLite con pocli db y genera informes HTML del PM."
bodyClass: page-about
---

Empieza a usar **POCLI** en segundos sobre Linux.

## 1. Instalación en Un Solo Comando (Recomendado)

Descarga el último tarball de GitHub Releases, instala Node.js LTS automáticamente en `~/.pocli/runtime/node/` si falta y deja el ejecutable listo en `~/.local/bin/pocli`:

```bash
curl -fsSL https://artificial-intelligence-engineering.github.io/pocli/install.sh | sh
```

Configura tu proveedor LLM y arranca el entorno:

```bash
pocli auth status
pocli
```

## 2. Instalar desde Código Fuente (Desarrollo)

```bash
git clone https://github.com/artificial-intelligence-engineering/pocli.git
cd pocli
npm install
npm run build
```

## 3. Comandos CLI Esenciales

```bash
# Interfaz TUI interactiva a pantalla completa (Ink)
pocli

# Generar informe de estado PM 100% HTML autónomo
pocli report <nombre-proyecto>

# Abrir el REPL SQLite central ($HOME/.pocli/pocli.sqlite)
pocli db
pocli db "SELECT id, name, phase FROM projects;" --format json

# Asignar modelos de forma global o independiente por agente
pocli models
pocli models developer ollama/qwen2.5-coder:14b

# Ejecutar la suite completa de tests desde el repositorio
npm test
```

## 4. Comandos Esenciales de la TUI Interactiva

Pulsa **`Ctrl+Tab`** en cualquier momento para alternar entre la **Vista Limpia estilo OpenCode** y el **Command Center Multipanel**. Escribe **`/`** para desplegar el menú interactivo de comandos:

| Comando | Acción |
| :--- | :--- |
| `/project` | Crea un proyecto en un directorio, inicializa `.pocli/artifacts` y autodescubre repositorios Git. |
| `/projects` | Lista y cambia entre proyectos activos en SQLite. |
| `/architect`, `/developer`, `/qa`, `/pm` | Cambia el especialista activo o lanza consultas paralelas/secuenciales del PM. |
| `/approve`, `/handoff`, `/accept` | Puertas de gobierno del Product Owner humano a lo largo del flujo SDLC. |
| `/validate` | Lanza la verificación independiente de QA con ejecución real aislada. |
| `/report` | Genera el Informe de Estado del Proyecto 100% HTML en `deliveries/project-status-report.html`. |
| `/compact [all]` | Condensa turnos antiguos en checkpoints DAG de SQLite liberando tokens. |
| `/system` | Inspecciona los system prompts activos y overrides locales (`~/.pocli/behavior/system/`). |
| `/db` | Ejecuta consultas SQL o dot-commands (`.tables`, `.experts`, `.stats`) dentro de la TUI. |
| `/settings` | Cambia idioma de interfaz (`en`/`es`), temas visuales y directorio de trabajo central. |

## 5. Personalizar Prompts de Agentes

Sobreescribe el prompt de cualquier agente sin modificar el repositorio base:

```bash
mkdir -p ~/.pocli/behavior/system
cp behavior/system/developer.md ~/.pocli/behavior/system/developer.md
# Edita ~/.pocli/behavior/system/developer.md para inyectar reglas de tu equipo
```

## 6. Comunidad y Código Fuente

- **Repositorio Principal**: [github.com/artificial-intelligence-engineering/pocli](https://github.com/artificial-intelligence-engineering/pocli)
- **Issues y Sugerencias**: [github.com/artificial-intelligence-engineering/pocli/issues](https://github.com/artificial-intelligence-engineering/pocli/issues)
- **Código del Sitio Web**: [github.com/artificial-intelligence-engineering/pocli-website](https://github.com/artificial-intelligence-engineering/pocli-website)

