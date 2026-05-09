---
title: Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c
source_raw: RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_at: 2026-05-09T17:26:48.673Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, af6c6ecf, 58d0, 42d7]
---

# Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c

## Summary
The AiAgentNerd knowledge system provides an automated ingestion, structuring, and maintenance pipeline across the project's knowledge repositories. Raw inputs are cleaned, categorized, and stored as structured notes, with a merge-first design that evolves existing documents rather than creating duplicates. A Knowledge Cleanup Agent scans for duplicates and low-value content, recommending merge, archive, or ignore actions with mandatory confirmation and backups.

## Key Concepts
- **Ingestion Pipeline**: Accepts raw input (notes, transcripts, chat outputs, ideas) and structures it into topics, context, key concepts, steps, commands, and important details.
- **Auto-Organization**: Automatically selects a category, generates a filename, and stores content in the correct repository location.
- **Merge-First Design**: New information is merged into existing knowledge rather than creating duplicate files.
- **Safety Model**: Mutating operations require `Preview → confirm → save`. No automatic deletion; archive is preferred over delete; backups are created before changes.
- **Knowledge Cleanup Agent**: Scans the knowledge base to find duplicates, similar topics, and low-value or noisy notes, grouping them for operator review.
- **Cleanup Groups**: Duplicate group, low-value group, similar topic group. Each group lists files, a confidence score, and a recommendation.

## Practical Use
### Daily Capture Commands
- **Ingest with save**: `Clean this up and save it` + `<paste content>`
- **Ingest with preview**: `Save this to knowledge with preview` + `<paste content>` → `confirm`
- **Clean only (no save)**: `Clean this up` + `<paste content>`

### Merge Workflows
- **Merge multiple raw pieces**: `Merge these` + `<paste RAW chunk 1>` + `<paste RAW chunk 2>` → `confirm merge`
- **Merge into topic**: `Merge this with existing knowledge about <topic> with preview` + `<new information>` → `merge 1` → `confirm merge`
- **Merge into specific file**: `Merge this with existing file <filename>.md with preview` + `<new info>` → confirm
- **Split large content**: `Split this into multiple notes` + `<large content>`

### Global Controls
- `confirm` / `cancel`
- `confirm merge` / `cancel merge`

### Cleanup Workflow
1. **Run scan**: `cleanup knowledge` or `cleanup knowledge about <topic>`
2. **Review groups**: duplicate group, low-value group, similar topic group
3. **Actions**:
   - Merge: `merge cleanup group <N> into canonical with preview` → `confirm cleanup merge`
   - Archive: `archive cleanup group <N>` → `confirm archive`
   - Delete (restricted): `delete cleanup group <N>` — executes only for high-confidence cases
   - Cancel: `cancel cleanup`

### Daily Flow
1. Capture: `Clean this up and save it`
2. Improve: `Merge with existing knowledge`
3. Combine: `Merge related ideas`

## Implementation Notes
- **Structured Output Schema**: Every ingested input is transformed into a standard structure containing topics, context, key concepts, steps (if applicable), commands (if applicable), and important details.
- **Repository Scope**: The system operates across three repositories:
  - `aiagentnerd-wiki` — human builder knowledge, architecture, and maintenance docs
  - `aiagentnerd-system` — machine memory, logs, and operational records
  - `goldienerd-knowledge` — product and user knowledge
- **Cleanup Safety**: The system never deletes automatically. Archive is the preferred remediation for low-value content. All merge and archive operations require explicit confirmation, and backups are created prior to changes.
- **Preview Expiry**: Preview sessions can expire if not confirmed promptly; a new preview must be generated if confirmation fails.

## Related
- [[knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
