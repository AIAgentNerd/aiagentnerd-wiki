---
title: Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c
source_raw: RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_at: 2026-05-09T15:53:39.562Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, af6c6ecf, 58d0, 42d7]
---

# Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c

## Summary
The AiAgentNerd knowledge system is an ingestion and maintenance pipeline that transforms unstructured input into structured, evolving technical knowledge. It enforces a mandatory preview-confirmation gate before writes, supports merging new information into existing canonical files to prevent duplication, and provides a cleanup agent for duplicate detection and archival. This note documents the operator commands, safety behaviors, and daily workflows for interacting with the system.

## Key Concepts
- **Ingestion Pipeline**: Accepts raw input (notes, transcripts, chat logs, ideas) and structures it into topics, context, key concepts, steps, commands, and details.
- **Automatic Organization**: The system assigns categories (e.g., `concepts`, `inbox`), generates filenames, and places content without requiring manual path decisions.
- **Merge-First Semantics**: New information is merged into existing files rather than creating duplicates; knowledge is treated as continuously evolving.
- **Safety Gate**: All mutating operations follow `Preview → confirm → save`. No automatic overwrites occur.
- **Knowledge Cleanup Agent**: Scans the knowledge base to surface duplicates, similar topics, and low-value notes for operator review.
- **Cleanup Actions**: Merge into canonical, archive (preferred), or delete (restricted to high-confidence cases).
- **Immutable Audit Trail**: Backups are created before changes; archive is the default removal action.

## Practical Use
### Daily Operator Commands
- **Ingest with preview**: `Save this to knowledge with preview` → paste content → `confirm`
- **Ingest without preview**: `Clean this up and save it` → paste content
- **Clean only (no save)**: `Clean this up` → paste content
- **Merge multiple raw chunks**: `Merge these` → paste chunk 1 → paste chunk 2 → `confirm merge`
- **Merge into topic**: `Merge this with existing knowledge about <topic> with preview` → paste content → `merge 1` → `confirm merge`
- **Merge into specific file**: `Merge this with existing file <filename>.md with preview` → paste content
- **Split large content**: `Split this into multiple notes` → paste content
- **Cancel pending operation**: `cancel`, `cancel merge`, `cancel cleanup`

### Cleanup Workflow
- **Run scan**: `cleanup knowledge` or `cleanup knowledge about <topic>`
- **Review output groups**:
  - duplicate group
  - low-value group
  - similar topic group
  - Each group lists files, confidence score, and recommendation.
- **Merge group into canonical**: `merge cleanup group 1 into canonical with preview` → `confirm cleanup merge`
- **Archive group**: `archive cleanup group 1` → `confirm archive`
- **Delete group (restricted)**: `delete cleanup group 1` — only executes on high-confidence matches
- **Cancel cleanup**: `cancel cleanup`

### Recommended Daily Flow
1. **Capture**: `Clean this up and save it`
2. **Improve**: `Merge with existing knowledge`
3. **Combine**: `Merge related ideas`

### Operator Guidance
- Do not pre-clean input; keep it raw and let the system structure it.
- Do not overthink categories; let the system assign them.
- Prefer merge over duplicate; always update existing knowledge instead of re-saving.
- Use preview for important content.
- Think in topics, not files.

## Implementation Notes
- **Structured Output Schema**: Every ingested item is structured into `topics`, `context`, `key concepts`, `steps` (if procedural), `commands` (if relevant), and `important details`.
- **Frontmatter**: Saved notes carry metadata such as `category`, `filename`, and `type` (e.g., `raw`).
- **Target Repositories**: The system can write to multiple repositories (`aiagentnerd-wiki`, `aiagentnerd-system`, `goldienerd-knowledge`). When updating existing knowledge, the operator may need to specify the exact file path or repo context.
- **Preview State & Expiration**: Previews are held in a pending session state but can expire between turns. If expired, the operator must regenerate the preview before confirmation (`create a new preview first`).
- **Safety Constraints**:
  - No automatic deletion ever occurs.
  - Archive is the default and preferred removal action.
  - Confirmation is mandatory for all mutating operations.
  - Backups are created before any change.
- **Delete Restriction**: The `delete cleanup group` command is gated and only processes high-confidence matches.

## Related
- [[knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
