---
title: Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c
source_raw: RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_at: 2026-05-09T15:18:35.749Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, af6c6ecf, 58d0, 42d7]
---

# Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c

## Summary
Operational documentation for the AiAgentNerd knowledge ingestion and cleanup interface. The system transforms unstructured input into structured notes, supports merging with existing knowledge, and enforces a preview-confirm-save safety model. A cleanup agent scans for duplicates and low-value content but requires explicit operator confirmation for all actions.

## Key Concepts
- **Automatic ingestion**: Accepts raw notes, transcripts, chat outputs, and unstructured text
- **Automatic organization**: Infers category, generates filename, structures content, and stores in the appropriate knowledge repository
- **Structured output**: Every input is structured into topics, context, key concepts, steps, commands, and important details
- **Merge workflow**: New information is merged into existing knowledge rather than creating duplicates
- **Preview-confirm-save**: All write operations require a preview step and explicit confirmation before persistence
- **Knowledge Cleanup Agent**: Scans the knowledge base for duplicates, similar topics, and low-value or noisy notes; groups findings for review
- **Cleanup actions**: merge into canonical, archive, ignore; delete is restricted to high-confidence cases
- **Safety constraints**: No automatic deletion; archive preferred over delete; backups created before changes

## Practical Use
**Ingestion commands**

- Save new knowledge: `Clean this up and save it` → paste content
- Save with preview: `Save this to knowledge with preview` → paste content → `confirm`
- Clean only (no save): `Clean this up` → paste content
- Merge multiple pieces: `Merge these` → paste chunk 1 → paste chunk 2 → `confirm merge`
- Improve existing knowledge: `Merge this with existing knowledge about <topic> with preview` → paste new info; if multiple files match, `merge 1` → `confirm merge`
- Merge into specific file: `Merge this with existing file <filename>.md with preview` → paste new info
- Split large content: `Split this into multiple notes` → paste large content
- Control verbs: `confirm`, `cancel`, `confirm merge`, `cancel merge`

**Cleanup commands**

- Run scan: `cleanup knowledge` or `cleanup knowledge about <topic>`
- Review groups: duplicate group, low-value group, similar topic group (each includes files, confidence, recommendation)
- Merge duplicates: `merge cleanup group <n> into canonical with preview` → `confirm cleanup merge`
- Archive files: `archive cleanup group <n>` → `confirm archive`
- Delete (restricted): `delete cleanup group <n>` (high-confidence cases only)
- Cancel: `cancel cleanup`

**Recommended daily flow**
1. Capture: `Clean this up and save it`
2. Improve: `Merge with existing knowledge`
3. Combine: `Merge related ideas`

## Implementation Notes
- The preview mechanism generates a temporary preview with suggested `category` and `filename`. Previews expire; if confirmation is delayed, the preview must be recreated.
- If automatic cleaning fails, the system falls back to a safe raw capture preview with `type: raw` and defaults the category to `inbox`.
- Knowledge notes use frontmatter fields including `category`, `filename`, and `type`.
- The cleanup agent never modifies the knowledge base automatically; all actions require operator confirmation.
- Operators should prefer merging over creating duplicates and let the system infer categories rather than manually specifying them.

## Related
- [[knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
