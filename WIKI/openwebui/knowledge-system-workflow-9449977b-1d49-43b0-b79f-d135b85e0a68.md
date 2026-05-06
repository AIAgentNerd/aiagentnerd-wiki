---
title: Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68
source_raw: RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_at: 2026-05-06T16:05:59.667Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, 9449977b, 1d49, 43b0]
---

# Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68

## Summary
The AiAgentNerd knowledge system ingests unstructured input—notes, transcripts, chat outputs, and raw thoughts—and automatically structures, categorizes, and stores it. The system supports iterative refinement through merging with existing knowledge and includes a cleanup agent for deduplication and maintenance. All writes pass through a preview-review-confirm cycle to prevent accidental overwrites.

## Key Concepts
- **Automatic Ingestion**: Accepts arbitrary raw input and transforms it into structured knowledge with topics, context, key concepts, steps, and commands.
- **Automatic Organization**: Selects a category, generates a filename, structures content, and places it in the correct storage location without manual folder management.
- **Knowledge Merging**: Updates existing files rather than creating duplicates, enabling continuous evolution of knowledge over time.
- **Preview-Confirm-Save Gate**: All persistence operations require a preview step followed by explicit confirmation (`confirm`, `confirm merge`, `confirm cleanup merge`, etc.).
- **Knowledge Cleanup Agent**: Scans the knowledge base for duplicates, similar topics, and low-value or noisy notes, grouping them for review with confidence scores and recommendations (merge, archive, ignore).
- **Safety-First Cleanup**: No automatic deletions; archive is preferred over delete; backups are created before changes; deletion is restricted to high-confidence cases only.
- **Three-Phase Daily Flow**: Capture (ingest raw input), Improve (merge with existing knowledge), Combine (merge related ideas).

## Practical Use
- **Save new knowledge**: Paste content and request `Clean this up and save it`. For a safety review, use `Save this to knowledge with preview`, then reply `confirm`.
- **Clean without saving**: Use `Clean this up` to format content without persisting it.
- **Merge multiple raw chunks**: Use `Merge these`, paste each chunk separated by `---`, then reply `confirm merge`.
- **Update existing knowledge by topic**: Use `Merge this with existing knowledge about <topic> with preview`. If multiple candidate files appear, select with `merge 1` (or appropriate index), then `confirm merge`.
- **Update a specific file**: Use `Merge this with existing file <filename>.md with preview`, then confirm.
- **Split oversized input**: Use `Split this into multiple notes` followed by the content.
- **Cancel pending operations**: Use `cancel`, `cancel merge`, or `cancel cleanup` to abort.
- **Run knowledge cleanup**: Trigger `cleanup knowledge` or scoped cleanup with `cleanup knowledge about <topic>`. Review output groups (duplicate, low-value, similar topic), each listing files, confidence scores, and recommendations.
- **Act on cleanup groups**:
  - Merge duplicates into a canonical file: `merge cleanup group <n> into canonical with preview`, then `confirm cleanup merge`.
  - Archive a group: `archive cleanup group <n>`, then `confirm archive`.
  - Delete (restricted): `delete cleanup group <n>` only works for high-confidence cases.

## Implementation Notes
- The compilation pipeline moves compiled pages from `RAW/` to `WIKI/` and applies a `compiled_at` timestamp.
- **No documented direct-save bypass**: The preview step is mandatory. Skipping it would require adding a `--no-preview` flag or endpoint parameter, exposing a "Save Directly" UI control, or triggering compilation with a pre-approved flag.
- **Preview expiration**: Previews can expire between generation and confirmation. If `confirm save` returns "No pending knowledge preview found. It may have expired," regenerate the preview before confirming.
- Hermes cannot modify wiki content or tooling unless explicitly instructed by a builder.
- Files are stored with frontmatter metadata such as `category`, `filename`, and `type` (e.g., `type: raw`).

## Related
- [[knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
