---
title: Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c
source_raw: RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_at: 2026-05-07T07:04:16.818Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, af6c6ecf, 58d0, 42d7]
---

# Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c

## Summary
Documentation of the AiAgentNerd knowledge system’s user-facing ingestion, merge, and cleanup workflows. Describes how unstructured input is automatically structured, the preview-confirm-save safety model, the Knowledge Cleanup Agent’s duplicate detection, and the exact natural-language commands used to interact with the system. Derived from an OpenWebUI session that also exposed a recurring preview-expiration failure mode.

## Key Concepts
- **Messy Input Ingestion**: Accepts notes, transcripts, chat outputs, and unstructured thoughts; automatically structures into topics, context, key concepts, steps, commands, and important details.
- **Automatic Organization**: System infers category, generates filename, structures content, and stores it in the correct repository location without manual filing.
- **Merge-First Philosophy**: New information is merged into existing knowledge rather than creating duplicates; canonical files are updated and improved over time.
- **Safety Model**: Preview → confirm → save workflow prevents accidental overwrites. No automatic deletions; archive is preferred over delete. Backups are created before changes.
- **Knowledge Cleanup Agent**: Scans the knowledge base for duplicates, similar topics, and low-value or noisy notes. Groups them into review buckets (duplicate group, low-value group, similar topic group) with confidence scores and recommended actions: merge, archive, or ignore.
- **Daily Workflow**: Three-step pattern — capture (`Clean this up and save it`), improve (`Merge with existing knowledge`), combine (`Merge related ideas`).
- **Command Interface**: Natural-language commands for save, preview, merge, split, cleanup, confirm, and cancel operations.

## Practical Use
- **Saving New Knowledge**: Paste raw content and issue `Clean this up and save it` or `Save this to knowledge with preview`. Review the generated preview, then reply `confirm` to persist.
- **Merging Updates**: Use `Merge this with existing knowledge about <topic> with preview` to augment existing notes. If multiple files match, select by index (`merge 1`) and confirm.
- **Targeted Merging**: Use `Merge this with existing file <filename>.md with preview` to update a specific canonical note.
- **Cleanup Execution**: Run `cleanup knowledge` or `cleanup knowledge about <topic>`. Review grouped recommendations, then execute `merge cleanup group 1 into canonical with preview`, `archive cleanup group 1`, or `delete cleanup group 1` (restricted to high-confidence cases), followed by explicit confirmation.
- **Splitting Content**: Use `Split this into multiple notes` for large inputs that should become separate notes.
- **Cancellation**: Use `cancel`, `cancel merge`, or `cancel cleanup` to abort pending operations.
- **Operational Warning**: Previews can expire before confirmation, requiring regeneration. In this session, multiple `confirm save` attempts failed with the error *“No pending knowledge preview found. It may have expired; create a new preview first.”*

## Implementation Notes
- **Structured Output Schema**: Every ingested item is structured into topics, context, key concepts, steps (if procedural), commands (if relevant), and important details.
- **Cleanup Group Metadata**: Each cleanup result includes file references, confidence level, and recommended action.
- **Fallback Behavior**: If automatic cleaning fails, the system falls back to a safe raw capture preview with a suggested category and filename (e.g., `category: inbox`, `type: raw`).
- **Observed Failure Mode**: The OpenWebUI knowledge preview state appears to be ephemeral or session-bound. Sequential `confirm save` commands repeatedly returned *“No pending knowledge preview found”* even immediately after a preview was generated, indicating a broken or misaligned preview-confirmation state handoff in the interface.
- **Repository Scope**: The guide references three knowledge stores: `aiagentnerd-wiki` (human builder docs), `aiagentnerd-system` (machine memory), and `goldienerd-knowledge` (product/user knowledge). Workflow commands operate across these stores based on inferred or specified category.

## Related
- [[knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
