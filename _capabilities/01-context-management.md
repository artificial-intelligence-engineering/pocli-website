---
title: "Capability #1 — Context Management"
cap_number: 1
subsystem: "4.1 Instructions"
status: "implemented"
permalink: /capabilities/01-context-management/
description: "Capability #1 — Context Management — Implemented in POCLI."
---

## What It Is

Deterministically controls what enters the LLM prompt on every turn and in what order: system instructions, normative project artifacts, layered memory, compaction checkpoints, active turns, and grounded retrieval passages.

## Why It Matters

Unbounded chat transcripts cause context rot (*lost in the middle*), silently drop architectural constraints, and waste token budget on stale or irrelevant tool output.

## Implementation Status in POCLI

**Status:** Implemented

In POCLI, context assembly is not left to ad-hoc string concatenation or raw chat histories. Instead, `PoCliDatabase.assembleAgentContextWindow(projectId, expertRole)` (`src/storage/database.ts`) deterministically constructs an `AssembledContextWindow` organized into **three ordered tiers**, complemented by on-demand grounded citations from `NotebookRagEngine` (`src/runtime/notebook-rag.ts`).

<div class="ctx-diagram">
  <div class="ctx-diagram-title">
    <span>POCLI 3-Tier Context Window + On-Demand RAG</span>
    <code>PoCliDatabase.assembleAgentContextWindow()</code>
  </div>

  <div class="ctx-tiers">
    <div class="ctx-tier ctx-tier--t1">
      <div class="ctx-tier-label">
        <span class="ctx-tier-tag">Tier 1 · Cacheable Prefix</span>
        <span class="ctx-tier-name">Normative Artifacts</span>
      </div>
      <div class="ctx-tier-body">
        <p><strong>Authoritative project truth</strong> (cannot be overridden by memory): versioned artifacts (<code>REQ</code>, <code>ARCH</code>, etc.) formatted with code, version, type, status, relative file path, and traceability (<code>tracesTo</code>).</p>
        <div class="ctx-tier-source">Source: this.listArtifacts(projectId, true)</div>
      </div>
    </div>

    <div class="ctx-tier ctx-tier--t2">
      <div class="ctx-tier-label">
        <span class="ctx-tier-tag">Tier 2 · Durable State</span>
        <span class="ctx-tier-name">4-Layer Memory &amp; Compaction</span>
      </div>
      <div class="ctx-tier-body">
        <p>Injects up to <strong>8 persistent memory snippets</strong> (<code>CONVERSATIONAL</code>, <code>WORKING</code>, <code>PROJECT</code>, <code>AGENT</code>) plus the latest structured compaction summary (<code>structuredSummary</code>) from <code>context_compactions</code>.</p>
        <div class="ctx-tier-source">Source: this.listMemories(...) + this.getLatestCompactionCheckpoint(...)</div>
      </div>
    </div>

    <div class="ctx-tier ctx-tier--t3">
      <div class="ctx-tier-label">
        <span class="ctx-tier-tag">Tier 3 · Active Window</span>
        <span class="ctx-tier-name">Uncompacted Turns</span>
      </div>
      <div class="ctx-tier-body">
        <p>Appends the <strong>last 6 active uncompacted turns</strong> as DAG leaf snippets (<code>[id &lt;- parentId | fromRole -&gt; toRole]</code>), keeping immediate conversational continuity concise.</p>
        <div class="ctx-tier-source">Source: this.listMessages(projectId, expertRole, true).slice(-6)</div>
      </div>
    </div>

    <div class="ctx-tier ctx-tier--rag">
      <div class="ctx-tier-label">
        <span class="ctx-tier-tag">On-Demand · Grounded</span>
        <span class="ctx-tier-name">NotebookRagEngine</span>
      </div>
      <div class="ctx-tier-body">
        <p>Indexes workspace documentation incrementally via <strong>SHA-256</strong> file hashes, chunks by headings/lines, and retrieves grounded <code>RagCitation</code> passages using <strong>SQLite FTS5</strong> + semantic embeddings.</p>
        <div class="ctx-tier-source">Source: NotebookRagEngine.queryForProjectRole() (src/runtime/notebook-rag.ts)</div>
      </div>
    </div>
  </div>

  <div class="ctx-arrow">&darr; Assembled into AssembledContextWindow &darr;</div>

  <div class="ctx-output">
    <strong>Output:</strong> <code>formattedPromptContext</code> + live token accounting (<code>activeTokens</code>, <code>savedTokensByCompaction</code>, <code>compactionCount</code>)
  </div>
</div>

### How Each Tier Works in Detail

1. **Tier 1 — Cacheable Normative Artifacts Prefix:**
   `listArtifacts(projectId, true)` fetches the active, authoritative project artifacts (`REQ`, `ARCH`, etc.) and places them at the very start of `formattedPromptContext` under an explicit header: *cannot be overridden by memory*. Because this prefix only changes when a normative artifact is updated, LLM providers can maximize prompt-cache hits across turns.
2. **Tier 2 — 4-Layer Persistent Memory & Pi Compaction Checkpoint:**
   `listMemories(projectId, undefined, expertRole)` retrieves up to 8 relevant entries across POCLI's four memory layers (`CONVERSATIONAL`, `WORKING`, `PROJECT`, `AGENT`), formatted as compact one-line snippets (`[layer] key: value`). Right below it, `getLatestCompactionCheckpoint(projectId, expertRole)` injects the `structuredSummary` produced by `/compact`, preserving key decisions from older turns without keeping the full transcript.
3. **Tier 3 — Active Recent Conversation Window:**
   `listMessages(projectId, expertRole, true).slice(-6)` selects only the 6 most recent uncompacted messages, formatted with parent-turn links (`id <- parentId`) and role routing (`fromRole -> toRole`). Older messages already linked via `compacted_into_id` remain auditable in SQLite but stay out of the active prompt.
4. **On-Demand Grounded Retrieval (`NotebookRagEngine`):**
   Instead of stuffing entire documentation folders into every prompt, `NotebookRagEngine` (`src/runtime/notebook-rag.ts`) watches and indexes workspace notebooks incrementally (skipping unchanged files via **SHA-256** hashes), splits documents into line-numbered chunks, and injects verified `RagCitation` snippets via `queryForProjectRole()` only when relevant to the active role and turn.

### Pending / Roadmap

Automatic provider-threshold compaction triggered transparently before context saturation without requiring manual `/compact`.
