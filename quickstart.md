---
title: Quick Start
layout: page
description: "Install, configure models, launch the POCLI TUI Command Center, query SQLite with pocli db, and generate PM HTML reports."
permalink: "/quickstart/"
bodyClass: page-about
---

Get started with **POCLI** in seconds on Linux.

## 1. One-Command Install (Recommended)

Downloads the latest Linux release tarball from GitHub Releases, provisions standalone Node.js LTS automatically if missing, and installs the `pocli` launcher into `~/.local/bin/pocli`:

```bash
curl -fsSL https://artificial-intelligence-engineering.github.io/pocli/install.sh | sh
```

Then configure your LLM provider key and launch:

```bash
pocli auth status
pocli
```

## 2. Install from Source (Development)

```bash
git clone https://github.com/artificial-intelligence-engineering/pocli.git
cd pocli
npm install
npm run build
```

## 3. Essential CLI Commands

```bash
# Interactive fullscreen TUI (Ink)
pocli

# Generate a 100% self-contained HTML PM Status Report
pocli report <project-name>

# Inspect the central SQLite database REPL ($HOME/.pocli/pocli.sqlite)
pocli db
pocli db "SELECT id, name, phase FROM projects;" --format json

# Configure models globally or per-agent
pocli models
pocli models developer ollama/qwen2.5-coder:14b

# Run the full test suite from source
npm test
```

## 4. Essential Interactive TUI Commands

Press **`Ctrl+Tab`** at any time to switch between the **Clean OpenCode View** and the **Multipanel Command Center**. Type **`/`** to open the interactive command menu:

| Command | Action |
| :--- | :--- |
| `/project` | Create a new workspace project, initialize `.pocli/artifacts`, and auto-discover git repos. |
| `/projects` | List and switch active projects in SQLite. |
| `/architect`, `/developer`, `/qa`, `/pm` | Switch active interlocutor or trigger parallel/sequential PM inquiries. |
| `/approve`, `/handoff`, `/accept` | Human Product Owner governance gates across the SDLC workflow. |
| `/validate` | Trigger Independent QA verification and isolated test execution. |
| `/report` | Generate a 100% HTML Project Status Report in `deliveries/project-status-report.html`. |
| `/compact [all]` | Condense older conversation turns into SQLite DAG compaction checkpoints. |
| `/system` | Inspect active agent system prompts and user overrides (`~/.pocli/behavior/system/`). |
| `/db` | Run SQL queries or dot-commands (`.tables`, `.experts`, `.stats`) inside the TUI. |
| `/settings` | Switch UI language (`en`/`es`), color themes, and central working directory. |

## 5. Customizing Agent Prompts

Override any agent's system prompt cleanly without modifying the repository:

```bash
mkdir -p ~/.pocli/behavior/system
cp behavior/system/developer.md ~/.pocli/behavior/system/developer.md
# Edit ~/.pocli/behavior/system/developer.md to inject team conventions
```

## 6. Community & Source

- **Main Repository**: [github.com/artificial-intelligence-engineering/pocli](https://github.com/artificial-intelligence-engineering/pocli)
- **Issues & Feature Requests**: [github.com/artificial-intelligence-engineering/pocli/issues](https://github.com/artificial-intelligence-engineering/pocli/issues)
- **Website Source**: [github.com/artificial-intelligence-engineering/pocli-website](https://github.com/artificial-intelligence-engineering/pocli-website)

