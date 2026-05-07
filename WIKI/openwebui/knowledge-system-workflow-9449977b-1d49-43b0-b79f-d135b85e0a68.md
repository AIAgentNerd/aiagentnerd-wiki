---
title: Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68
source_raw: RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_at: 2026-05-07T07:01:46.668Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, 9449977b, 1d49, 43b0]
---

# Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68

## Summary
Documents the AiAgentNerd knowledge ingestion and cleanup workflow, the operator command interface, and observed behaviors of the preview-confirmation pipeline. Explains how raw inputs are compiled into structured wiki notes and how the Knowledge Cleanup Agent maintains repository hygiene.

## Key Concepts
- **Ingestion Pipeline**: Compiled pages move from `RAW/` to `WIKI/` and receive a `compiled_at` timestamp
- **Preview Gate**: Saves require a preview step followed by operator confirmation; previews are stateful and can expire
- **Knowledge Cleanup Agent**: Scans the knowledge base for duplicates, similar topics, and low-value or noisy notes; groups them for review without auto-applying changes
- **Canonical File**: Preferred merge target when deduplicating during cleanup
- **Safety Model**: No automatic deletion; archive preferred over delete; confirmation required for all mutations; backups created before changes
- **Command-Driven Interface**: Operators use natural language commands to trigger ingestion, merge, split, and cleanup actions

## Practical Use
- **Save new knowledge**: `Clean this up and save it` (paste content), or `Save this to knowledge with preview` (paste content) → `confirm`
- **Clean only**: `Clean this up` (paste content)
- **Merge pieces**: `Merge these` (paste RAW chunks) → `confirm merge`
- **Improve existing topic**: `Merge this with existing knowledge about <topic> with preview` (new info) → if multiple files appear, `merge 1` → `confirm merge`
- **Merge specific file**: `Merge this with existing file <filename>.md with preview` (new info)
- **Split large content**: `Split this into multiple notes` (large content)
- **Cancel**: `cancel`, `cancel merge`

### Cleanup Workflow
- **Run scan**: `cleanup knowledge` or `cleanup knowledge about <topic>`
- **Review output**: Groups include duplicate group, low-value group, similar topic group; each lists files, confidence, and recommendation
- **Merge duplicates**: `merge cleanup group 1 into canonical with preview` → `confirm cleanup merge`
- **Archive files**: `archive cleanup group 1` → `confirm archive`
- **Delete (restricted)**: `delete cleanup group 1` — only works for high-confidence cases
- **Cancel cleanup**: `cancel cleanup`

### Procedural Notes
- Do not overthink categories; let the system decide.
- Prefer merge over duplicate; update existing files instead of re-saving.
- Use preview for important content.
- Think in topics, not files.
- Keep input raw and let the system handle cleanup.

## Implementation Notes
- The current compilation pipeline does not document a mechanism to bypass the preview step. The internal wiki only notes that compiled pages move from `RAW/` to `WIKI/` with a `compiled_at` timestamp; there is no confirmation interlock mentioned in the backend docs.
- If a preview expires before confirmation, the system returns: `No pending knowledge preview found. It may have expired; create a new preview first.`
- To add direct-save capability, a builder would likely need to:
  - Add a `--no-preview` flag or endpoint parameter to the compilation script/service
  - Expose a “Save Directly” UI action
  - Support a pre-approved CLI flag for command-line use
- During ingestion, the system auto-selects `category`, `filename`, and `type` metadata.
- Cleanup recommendations include `merge`, `archive`, or `ignore`.

## Related
- [[knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
