---
title: Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68
source_raw: RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_at: 2026-05-09T17:39:30.089Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, 9449977b, 1d49, 43b0]
---

# Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68

## Summary
Documents the AiAgentNerd knowledge ingestion and maintenance workflow, including the command-driven interaction model, preview-confirm-save pipeline, merge behaviors, and cleanup agent operations. Defines the safety constraints and directory conventions that govern how raw captures become structured wiki entries.

## Key Concepts
- **Preview-Confirm-Save Pipeline**: All knowledge mutations require an explicit preview stage and user confirmation before persistence; no direct-save bypass is currently implemented
- **RAW/ to WIKI/ Compilation**: Source material enters via `RAW/` and is compiled into `WIKI/` with generated frontmatter and a `compiled_at` timestamp
- **Command-Driven Interface**: Specific natural-language phrases trigger ingestion, merge, split, and cleanup operations
- **Knowledge Cleanup Agent**: Scans the knowledge base for duplicates, similar topics, and low-value notes; surfaces grouped recommendations for review
- **Safety Controls**: No automatic deletion; archive is preferred over delete; backups are created before changes; previews can expire if not confirmed promptly
- **Frontmatter Schema**: Raw captures include `category`, `filename`, and `type` (e.g., `type: raw`) in the header

## Practical Use
- **Ingest new knowledge**: Use `Clean this up and save it` for automatic capture, or `Save this to knowledge with preview` to stage a preview first, then reply `confirm`
- **Clean without saving**: Use `Clean this up` followed by pasted content to format only
- **Merge multiple raw pieces**: Use `Merge these`, paste each chunk separated by `---`, then `confirm merge`
- **Update existing knowledge by topic**: Use `Merge this with existing knowledge about <topic> with preview`, then `confirm merge`; if multiple files match, select with `merge 1`
- **Update a specific file**: Use `Merge this with existing file <filename>.md with preview`
- **Split large content**: Use `Split this into multiple notes` followed by the large block
- **Cancel an operation**: Use `cancel`, `cancel merge`, or `cancel cleanup` to abort a pending preview
- **Run cleanup**: Use `cleanup knowledge` or `cleanup knowledge about <topic>` to trigger the cleanup agent
- **Review cleanup output**: The agent returns groups (duplicate, low-value, similar topic) with file lists, confidence scores, and recommendations (merge, archive, ignore)
- **Merge cleanup group**: Use `merge cleanup group <n> into canonical with preview`, then `confirm cleanup merge`
- **Archive cleanup group**: Use `archive cleanup group <n>`, then `confirm archive`
- **Delete (restricted)**: Use `delete cleanup group <n>` only for high-confidence cases

## Implementation Notes
- The compilation pipeline does not expose a `--no-preview` flag or direct-save endpoint; skipping preview would require adding a CLI parameter, a UI bypass button, or a pre-approved automation trigger
- Preview state is ephemeral and server-side; if confirmation is delayed the preview may expire with the message `No pending knowledge preview found. It may have expired; create a new preview first.`
- RAW files remain in `RAW/`; compiled wiki notes are written to `WIKI/` with structured frontmatter
- The cleanup agent never modifies content automatically; all actions require explicit operator confirmation
- Backups are generated before merge, archive, and delete operations

## Related
- [[knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
