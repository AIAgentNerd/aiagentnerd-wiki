---
title: Openwebui Broken Test Preview Bbffa48b Fb2b 4f65 Ac58 2963bd6e0b82
source_raw: RAW/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82.md
compiled_wiki_path: WIKI/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82.md
compiled_at: 2026-05-07T08:03:01.667Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, broken, preview, bbffa48b, fb2b, 4f65]
---

# Openwebui Broken Test Preview Bbffa48b Fb2b 4f65 Ac58 2963bd6e0b82

## Summary
OpenWebUI chat transcript capturing edge cases and failure modes in the AiAgentNerd knowledge ingestion pipeline. Demonstrates git push failures, reclassification target collisions, expired preview tokens, and pending-action blocking behavior during save-to-knowledge operations.

## Key Concepts
- **Preview workflow**: two-step save requiring preview generation followed by explicit `confirm save`
- **Pending action lock**: only one knowledge action may be pending at a time; new requests are blocked until confirmation or cancellation
- **Safe raw capture fallback**: when automatic cleaning fails, the system generates a literal raw preview instead of structured content
- **RAW vs compiled notes**: RAW files are unprocessed source captures; compiled notes are enriched, structured, and stored in `WIKI/` with metadata
- **Auto-categorization**: inputs are assigned categories (e.g., `inbox`, `concepts`, `architecture`) and auto-generated filenames
- **Git-backed persistence**: saves trigger git commits pushed to `github.com:AIAgentNerd/aiagentnerd-wiki.git`

## Practical Use
- Use `confirm save` to finalize a preview; if the preview expires, regenerate it
- Cancel existing pending actions before creating new previews when blocked
- If `raw_reclassification_target_exists` occurs, retry by compiling the existing RAW file rather than re-saving
- Expect compilation metrics (`compiled=N, skipped=N, failed=N`) and a target `wikiPath` after successful saves
- RAW files land in `/home/nerd/aiagentnerd-wiki/RAW/<category>/<filename>.md`
- Generic cancel commands may fail if not targeted at the specific pending action type

## Implementation Notes
- **Error states observed**:
  - `git_failed`: git push failed during save; may retry on next attempt
  - `raw_reclassification_target_exists`: a compiled note already exists for this RAW content; system suggests compiling `RAW/inbox/<file>.md` directly
  - `No pending knowledge preview found. It may have expired`: the preview token was invalidated before confirmation
- **Pipeline output example**:
  ```
  Compile: compiled=1, skipped=0, failed=0, wikiPath=concepts/random-messy-broken-test.md
  Git: To github.com:AIAgentNerd/aiagentnerd-wiki.git
     2faa26b..e52886a  main -> main
  ```
- **Directory mapping**:
  - RAW inputs: `RAW/inbox/...`
  - Compiled outputs: `concepts/...`, `architecture/...`, or `WIKI/...`
- The assistant distinguishes between RAW (original, unprocessed) and compiled (curated with frontmatter, summary, key concepts, cross-references)

## Related
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[random-messy-broken-test]]
- [[system-functionality-test-671903ef-e8f7-4afc-8ff2-ad2c8d1423eb]]
- [[lets-try-again-save-this-to-knowledge-with-preview-random-test-about-systems-architecture]]

## Source
- RAW: [[RAW/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82]]
