---
title: "Capacidad #1 — Gestión de Contexto"
lang: es
cap_number: 1
subsystem: "4.1 Instructions"
status: "implemented"
permalink: /es/capabilities/01-context-management/
description: "Capacidad #1 — Gestión de Contexto — Implementada en POCLI."
---

## Qué es

Controla de forma determinista qué entra en el prompt del LLM en cada turno y en qué orden: instrucciones de sistema, artefactos normativos del proyecto, memoria por capas, checkpoints de compactación, turnos activos y pasajes recuperados.

## Por qué importa

Los historiales sin acotar provocan degradación del contexto (*lost in the middle*), hacen que el modelo olvide decisiones de arquitectura y disparan el consumo de tokens con salidas obsoletas.

## Estado e Implementación en POCLI

**Estado:** Implementada

En POCLI, el ensamblado del contexto no se deja a concatenaciones ad-hoc ni a historiales planos de chat. `PoCliDatabase.assembleAgentContextWindow(projectId, expertRole)` (`src/storage/database.ts`) construye de forma determinista un objeto `AssembledContextWindow` estructurado en **tres niveles ordenados**, complementado bajo demanda con citas verificables de `NotebookRagEngine` (`src/runtime/notebook-rag.ts`).

<div class="ctx-diagram">
  <div class="ctx-diagram-title">
    <span>Ventana de Contexto en 3 Niveles + RAG bajo Demanda</span>
    <code>PoCliDatabase.assembleAgentContextWindow()</code>
  </div>

  <div class="ctx-tiers">
    <div class="ctx-tier ctx-tier--t1">
      <div class="ctx-tier-label">
        <span class="ctx-tier-tag">Nivel 1 · Prefijo Cacheable</span>
        <span class="ctx-tier-name">Artefactos Normativos</span>
      </div>
      <div class="ctx-tier-body">
        <p><strong>Verdad autoritativa del proyecto</strong> (la memoria no puede sobrescribirla): artefactos versionados (<code>REQ</code>, <code>ARCH</code>, etc.) con código, versión, tipo, estado, ruta relativa y trazabilidad (<code>tracesTo</code>).</p>
        <div class="ctx-tier-source">Fuente: this.listArtifacts(projectId, true)</div>
      </div>
    </div>

    <div class="ctx-tier ctx-tier--t2">
      <div class="ctx-tier-label">
        <span class="ctx-tier-tag">Nivel 2 · Estado Durable</span>
        <span class="ctx-tier-name">Memoria 4 Capas y Compactación</span>
      </div>
      <div class="ctx-tier-body">
        <p>Inyecta hasta <strong>8 entradas de memoria persistente</strong> (<code>CONVERSATIONAL</code>, <code>WORKING</code>, <code>PROJECT</code>, <code>AGENT</code>) junto con el último resumen estructurado (<code>structuredSummary</code>) de <code>context_compactions</code>.</p>
        <div class="ctx-tier-source">Fuente: this.listMemories(...) + this.getLatestCompactionCheckpoint(...)</div>
      </div>
    </div>

    <div class="ctx-tier ctx-tier--t3">
      <div class="ctx-tier-label">
        <span class="ctx-tier-tag">Nivel 3 · Ventana Activa</span>
        <span class="ctx-tier-name">Turnos Sin Compactar</span>
      </div>
      <div class="ctx-tier-body">
        <p>Añade los <strong>últimos 6 turnos activos sin compactar</strong> como nodos hoja del DAG (<code>[id &lt;- parentId | fromRole -&gt; toRole]</code>), manteniendo la continuidad inmediata de forma concisa.</p>
        <div class="ctx-tier-source">Fuente: this.listMessages(projectId, expertRole, true).slice(-6)</div>
      </div>
    </div>

    <div class="ctx-tier ctx-tier--rag">
      <div class="ctx-tier-label">
        <span class="ctx-tier-tag">Bajo Demanda · Fundamentado</span>
        <span class="ctx-tier-name">NotebookRagEngine</span>
      </div>
      <div class="ctx-tier-body">
        <p>Indexa la documentación del workspace de forma incremental mediante hashes <strong>SHA-256</strong>, trocea por encabezados y líneas, y recupera citas <code>RagCitation</code> con <strong>SQLite FTS5</strong> + embeddings semánticos.</p>
        <div class="ctx-tier-source">Fuente: NotebookRagEngine.queryForProjectRole() (src/runtime/notebook-rag.ts)</div>
      </div>
    </div>
  </div>

  <div class="ctx-arrow">&darr; Ensamblado en AssembledContextWindow &darr;</div>

  <div class="ctx-output">
    <strong>Salida:</strong> <code>formattedPromptContext</code> + contabilidad de tokens (<code>activeTokens</code>, <code>savedTokensByCompaction</code>, <code>compactionCount</code>)
  </div>
</div>

### Cómo funciona cada nivel en detalle

1. **Nivel 1 — Prefijo cacheable de artefactos normativos:**
   `listArtifacts(projectId, true)` obtiene los artefactos activos y autoritativos (`REQ`, `ARCH`, etc.) y los sitúa al principio de `formattedPromptContext` bajo una cabecera explícita: *no pueden ser sobrescritos por la memoria*. Como este prefijo solo cambia cuando se actualiza un artefacto normativo, los proveedores LLM pueden maximizar los aciertos de caché entre turnos.
2. **Nivel 2 — Memoria persistente en 4 capas y checkpoint de compactación:**
   `listMemories(projectId, undefined, expertRole)` recupera hasta 8 entradas relevantes de las cuatro capas de memoria de POCLI (`CONVERSATIONAL`, `WORKING`, `PROJECT`, `AGENT`) en formato compacto de una línea (`[layer] key: value`). Justo debajo, `getLatestCompactionCheckpoint(projectId, expertRole)` inyecta el `structuredSummary` generado por `/compact`, preservando decisiones clave de turnos antiguos sin arrastrar todo el historial.
3. **Nivel 3 — Ventana de conversación activa reciente:**
   `listMessages(projectId, expertRole, true).slice(-6)` selecciona únicamente los 6 mensajes sin compactar más recientes, con enlace al turno padre (`id <- parentId`) y enrutamiento de rol (`fromRole -> toRole`). Los mensajes anteriores ya vinculados con `compacted_into_id` siguen auditables en SQLite pero fuera del prompt activo.
4. **Recuperación fundamentada bajo demanda (`NotebookRagEngine`):**
   En lugar de volcar carpetas enteras de documentación en cada prompt, `NotebookRagEngine` (`src/runtime/notebook-rag.ts`) vigila e indexa los notebooks del workspace de forma incremental (saltando archivos sin cambios mediante hashes **SHA-256**), segmenta por encabezados y rangos de líneas, e inyecta citas verificadas `RagCitation` mediante `queryForProjectRole()` solo cuando son relevantes para el rol y el turno actual.

### Pendiente / Hoja de ruta

Compactación automática basada en umbrales del proveedor antes de saturar la ventana sin requerir `/compact` manual.
