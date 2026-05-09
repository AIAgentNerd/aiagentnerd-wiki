---
title: Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68
source_raw: RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_at: 2026-05-09T17:25:27.666Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, 9449977b, 1d49, 43b0]
---

# Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68

## Summary
Describes the AiAgentNerd knowledge ingestion and cleanup workflow. Unstructured input is compiled from `RAW/` into structured `WIKI/` notes via a preview/confirm pipeline. Documents the command interface for saving, merging, and cleaning knowledge, plus observed behavior where preview states can expire before confirmation.

## Key Concepts
- **RAW → WIKI pipeline**: Unstructured input is auto-categorized, named, and compiled into structured markdown with `compiled_at` timestamps
- **Preview/confirm interlock**: All saves and merges require a preview step followed by explicit confirmation; no direct-save bypass is currently documented
- **Knowledge Cleanup Agent**: Background scan that groups duplicates, similar topics, and low-value notes for review without auto-modifying files
- **Canonical merging**: New information is merged into existing canonical files rather than creating duplicates
- **Safety defaults**: Archive preferred over delete; backups created before changes; no automatic deletions

## Practical Use
**Ingestion triggers**
- `Clean this up and save it` — ingest raw content directly
- `Save this to knowledge with preview` — stage a preview for review
- `Clean this up` — format without saving

**Merge triggers**
- `Merge these` — combine multiple raw chunks
- `Merge this with existing knowledge about <topic> with preview` — target merge by topic
- `Merge this with existing file <filename>.md with preview` — merge into specific file
- `confirm merge` / `cancel merge`

**Cleanup triggers**
- `cleanup knowledge` — full knowledge base scan
- `cleanup knowledge about <topic>` — scoped scan
- `merge cleanup group <n> into canonical with preview` — deduplicate
- `archive cleanup group <n>` — archive flagged group
- `delete cleanup group <n>` — restricted to high-confidence cases only
- `confirm cleanup merge` / `confirm archive` / `cancel cleanup`

**Utility triggers**
- `Split this into multiple notes` — break large inputs into separate notes
- `confirm` / `cancel` — generic preview approval/rejection

## Implementation Notes
- **Frontmatter generation**: The system auto-generates `category`, `filename`, and `type: raw` for new captures
- **Preview expiration**: Observed in OpenWebUI integration where `confirm save` returned "No pending knowledge preview found. It may have expired; create a new preview first." This implies preview state is held temporarily server-side and can time out.
- **No direct-save flag**: The compilation pipeline does not expose a `--no-preview` parameter or direct-save endpoint; all mutations must pass through the preview/confirm flow
- **Cleanup group format**: Output includes `duplicate group`, `low-value group`, and `similar topic group`; each lists affected files, a confidence score, and a recommended action (`merge`, `archive`, `ignore`)

## Related
- [[knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
