---
title: Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c
source_raw: RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_at: 2026-05-06T15:24:33.042Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, af6c6ecf, 58d0, 42d7]
---

# Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c

## Summary
The AiAgentNerd knowledge system ingests unstructured content, automatically structures and categorizes it, and maintains an evolving knowledge base through merge and cleanup workflows. It uses a preview-confirmation safety model and prioritizes updating existing knowledge over creating duplicates.

## Key Concepts
- **Automatic Ingestion**: Accepts raw notes, transcripts, chat outputs, and ideas without pre-formatting
- **Auto-Organization**: Assigns categories, generates filenames, structures content, and stores it in the correct location automatically
- **Structured Knowledge**: Transforms input into topics, context, key concepts, steps, commands, and important details
- **Merge Workflow**: Combines new information into existing knowledge to prevent duplication and enable continuous evolution
- **Safety Model**: Preview → Confirm → Save pattern; backups created before changes; no automatic deletion
- **Cleanup Agent**: Scans the knowledge base for duplicates, similar topics, and low-value notes; groups them for review with confidence scores and recommendations
- **Canonical Files**: Preferred merge targets when duplicate groups are identified

## Practical Use
- **Save new knowledge**: `Clean this up and save it` (auto-save) or `Save this to knowledge with preview` (requires confirmation)
- **Clean without saving**: `Clean this up`
- **Merge multiple inputs**: `Merge these` followed by content chunks, then `confirm merge`
- **Update existing knowledge**: `Merge this with existing knowledge about <topic> with preview` → review → `confirm merge`
- **Targeted file merge**: `Merge this with existing file <filename>.md with preview`
- **Split large content**: `Split this into multiple notes`
- **Confirmation commands**: `confirm`, `cancel`, `confirm merge`, `cancel merge`

## Implementation Notes
- **Cleanup Workflow**: Trigger via `cleanup knowledge` or `cleanup knowledge about <topic>`
- **Cleanup Output**: Returns duplicate groups, low-value groups, and similar topic groups; each lists files, confidence, and recommendation
- **Cleanup Actions**:
  - Merge: `merge cleanup group <n> into canonical with preview` → `confirm cleanup merge`
  - Archive: `archive cleanup group <n>` → `confirm archive`
  - Delete: `delete cleanup group <n>` (restricted to high-confidence cases only)
  - Cancel: `cancel cleanup`
- **Daily Flow**: Capture (`Clean this up and save it`) → Improve (`Merge with existing knowledge`) → Combine (`Merge related ideas`)
- **Operational Preferences**: Prefer merge over duplicate; use preview for important content; think in topics not files; keep input raw and let the system handle cleanup

## Related
- [[knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
