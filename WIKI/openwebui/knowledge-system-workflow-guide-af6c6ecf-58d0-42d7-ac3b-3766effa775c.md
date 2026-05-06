---
title: Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c
source_raw: RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_at: 2026-05-06T14:22:24.056Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, af6c6ecf, 58d0, 42d7]
---

# Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c

## Summary
The AiAgentNerd knowledge system is an ingestion and maintenance pipeline that converts unstructured raw input into structured, evolving knowledge. It automatically cleans, categorizes, and filenames content, uses a preview-confirm-save safety model to prevent accidental changes, and provides a cleanup agent for periodic knowledge base hygiene. The system is designed to merge new information into existing canonical files rather than create duplicates, improving structure and utility over time.

## Key Concepts
- **Ingestion pipeline**: Accepts raw input such as notes, transcripts, chat outputs, ideas, and random thoughts; transforms them into structured knowledge automatically
- **Automatic organization**: Auto-selects a category, generates a filename, structures content, and stores it in the correct location without manual filing decisions
- **Structured output format**: Every input is structured into topics, context, key concepts, steps (if procedural), commands (if relevant), and important details
- **Merge workflow**: New information is merged into existing knowledge files to prevent duplication; the system updates and improves existing content continuously
- **Preview-confirm-save safety model**: All modifying operations require a preview step and explicit user confirmation (`confirm`, `confirm merge`, etc.) before persistence
- **Knowledge Cleanup Agent**: Scans the entire knowledge base to find duplicates, detect similar topics, and identify low-value or noisy notes; groups them for review with confidence scores and recommendations
- **Cleanup actions**: merge into canonical, archive (preferred), ignore, or delete (restricted to high-confidence cases)
- **Safety behaviors**: No automatic deletion; archive preferred over delete; confirmation required for all changes; backups created before modifications
- **Fallback behavior**: If automatic cleaning fails, the system creates a safe raw capture preview with suggested frontmatter (`category`, `filename`, `type`)

## Practical Use
- **Save new knowledge (immediate)**: Paste content and invoke `Clean this up and save it`
- **Save new knowledge (with preview)**: Invoke `Save this to knowledge with preview`, review the generated preview, then reply `confirm`
- **Clean only (no save)**: Invoke `Clean this up` with the raw content
- **Merge multiple pieces**: Invoke `Merge these`, paste the separate raw chunks separated by `---`, then reply `confirm merge`
- **Improve existing knowledge by topic**: Invoke `Merge this with existing knowledge about <topic> with preview`, paste new information; if multiple files appear, select the target with `merge <number>` (e.g., `merge 1`), then `confirm merge`
- **Merge into a specific file**: Invoke `Merge this with existing file <filename>.md with preview`, paste new information, then confirm
- **Split large content**: Invoke `Split this into multiple notes` with the large content block
- **Cancel operations**: Use `cancel`, `cancel merge`, or `cancel cleanup` to abort
- **Run full cleanup**: Invoke `cleanup knowledge`
- **Run scoped cleanup**: Invoke `cleanup knowledge about <topic>`
- **Review cleanup groups**: Output includes duplicate groups, low-value groups, and similar-topic groups, each listing files, confidence, and recommendation
- **Merge cleanup duplicates**: `merge cleanup group 1 into canonical with preview` → `confirm cleanup merge`
- **Archive cleanup items**: `archive cleanup group 1` → `confirm archive`
- **Delete cleanup items** (restricted): `delete cleanup group 1` (only for high-confidence cases)
- **Daily flow**: Step 1 — capture (`Clean this up and save it`); Step 2 — improve (`Merge with existing knowledge`); Step 3 — combine (`Merge related ideas`)

## Implementation Notes
- **Frontmatter**: Saved notes include YAML frontmatter with `category`, `filename`, and `type` fields. When the system is uncertain, it may default to `category: inbox` and `type: raw`
- **Preview expiration**: Previews are temporary; if confirmation fails with "No pending knowledge preview found", regenerate the preview before confirming
- **Category selection**: The system auto-assigns categories; manual override is possible but unnecessary for normal use
- **Canonical files**: The cleanup agent suggests a main canonical file for each duplicate/similar group to serve as the merge target
- **Operational pattern**: Prefer merging into existing knowledge over creating new duplicate files; keep input raw and let the system handle cleanup
- **Topic-oriented retrieval**: Users should think in topics rather than filenames when querying or merging knowledge

## Related
- [[knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
