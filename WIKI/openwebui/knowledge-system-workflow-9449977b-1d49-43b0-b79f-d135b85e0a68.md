---
title: Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68
source_raw: RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_at: 2026-05-07T10:24:20.503Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, 9449977b, 1d49, 43b0]
---

# Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68

## Summary
Documents the AiAgentNerd knowledge ingestion pipeline and maintenance workflow, including how raw inputs are transformed into structured wiki entries, the voice/text command interface for capture and merge operations, the preview-confirmation safety gate, and the Knowledge Cleanup Agent's deduplication and archival behaviors. Also captures a known operational issue where previews can expire before confirmation.

## Key Concepts
- **Ingestion Pipeline**: Raw input (notes, transcripts, chat logs, thoughts) is automatically cleaned, categorized, assigned a filename, structured into topics/context/key concepts/steps/commands, and stored.
- **Automatic Organization**: The system determines category, filename, content structure, and target location without manual folder management.
- **Preview-Confirm-Save Gate**: All destructive or new write operations require a preview step and explicit user confirmation (`confirm`, `confirm merge`, `confirm cleanup merge`, `confirm archive`). This prevents accidental overwrites.
- **Merge-First Policy**: Prefer merging new information into existing knowledge over creating duplicates. The system updates existing files to keep knowledge evolving.
- **Knowledge Cleanup Agent**: Periodically scans the knowledge base to detect duplicates, similar topics, and low-value notes. It groups findings for review with confidence scores and recommended actions.
- **Cleanup Actions**: Merge into canonical, archive, or ignore. Deletion is restricted and only offered for high-confidence cases.
- **Safety Defaults**: No automatic deletion. Archive is preferred over delete. Backups are created before changes.
- **Fallback Behavior**: If automatic cleaning fails, the system falls back to a safe raw capture preview.

## Practical Use
**Daily Capture Commands**
- Ingest and save: `Clean this up and save it` → paste content → `confirm`
- Preview first: `Save this to knowledge with preview` → paste content → review → `confirm`
- Clean only, no save: `Clean this up` → paste content

**Merge Commands**
- Merge raw chunks: `Merge these` → paste chunk 1 → paste chunk 2 → `confirm merge`
- Merge by topic: `Merge this with existing knowledge about <topic> with preview` → paste content → `merge 1` → `confirm merge`
- Merge to specific file: `Merge this with existing file <filename>.md with preview` → paste content → confirm

**Content Splitting**
- `Split this into multiple notes` → paste large content

**Cleanup Commands**
- Run full cleanup: `cleanup knowledge`
- Scoped cleanup: `cleanup knowledge about <topic>`
- Merge duplicates: `merge cleanup group <n> into canonical with preview` → `confirm cleanup merge`
- Archive group: `archive cleanup group <n>` → `confirm archive`
- Delete (restricted): `delete cleanup group <n>` (high-confidence only)
- Cancel: `cancel cleanup`

**Cancel Operations**
- `cancel`, `cancel merge`, `cancel cleanup`

**Daily Flow**
1. Capture: `Clean this up and save it`
2. Improve: `Merge with existing knowledge`
3. Combine: `Merge related ideas`

## Implementation Notes
- **Repository Flow**: Internally, compiled wiki pages move from `RAW/` to `WIKI/` and receive a `compiled_at` timestamp.
- **Preview State**: The preview mechanism is stateful and can expire. If too much time passes between preview generation and confirmation, the system responds with:
  > `No pending knowledge preview found. It may have expired; create a new preview first.`
  
  This requires regenerating the preview before confirmation will succeed.
- **No Direct Save Bypass**: At the time of this note, the internal wiki does not document a `--no-preview` flag or endpoint parameter to skip the preview interlock. Adding direct-save would require extending the compilation service or UI to support a pre-approved flag.
- **Structured Output Schema**: Every processed input is structured into: `topics`, `context`, `key concepts`, `steps` (if procedural), `commands` (if operational), and `important details`.
- **Cleanup Group Output**: Each cleanup group includes: file references, confidence level, and a recommendation (`merge`, `archive`, `ignore`).

## Related
- [[knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
