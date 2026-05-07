---
title: Openwebui Broken Test Preview Bbffa48b Fb2b 4f65 Ac58 2963bd6e0b82
source_raw: RAW/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82.md
compiled_wiki_path: WIKI/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82.md
compiled_at: 2026-05-07T09:53:16.649Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, broken, preview, bbffa48b, fb2b, 4f65]
---

# Openwebui Broken Test Preview Bbffa48b Fb2b 4f65 Ac58 2963bd6e0b82

## Summary
Transcript of a debugging session exercising the AiAgentNerd knowledge ingestion pipeline. Captures the preview-confirm-save workflow, the distinction between RAW and compiled notes, and specific failure modes including git push failures and reclassification target conflicts.

## Key Concepts
- **Preview Workflow**: Ingestion is gated by preview → confirm → save to prevent accidental writes
- **RAW Notes**: Unprocessed captures stored at `RAW/inbox/<filename>.md`
- **Compiled Notes**: Structured wiki outputs derived from RAW sources, written to category paths such as `concepts/` or `architecture/`
- **Pending Action State**: The system allows only one pending preview at a time; previews can expire
- **`git_failed`**: Save pipeline error when pushing to the remote wiki repository fails
- **`raw_reclassification_target_exists`**: Save pipeline error when the target compiled path for a RAW file already exists

## Practical Use
- Initiate ingestion with `Save this to knowledge with preview`, then reply `confirm save` after review
- Cancel or confirm any pending preview before starting a new ingestion request
- If confirmation fails with "No pending knowledge preview found", recreate the preview; do not retry the confirmation alone
- On `raw_reclassification_target_exists`, compile the existing RAW file directly rather than re-saving
- On `git_failed`, verify repository state and network connectivity to the git remote

## Implementation Notes
- RAW path on server: `/home/nerd/aiagentnerd-wiki/RAW/inbox/`
- Git remote: `github.com:AIAgentNerd/aiagentnerd-wiki.git`
- Compilation metrics reported per save: `compiled`, `skipped`, `failed`
- Auto-suggested metadata includes `category` (e.g., `inbox`) and `filename` derived from content
- RAW vs compiled distinction (as defined by the system):
  - RAW = original unprocessed source; unfiltered content without structure or enrichment
  - Compiled = curated wiki-ready document with added metadata, summary, key concepts, and cross-references
- Observed error messages:
  - `Save to Knowledge failed. Error: git_failed`
  - `Save to Knowledge failed. Error: raw_reclassification_target_exists`
  - `A pending action already exists. Please confirm or cancel it first.`
  - `No pending knowledge preview found. It may have expired; create a new preview first.`

## Related
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[random-messy-broken-test]]
- [[save-to-knowledge-with-preview-filename-codex-web-app-quickstart-and-command-sty-dd39234d-4541-4723-a5e0-174691c08c95]]
- [[system-functionality-test-671903ef-e8f7-4afc-8ff2-ad2c8d1423eb]]

## Source
- RAW: [[RAW/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82]]
