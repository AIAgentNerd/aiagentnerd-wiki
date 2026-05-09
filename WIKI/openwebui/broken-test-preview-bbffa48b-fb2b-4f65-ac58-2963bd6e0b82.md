---
title: Openwebui Broken Test Preview Bbffa48b Fb2b 4f65 Ac58 2963bd6e0b82
source_raw: RAW/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82.md
compiled_wiki_path: WIKI/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82.md
compiled_at: 2026-05-09T15:13:30.772Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, broken, preview, bbffa48b, fb2b, 4f65]
---

# Openwebui Broken Test Preview Bbffa48b Fb2b 4f65 Ac58 2963bd6e0b82

## Summary
Transcript of OpenWebUI chat `bbffa48b-fb2b-4f65-ac58-2963bd6e0b82` documenting knowledge-system ingestion tests. Captures successful save workflows, assistant explanations of RAW vs. compiled notes, and multiple failure modes including git failures, reclassification conflicts, and preview-state desync.

## Key Concepts
- **Knowledge ingestion pipeline**: preview → confirm → save workflow for capturing chat content into the wiki
- **RAW notes**: Unprocessed captures stored in `RAW/inbox/`; original source documents without enrichment
- **Compiled notes**: Processed, structured versions stored in `WIKI/` with metadata, summaries, extracted concepts, and cross-references
- **Pending action conflicts**: The system blocks new previews when an existing preview awaits confirmation
- **Preview expiration**: Preview state can be lost between conversation turns, forcing recreation
- **Reclassification target exists**: Error returned when saving RAW content that has already been compiled and reclassified to a wiki category
- **Git integration**: Successful saves trigger commits to `github.com:AIAgentNerd/aiagentnerd-wiki.git`

## Practical Use
- Reference this transcript when debugging knowledge-ingestion failures in OpenWebUI
- `git_failed` indicates a repository or network failure during the save step
- `raw_reclassification_target_exists` means the RAW file already exists and was compiled; retry by compiling the existing RAW file directly rather than re-saving
- If the assistant loses pending-action context, the cancel command may fail with "No pending knowledge preview to cancel" or a generic "I need more context" response
- Prefer merging with existing knowledge over re-saving similar short test phrases to avoid reclassification conflicts and filename collisions

## Implementation Notes
- **Storage paths observed**:
  - RAW inbox: `/home/nerd/aiagentnerd-wiki/RAW/inbox/<filename>.md`
  - Compiled wiki: `WIKI/<category>/<filename>.md` (e.g., `concepts/`, `architecture/`)
- **Git output example**:
  ```
  To github.com:AIAgentNerd/aiagentnerd-wiki.git
     2faa26b..e52886a  main -> main
  ```
- **Compilation stats example**: `compiled=1, skipped=0, failed=0, wikiPath=concepts/random-messy-broken-test.md`
- **Assistant behavior issue**: When the user issued "cancel it first" to clear a pending knowledge action, the assistant responded with a generic request for context instead of canceling, indicating pending-action state may not be reliably tracked across turns or bound to intent
- **Filename generation**: Derived from user input text; verbose or quoted inputs produce verbose filenames (e.g., `lets-try-again-save-this-to-knowledge-with-preview-random-test-about-systems-architecture.md`)
- **Successful ingestions recorded**:
  - `random-messy-broken-test.md` → compiled to `concepts/`
  - `random-note-about-knowledge-systems-and-structure.md` → compiled to `architecture/`
  - `aiagentnerd-knowledge-system-explainer-and-workflow.md` → compiled to `concepts/`

## Related
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[random-messy-broken-test]]
- [[save-to-knowledge-with-preview-filename-codex-web-app-quickstart-and-command-sty-dd39234d-4541-4723-a5e0-174691c08c95]]
- [[system-functionality-test-671903ef-e8f7-4afc-8ff2-ad2c8d1423eb]]

## Source
- RAW: [[RAW/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82]]
