---
title: Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68
source_raw: RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_at: 2026-05-09T15:52:26.084Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, 9449977b, 1d49, 43b0]
---

# Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68

## Summary
Documents the AiAgentNerd knowledge system ingestion, merge, and cleanup workflow, along with an observed operational issue where the preview confirmation step expires before save, blocking the compilation pipeline.

## Key Concepts
- **Preview-confirm-save interlock**: All knowledge writes require a staged preview and explicit confirmation before being committed to the wiki.
- **Automatic ingestion**: Raw input (notes, transcripts, chat outputs, ideas) is automatically categorized, assigned a filename, and structured into topics, context, key concepts, steps, commands, and details.
- **Raw capture fallback**: If automatic cleaning fails, the system falls back to a safe raw capture preview that preserves literal input with minimal processing.
- **Merge workflow**: New information is merged into existing knowledge rather than creating duplicates; the system suggests target files or topics for integration.
- **Cleanup agent**: Scans the entire knowledge base for duplicates, similar topics, and low-value or noisy notes. Results are grouped by type with confidence scores and recommended actions (merge, archive, ignore).
- **Safety behavior**: No automatic deletion; archive is preferred over delete; all destructive actions require explicit confirmation; backups are created before changes.

## Practical Use
- **Daily capture**: `Clean this up and save it` → paste content. For review first: `Save this to knowledge with preview` → paste content → `confirm`.
- **Clean only (no persistence)**: `Clean this up` → paste content.
- **Merge multiple chunks**: `Merge these` → paste raw chunks → `confirm merge`.
- **Improve existing knowledge**: `Merge this with existing knowledge about <topic> with preview` → if multiple files match, `merge 1` → `confirm merge`.
- **Targeted merge**: `Merge this with existing file <filename>.md with preview`.
- **Split large content**: `Split this into multiple notes`.
- **Cleanup commands**: `cleanup knowledge` or `cleanup knowledge about <topic>`. Review output groups, then:
  - Merge: `merge cleanup group 1 into canonical with preview` → `confirm cleanup merge`
  - Archive: `archive cleanup group 1` → `confirm archive`
  - Delete (restricted): `delete cleanup group 1` (only high-confidence cases)
  - Cancel: `cancel cleanup`
- **Constraints**: Prefer merge over duplicate; use preview for important content; think in topics rather than files; keep input raw and let the system structure it.
- **Warning**: The preview state can expire before confirmation, producing the error `No pending knowledge preview found. It may have expired; create a new preview first.` If this occurs, regenerate the preview and confirm immediately.

## Implementation Notes
- Raw captures carry frontmatter: `category`, `filename`, and `type: raw`.
- The compilation pipeline moves pages from `RAW/` to `WIKI/` and appends a `compiled_at` timestamp.
- There is currently no documented `--no-preview` flag, direct-save endpoint, or CLI parameter to bypass the confirmation interlock. Adding one would require modifying the compilation service or trigger logic.
- Cleanup groups are: duplicate group, low-value group, similar topic group. Each group lists affected files, a confidence score, and a recommendation.
- The transcript records two sequential failures of the preview-confirm step on identical input, suggesting the preview TTL or state store may be too short for interactive use.

## Related
- [[knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
