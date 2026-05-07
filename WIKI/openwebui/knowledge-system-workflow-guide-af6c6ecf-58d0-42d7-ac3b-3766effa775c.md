---
title: Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c
source_raw: RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_at: 2026-05-07T08:36:31.249Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, af6c6ecf, 58d0, 42d7]
---

# Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c

## Summary
The AiAgentNerd knowledge system ingestion and cleanup workflow, covering how unstructured input is captured, structured, merged, and maintained through natural language commands and a preview-confirm safety model.

## Key Concepts
- **Automatic Ingestion**: Accepts messy input (notes, transcripts, chat logs, thoughts) and structures it automatically
- **Structured Output Format**: Topics, context, key concepts, steps, commands, important details
- **Merge-First Design**: New information merges into existing knowledge rather than creating duplicates
- **Preview-Confirm-Save Safety**: All write operations require explicit confirmation after preview
- **Knowledge Cleanup Agent**: Scans the knowledge base to group duplicates, similar topics, and low-value notes for review
- **Canonical Files**: Cleanup identifies a primary file to serve as the merge target for duplicates

## Practical Use
- **Save new knowledge**: `Clean this up and save it` (immediate) or `Save this to knowledge with preview` → `confirm`
- **Clean without saving**: `Clean this up`
- **Merge multiple chunks**: `Merge these` (paste chunks) → `confirm merge`
- **Update existing topic**: `Merge this with existing knowledge about <topic> with preview` → select file → `confirm merge`
- **Update specific file**: `Merge this with existing file <filename>.md with preview`
- **Split large content**: `Split this into multiple notes`
- **Run cleanup**: `cleanup knowledge` or `cleanup knowledge about <topic>`
  - Review output groups (duplicate, low-value, similar topic) showing files, confidence, recommendation
  - `merge cleanup group <n> into canonical with preview` → `confirm cleanup merge`
  - `archive cleanup group <n>` → `confirm archive`
  - `delete cleanup group <n>` (restricted to high-confidence cases only)
  - `cancel cleanup`

## Implementation Notes
- **Frontmatter**: Captured knowledge uses `category`, `filename`, and `type: raw` fields
- **Categories**: Auto-assigned (e.g., `concepts`, `inbox`); user suggestions are accepted but system decides final placement
- **Safety Constraints**: No automatic deletion; archive preferred over delete; backups created before changes
- **Preview Lifecycle**: Previews expire if not confirmed promptly; expired previews must be regenerated before confirmation
- **Daily Flow**: Step 1 capture (`Clean this up and save it`), Step 2 improve (merge with existing), Step 3 combine (merge related ideas)
- **Operational Tips**: Prefer merge over duplicate saves; keep input raw and let the system structure it; think in topics rather than individual files

## Related
- [[knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
