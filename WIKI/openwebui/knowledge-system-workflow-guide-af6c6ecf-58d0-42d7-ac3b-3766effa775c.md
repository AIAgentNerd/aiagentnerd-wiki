---
title: Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c
source_raw: RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_at: 2026-05-09T16:56:02.419Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, af6c6ecf, 58d0, 42d7]
---

# Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c

## Summary
AiAgentNerd knowledge system workflow covering ingestion, automatic structuring, merge-first storage, and periodic cleanup. Raw input is accepted without manual formatting, organized into structured knowledge, and evolved over time through merges rather than duplicates. A preview-confirm safety gate protects against accidental overwrites, and a Knowledge Cleanup Agent scans for duplicates and low-value content.

## Key Concepts
- **Raw input ingestion**: Accepts unstructured notes, transcripts, chat outputs, and ideas without upfront formatting.
- **Auto-organization**: Automatically assigns category, filename, content structure, and storage location.
- **Structured output**: Every item is structured into topics, context, key concepts, steps (if needed), commands (if relevant), and important details.
- **Merge-first philosophy**: New information merges into existing knowledge; duplicates are avoided and existing files are improved over time.
- **Preview-confirm-save gate**: All mutating operations require a preview and explicit confirmation before persistence.
- **Knowledge Cleanup Agent**: Scans the knowledge base to surface duplicates, similar topics, and low-value or noisy notes for operator review.
- **Canonical targets**: When duplicates are found, the system suggests a primary (canonical) file as the merge destination.
- **Archive preferred over delete**: No automatic deletion; archive is the default remediation, and manual deletion is restricted to high-confidence cases.
- **Learning engine**: More input leads to better structure and outputs over time.

## Practical Use
- **Ingest new knowledge**: `Clean this up and save it` (paste content). For preview mode: `Save this to knowledge with preview` → review → `confirm`.
- **Clean only (no save)**: `Clean this up` (paste content).
- **Merge multiple raw chunks**: `Merge these` → paste chunk 1 and chunk 2 → `confirm merge`.
- **Improve existing knowledge by topic**: `Merge this with existing knowledge about <topic> with preview` → paste new information → select target with `merge 1` → `confirm merge`.
- **Merge into a specific file**: `Merge this with existing file <filename>.md with preview` → paste new information.
- **Split large content**: `Split this into multiple notes` → paste large content block.
- **Workflow controls**: `confirm`, `cancel`, `confirm merge`, `cancel merge`.
- **Run cleanup**: `cleanup knowledge` or `cleanup knowledge about <topic>`.
- **Review cleanup output**: Groups are returned as duplicate group, low-value group, and similar topic group. Each entry includes files, confidence score, and recommendation.
- **Cleanup actions**:
  - Merge duplicates into canonical: `merge cleanup group <n> into canonical with preview` → `confirm cleanup merge`
  - Archive group: `archive cleanup group <n>` → `confirm archive`
  - Delete (restricted): `delete cleanup group <n>` (high-confidence cases only)
  - Cancel: `cancel cleanup`
- **Daily flow**: Step 1 — capture (`Clean this up and save it`); Step 2 — improve (`Merge with existing knowledge`); Step 3 — combine (`Merge related ideas`).

## Implementation Notes
- Knowledge items are stored with frontmatter including `category`, `filename`, and `type` (e.g., `raw`).
- Backups are created before applying changes; accidental overwrites are prevented by the confirmation gate.
- Cleanup groups are identified by number (e.g., `cleanup group 1`) and acted upon via canonical merge, archive, or restricted delete commands.
- Keep input raw and let the system handle categorization and structuring; overthinking categories is discouraged.
- Think in topics rather than individual files when merging and retrieving knowledge.

## Related
- [[knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
