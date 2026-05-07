---
title: Openwebui Broken Test Preview Bbffa48b Fb2b 4f65 Ac58 2963bd6e0b82
source_raw: RAW/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82.md
compiled_wiki_path: WIKI/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82.md
compiled_at: 2026-05-07T10:41:54.762Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, broken, preview, bbffa48b, fb2b, 4f65]
---

# Openwebui Broken Test Preview Bbffa48b Fb2b 4f65 Ac58 2963bd6e0b82

## Summary
Transcript of a knowledge-system ingestion test session demonstrating the RAW→compiled pipeline, preview/confirm workflow, and failure modes. Includes the canonical explanation of RAW versus compiled notes and observed error states during save operations.

## Key Concepts
- **RAW notes**: original unprocessed captures imported directly from OpenWebUI or other feeds; stored in `RAW/` without enrichment
- **Compiled notes**: processed, structured outputs stored in `WIKI/` with added metadata, summaries, tags, and cross-references
- **Preview/confirm workflow**: two-phase save requiring explicit user confirmation before committing to the wiki
- **Pending action queue**: only one preview/save action may be in flight at a time; must confirm or cancel before starting another
- **Safe raw capture fallback**: when automatic cleaning fails, the system generates a `type: raw` preview instead of structured output
- **RAW reclassification**: compilation moves files from `RAW/inbox/` to category directories (e.g., `concepts/`, `architecture/`)

## Practical Use
- Reference this transcript when debugging ingestion failures or preview-state issues
- Use the RAW vs compiled distinction to explain the knowledge pipeline to operators
- Note the specific error signatures (`git_failed`, `raw_reclassification_target_exists`) for log analysis and alerting

## Implementation Notes
- **RAW storage path**: `/home/nerd/aiagentnerd-wiki/RAW/inbox/<filename>.md`
- **Compiled wiki paths observed**: `concepts/random-messy-broken-test.md`, `architecture/random-note-about-knowledge-systems-and-structure.md`
- **Git remote**: `github.com:AIAgentNerd/aiagentnerd-wiki.git`
- **Compilation report format**: `compiled=N, skipped=N, failed=N, wikiPath=<path>`
- **Git push output**: shows commit range and branch, e.g., `2faa26b..e52886a  main -> main`
- **Observed error states**:
  - `git_failed`: push to remote failed after local save
  - `raw_reclassification_target_exists`: compiled target already present when reprocessing
  - Preview expiration: unconfirmed previews expire, returning "No pending knowledge preview found"
- **Concurrency guard**: the system rejects new preview requests while a pending action exists for the same file
- **Auto-generated filenames**: derived from content, lowercased, hyphenated
- **Suggested categories**: `inbox` (default), `concepts`, `architecture`

## Related
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[random-messy-broken-test]]
- [[save-to-knowledge-with-preview-filename-codex-web-app-quickstart-and-command-sty-dd39234d-4541-4723-a5e0-174691c08c95]]
- [[system-functionality-test-671903ef-e8f7-4afc-8ff2-ad2c8d1423eb]]

## Source
- RAW: [[RAW/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82]]
