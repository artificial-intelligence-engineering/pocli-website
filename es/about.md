---
title: Arquitectura e Investigación
lang: es
layout: page
permalink: /es/about/
description: "Qué es un harness de agentes, estándares de facto, fundamentos neuro-simbólicos, los 5 subsistemas fundamentales y cómo los implementa POCLI."
bodyClass: page-about
---

POCLI es un harness. En esta sección examinamos qué es un harness y cómo lo implementa POCLI.

---

## 1. ¿Qué es Harness Engineering?

### 1.1 Prefacio

**"Harness engineering"** como disciplina con nombre propio no tiene todavía un paper canónico ni un estándar formal. Es un término emergente de ingeniería (2024–2026) que aún vive principalmente en blogs de ingeniería, reportes técnicos y repositorios open-source, más que en literatura académica consolidada.

### 1.2 Referencias de Facto en la Industria y Academia

1. **Anthropic — ["Building Effective Agents"](https://www.anthropic.com/engineering/building-effective-agents)** (Erik Schluntz & Barry Zhang, 19 dic. 2024): Post de ingeniería (no PDF) — la referencia práctica más citada del campo.
2. **Anthropic — ["Effective Context Engineering for AI Agents"](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)** (Anthropic Engineering, 2025): Referencia clave sobre cómo curar un contexto acotado y de alta señal en cada turno.
3. **OpenAI — ["A Practical Guide to Building Agents"](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf)** (PDF oficial, 2025; también disponible en [openai.com](https://openai.com/) → Business → Guides).
4. **Kapoor et al. — ["AI Agents That Matter"](https://arxiv.org/abs/2407.01502)** ([PDF](https://arxiv.org/pdf/2407.01502), Princeton, julio 2024 — Sayash Kapoor, Benedikt Stroebl, Zachary S. Siegel, Nitya Nadgir, András Vécsey, Daniel Chen, Arvind Narayanan): El paper académico más citado sobre cómo evaluar agentes de forma rigurosa, criticando fallos de benchmarks y comparativas sin control de costes — lo más cercano a un "paper oficial" sobre evaluar el *sistema completo* y no solo el modelo.
5. **Chip Huyen — ["AI Engineering"](https://www.oreilly.com/library/view/ai-engineering/9781098166298/)** (O'Reilly, enero 2025; material relacionado gratuito en [huyenchip.com](https://huyenchip.com/)): El libro más consolidado que cubre evals, RAG, agentes y fine-tuning con rigor de ingeniería — cubriendo el "sistema alrededor del modelo" aunque no use con frecuencia el término *harness*.
6. **Cognition — ["Don't Build Multi-Agents"](https://cognition.ai/blog/dont-build-multi-agents)** (Walden Yan, 2025): El post que articuló el principio *"share full context / don't fragment agents"* — el contrargumento más citado al diseño multi-agente ingenuo.
7. **Anthropic — ["How We Built Our Multi-Agent Research System"](https://www.anthropic.com/engineering/built-multi-agent-research-system)** (2025): El complemento ideal al de Cognition, mostrando cuándo la coordinación multi-agente *sí* merece la pena.
8. **Surveys académicos de agentes LLM:** *"A Survey on LLM-based Autonomous Agents"* (Wang et al., 2023) y *"Understanding the Planning of LLM Agents"* (Huang et al.) aportan taxonomías académicas base previas a la ola *harness*.

---

## 2. Agent vs. Harness: Núcleo Estocástico y Envolvente Determinista

- **`Agent`** ≈ la parte **estocástica** (modelo LLM + bucle de razonamiento + selección de herramientas).
- **`Harness`** ≈ la parte **determinista** que lo envuelve, alimenta, restringe y verifica.

¿Qué significa *estocástico* en este contexto?

| Comportamiento | Definición |
| :--- | :--- |
| **Determinista** | Produce siempre **1 salida predecible** para una entrada dada. |
| **Indeterminista** | Varias salidas posibles **sin probabilidad asignada** (elección libre, no-determinismo de autómatas: *"cualquiera de estas ramas puede pasar"*). |
| **Estocástico** | Varias salidas posibles, **cada una con una distribución de probabilidad** (un dado, una cadena de Markov, un LLM muestreando tokens de una distribución — *"aleatorio con distribución"*). |

---

## 3. El Harness como IA Neuro-Simbólica Práctica

A partir de la formulación de [Gary Marcus](https://en.wikipedia.org/wiki/Gary_Marcus) sobre la **IA neuro-simbólica**, un harness es, arquitectónicamente, un sistema neuro-simbólico *ad hoc* que combina dos paradigmas históricos tradicionalmente rivales:

```text
IA simbólica (GOFAI, años 70–90)         IA subsimbólica / neuronal (2010+)
───────────────────────────────────      ───────────────────────────────────
Reglas explícitas, lógica, árboles       Redes neuronales que aprenden
de conocimiento, ontologías,             patrones de enormes datasets
Prolog, razonamiento deductivo           (LLMs, CNNs, transformers)
                 └──────────────┬──────────────┘
                                ▼
                       IA NEURO-SIMBÓLICA
              neuronal para PERCIBIR + simbólica para RAZONAR
```

- **La idea nuclear:** Las redes neuronales son excelentes *percibiendo* (extrayendo señal y patrones del mundo), pero malas razonando con garantías lógicas (alucinan). Las reglas simbólicas son excelentes *razonando y verificando*, pero frágiles percibiendo (un símbolo mal extraído rompe todo). La hibridación deja a cada lado hacer lo que mejor sabe.

### 3.1 Patrones de Hibridación y Ejemplos Reales

1. **Red → Símbolos → Razón:** El LLM extrae estructura; un motor determinista verifica reglas.
2. **Símbolos guían a la red:** Una gramática o esquema formal restringe la generación (p. ej., *constrained decoding*).
3. **Arquitecturas internas:** Módulos simbólicos diferenciables integrados dentro de redes neuronales.

| Ejemplo real | Neuronal (Percepción / Propuesta) | Simbólico (Razón / Verificación) |
| :--- | :--- | :--- |
| **AlphaGo / AlphaZero** | La red evalúa posiciones del tablero | Búsqueda algorítmica MCTS explora el árbol de jugadas |
| **LLM + Prolog / SMT** | El modelo traduce el problema a lógica formal | Un solver (Z3, Prolog) resuelve con garantías |
| **Grammar-constrained decoding** | El LLM propone los siguientes tokens | Una gramática formal (GBNF, JSON Schema) acota la salida |
| **Tool calling + verificador** | El agente propone cambios de código | Compilador, type-checker y tests verifican de forma determinista |
| **RAG + base de conocimiento** | El modelo recupera y sintetiza pasajes | Las "verdades" provienen de una estructura simbólica consultable |
| **CodeQL + LLM** | El LLM razona sobre el contexto | El analizador estático realiza *dataflow* formal |
| **VSA / Neuro-Vector-Symbolic** | Representaciones vectoriales de alta dimensión | Composición algebraica de símbolos (investigación activa) |

**Correspondencia directa entre IA Neuro-Simbólica y un Harness de Agentes:**

| Concepto Neuro-Simbólico | Harness de Agentes en la Práctica (`POCLI`) |
| :--- | :--- |
| El componente neuronal *"percibe"* | El LLM genera, decide y propone (`REQ`, `ARCH`, `CODE`) |
| El componente simbólico *"razona / verifica"* | Gates deterministas (`AuthorityGuard`), tests, linters y tool calls |
| La arquitectura decide qué va a cada lado | Diseño del pipeline: selección de ficheros, call graphs, gates de fase |
| Fallo: un símbolo mal extraído rompe todo | Fallo: un filtro defectuoso (ej. `is_source_file`) descarta el fichero real |

### 3.2 La postura de Gary Marcus sobre Claude Code

Marcus sostiene desde hace años (notablemente en su libro *Rebooting AI* de 2019) que el aprendizaje profundo puro (*deep learning*) choca contra un muro porque los LLMs son esencialmente predictores probabilísticos de tokens sin noción intrínseca de verdad, lógica formal o límites de seguridad.

Cuando se analizó la arquitectura interna de Claude Code, Marcus argumentó que el salto cualitativo de esta herramienta **no se debe a un modelo de lenguaje aislado más grande**, sino a que **no es un LLM puro**: es un sistema híbrido que envuelve a la red neuronal con ingeniería de software tradicional y componentes simbólicos deterministas.

### 3.3 El concepto de *Harness* (Arnés) como el componente simbólico

En el diseño de agentes modernos, la industria y los analistas adoptaron la metáfora de la habitación y el arnés:

- **El componente neural:** El LLM actúa como un experto probabilístico dentro de una caja que sugiere intenciones, código y razonamientos en lenguaje natural.
- **El arnés (Harness):** Es el andamiaje de software determinista (escrito en lenguajes clásicos como TypeScript o Python) que opera fuera de la caja. El arnés:
  1. **Controla el flujo con lógica determinista:** Implementa árboles de decisión explícitos (estructuras `IF-THEN`, enrutadores, políticas de ejecución).
  2. **Intermediación formal con el entorno:** Analiza árboles de sintaxis abstracta (AST), compila, ejecuta pruebas unitarias deterministas (`pytest`, `npm test`) y valida la salida antes de confirmar cambios.
  3. **Aplica límites y guardrails:** Frena comandos peligrosos, fuerza verificaciones de seguridad y define qué información contextual puede leer el modelo.

Para Marcus, este *harness* de reglas, gramáticas y herramientas formales es precisamente la **encarnación práctica del subsistema simbólico**, compensando la falta de rigor lógico del modelo neuronal con la precisión del software determinista.

---

## 4. Los 5 Subsistemas Fundamentales y el Mapeo de Capacidades

Un harness gobernado puede estructurarse en **cinco subsistemas fundamentales**. Al mapear las **40 capacidades** (de la [Matriz de Capacidades y Cobertura](/es/services/#harness-matrix) de POCLI) sobre estos cinco pilares, se distingue claramente qué pertenece al entorno gobernado y qué forma parte del runtime operativo puro:

### 4.1 Instructions
*Reglas, convenciones, arquitectura y pasos que el agente debe seguir (más allá de `AGENTS.md`: todo lo que indica al modelo qué es verdad y qué debe hacer).*

- **Capacidad #1 — Gestión de contexto:** qué entra en el prompt y cómo se monta.
- **Capacidad #2 — Compactación estructurada:** reglas para preservar lo esencial entre turnos.
- **Capacidad #3 — Tool discovery y carga JIT:** catálogo de capacidades bajo demanda.
- **Capacidad #4 — Plugins y skills:** extensión declarativa de instrucciones.
- **Capacidad #5 — Context provenance:** procedencia documentada de cada elemento inyectado.
- **Capacidad #6 — Append-only event log:** registro inmutable de qué instrucciones recibió.

### 4.2 State
*Progreso, decisiones, archivos modificados y handoffs entre sesiones.*

- **Capacidad #7 — Persistencia de sesiones:** almacenamiento durable de conversaciones.
- **Capacidad #8 — Memoria por capas:** memoria de trabajo, corto/largo plazo y episódica.
- **Capacidad #9 — Checkpoints y durable execution:** puntos de reanudación seguros.
- **Capacidad #10 — Handoffs tipados:** contrato de continuidad entre sesiones.
- **Capacidad #11 — Replay y recuperación:** reconstrucción determinista de estado.
- **Capacidad #12 — Memoria episódica / observacional:** trazabilidad histórica de comportamiento.
- **Capacidad #13 — Feature state tracking:** estado de funcionalidades y artefactos como primitiva.
- **Capacidad #14 — State merge semantics:** reglas deterministas de combinación de escrituras.

### 4.3 Verification
*Tests, lint, type-check, smoke tests y validación empírica.*

- **Capacidad #15 — Tests del runtime:** el harness se testea a sí mismo.
- **Capacidad #16 — Evals del agente:** medición de la calidad del modelo.
- **Capacidad #17 — Failure routing / rollback:** qué ocurre cuando la verificación falla.
- **Capacidad #18 — Harness-level evaluation:** medición del sistema completo.

### 4.4 Scope
*Límites de lo que el agente puede tocar y del tamaño de la tarea.*

- **Capacidad #19 — Ejecución segura / sandbox:** límites de sistema operativo sobre qué puede ejecutarse.
- **Capacidad #20 — Aprobaciones y permisos:** gates que requieren firma explícita del PO.
- **Capacidad #21 — Routing:** qué camino toma el flujo y cuál queda bloqueado.
- **Capacidad #22 — Worktrees:** aislamiento físico del espacio de trabajo.
- **Capacidad #23 — Scope control:** acotación estricta del tamaño de tarea y archivos editables.

### 4.5 Session Lifecycle
*Inicialización, ejecución, limpieza, persistencia y reanudación.*

- **Capacidad #24 — Recuperación de errores:** manejo resiliente de fallos transitorios.
- **Capacidad #25 — Streaming y cancelación:** ciclo de vida de la salida en curso.
- **Capacidad #26 — Session lifecycle:** arranque, pausa, reanudación y cierre.
- **Capacidad #27 — Bootstrap / preflight:** la fase `initialize`.

### 4.6 Capa de Runtime Operativo Puro (Fuera de los 5 Pilares)
*La **"capa de servicio"** subyacente que el modelo de gobernanza de 5 pilares da por supuesta:*

- **Capacidad #28 — Agent loop:** el mecanismo mismo de ejecución.
- **Capacidad #29 — Model gateway:** abstracción de proveedores LLM.
- **Capacidad #30 — Tool calling tipado:** la interfaz agente ↔ mundo.
- **Capacidad #31 — Observabilidad:** telemetría y logs transversales.
- **Capacidad #32 — Cost tracking:** contabilidad de tokens y gasto.
- **Capacidad #33 — Multi-agent orchestration:** coordinación de múltiples agentes especializados.
- **Capacidad #34 — Event-driven agents:** ejecución reactiva por eventos.
- **Capacidad #35 — Sub-agent delegation:** delegación de subtareas acotadas.
- **Capacidad #36 — Snapshots por rol:** inspección del estado por rol.
- **Capacidad #37 — Adaptive model routing:** selección dinámica de modelo por tarea.
- **Capacidad #38 — Métricas de productividad:** medición del rendimiento de entrega.
- **Capacidad #39 — Capability seams:** arquitectura de providers, no un pilar funcional.
