---
title: Openwebui Broken Test Preview Bbffa48b Fb2b 4f65 Ac58 2963bd6e0b82
source_raw: RAW/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82.md
compiled_wiki_path: WIKI/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82.md
compiled_at: 2026-05-06T14:49:39.656Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, broken, preview, bbffa48b, fb2b, 4f65]
---

# Openwebui Broken Test Preview Bbffa48b Fb2b 4f65 Ac58 2963bd6e0b82

## Summary
OpenWebUI chat transcript documenting a test session of the knowledge ingestion pipeline. Demonstrates the preview/confirm save workflow, successful compilation paths, and multiple failure modes including git failures, reclassification conflicts, expired previews, and pending-action deadlocks. Includes the assistant’s definition of RAW versus compiled notes and a user-submitted explainer of knowledge system workflows used as test input.

## Key Concepts
- **Preview/confirm pattern**: Two-step ingestion where the assistant generates a preview with suggested category and filename, then awaits explicit user confirmation before saving to the wiki repo
- **RAW notes**: Original unprocessed captures stored under `RAW/<category>/<filename>.md`
- **Compiled notes**: Curated, structured outputs enriched with metadata, stored in category folders (e.g., `concepts/`, `architecture/`)
- **Automatic categorization**: System infers category (`inbox`, `concepts`, `architecture`) and generates kebab-case filenames from content
- **Git integration**: Each save commits and pushes to `github.com:AIAgentNerd/aiagentnerd-wiki.git` on branch `main`
- **Compile stats**: Reported as `compiled=X, skipped=Y, failed=Z, wikiPath=<path>`

## Practical Use
- **Typical flow**: Request preview → review suggested category/filename → reply `confirm save`
- **Expired previews**: If confirmation fails with "No pending knowledge preview found", recreate the preview; do not retry confirmation alone
- **Pending action conflicts**: When "A pending action already exists" appears, explicitly `confirm` or `cancel` before starting a new preview
- **Git failures**: If `Error: git_failed` occurs, verify repo state on the server; the RAW file may exist without a successful push
- **Reclassification errors**: `Error: raw_reclassification_target_exists` means the target compiled path already has a mapping; retry by compiling the RAW source directly rather than re-saving
- **Cancel ambiguity**: Bare `cancel` commands may be misinterpreted when context is thin; cancel works best when a preview is actively pending

## Implementation Notes
- **Server paths**:
  - RAW storage: `/home/nerd/aiagentnerd-wiki/RAW/<category>/<filename>.md`
  - Example compilations:
    - `RAW/inbox/random-messy-broken-test.md` → `concepts/random-messy-broken-test.md`
    - `RAW/inbox/random-note-about-knowledge-systems-and-structure.md` → `architecture/random-note-about-knowledge-systems-and-structure.md`
- **Git remote**: `github.com:AIAgentNerd/aiagentnerd-wiki.git`
- **Observed error states**:
  - `git_failed`: Git operation failed during save
  - `raw_reclassification_target_exists`: Previously classified target already exists; system suggests retrying compilation from RAW
  - Preview expiration: Preview token/state lost between turns
  - Orphaned pending state: Assistant tracks a pending preview that the user cannot confirm because it expired
- **Assistant behavior**: Can fall into loops where repeated confirmations fail due to stale state; creating a fresh preview usually resets the state machine
- **Submitted test payload**: A full knowledge system explainer covering ingestion, cleanup, merge workflows, and daily usage was pasted as test input during this session (assistant response to that specific submission was not captured in the transcript)

## Related
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[random-messy-broken-test]]
- [[system-functionality-test-671903ef-e8f7-4afc-8ff2-ad2c8d1423eb]]
- [[lets-try-again-save-this-to-knowledge-with-preview-random-test-about-systems-architecture]]

## Source
- RAW: [[RAW/openwebui/broken-test-preview-bbffa48b-fb2b-4f65-ac58-2963bd6e0b82]]
