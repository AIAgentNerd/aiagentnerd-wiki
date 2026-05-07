---
title: Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68
source_raw: RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_at: 2026-05-07T07:40:02.927Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, 9449977b, 1d49, 43b0]
---

# Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68

## Summary
The AiAgentNerd knowledge system ingests unstructured raw input, compiles it into structured internal wiki notes, and maintains quality through a cleanup agent. All persistence operations pass through a preview-and-confirm gate. The internal wiki currently does not document a method to skip the preview step in the compilation pipeline.

## Key Concepts
- **Ingestion Pipeline**: Raw input is compiled from `RAW/` into structured notes under `WIKI/` with a `compiled_at` timestamp
- **Preview/Confirm Gate**: Every save, merge, and cleanup action requires an explicit preview followed by user confirmation before persistence
- **Automatic Structuring**: The system assigns a category, generates a filename, and structures content into topics, context, key concepts, steps, and commands
- **Knowledge Cleanup Agent**: Background process that scans the knowledge base, groups duplicates/similar topics/low-value notes, and recommends merge, archive, or ignore actions
- **Safety-First Design**: No automatic deletions; archive is preferred over delete; backups are created before changes; destructive actions require confirmation

## Practical Use
- **Save new knowledge**: `Clean this up and save it` (auto-save) or `Save this to knowledge with preview` (with review step), then reply `confirm`
- **Clean without saving**: `Clean this up` followed by pasted content
- **Merge multiple inputs**: `Merge these`, paste chunks separated by `---`, then `confirm merge`
- **Update existing knowledge**: `Merge this with existing knowledge about <topic> with preview` or `Merge this with existing file <filename>.md with preview`, then `merge 1` and `confirm merge` if multiple candidates appear
- **Split large content**: `Split this into multiple notes` followed by the large content block
- **Cancel any operation**: `cancel`, `cancel merge`, or `cancel cleanup`

### Cleanup Workflow
1. Trigger: `cleanup knowledge` or `cleanup knowledge about <topic>`
2. Review output groups: duplicate group, low-value group, similar topic group (each lists files, confidence, recommendation)
3. Resolve:
   - Merge: `merge cleanup group <n> into canonical with preview` → `confirm cleanup merge`
   - Archive: `archive cleanup group <n>` → `confirm archive`
   - Delete (restricted): `delete cleanup group <n>` — only available for high-confidence cases
   - Abort: `cancel cleanup`

### Daily Flow
1. Capture: `Clean this up and save it`
2. Improve: `Merge with existing knowledge`
3. Combine: `Merge related ideas`

## Implementation Notes
- **No Direct Save Bypass**: The compilation pipeline does not currently expose a `--no-preview` flag or endpoint parameter to skip the review interlock. Adding direct-save would require modifying the compilation service or UI to support a pre-approved flag
- **Cleanup Agent Behavior**: Scans are read-only until an operator acts on a group. The agent suggests a canonical file for duplicates and flags low-value content, but never modifies files autonomously
- **Confirmation Expiry**: Preview states can expire; if `confirm` is rejected with "No pending knowledge preview found", regenerate the preview first
- **File Conventions**: Raw captures use frontmatter with `category`, `filename`, and `type: raw`. Compiled wiki notes are stored in the target wiki path with compiled metadata

## Related
- [[knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
