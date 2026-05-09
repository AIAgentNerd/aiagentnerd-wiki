---
title: Openwebui Save To Knowledge Category Architecture Filename Aiagentnerd Backend Hardeni 909d0e21 46ec 4eb0 A526 F3c3ebef4fa9
source_raw: RAW/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9.md
compiled_wiki_path: WIKI/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9.md
compiled_at: 2026-05-09T18:06:45.457Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, save, knowledge, category, architecture, filename]
---

# Openwebui Save To Knowledge Category Architecture Filename Aiagentnerd Backend Hardeni 909d0e21 46ec 4eb0 A526 F3c3ebef4fa9

## Summary
This note documents the debugging and hardening phase that moved the AiAgentNerd / Hermes backend knowledge system from a fragile prototype to a deterministic, production-grade ingestion and compilation engine. The work focused on making save-to-knowledge resilient, deterministic, and safe across RAW ingestion, WIKI compilation, Git sync, cleanup operations, and intent routing.

## Key Concepts
- **RAW as source of truth**: WIKI is derived from RAW; RAW files are preserved exactly or normalized safely.
- **Preview-before-confirm**: all Save-to-Knowledge writes require user preview and explicit confirmation.
- **Deterministic intent routing**: command detection relies on the first command line so pasted content does not accidentally trigger actions.
- **Pending state safety**: only one pending action (ingestion, merge, cleanup, auto cleanup, mark superseded) may exist at a time; new actions require resolving the existing one first.
- **Fuzzy pending commands**: during a pending state, variations like "save as new version", "merge existing", "overwrite file", "confirm", and "cancel" are understood without exact wording.
- **Chunking guard**: oversized prompts are detected before model calls; supported tasks (wiki_compile, merge_knowledge, cleanup_processing, save_to_knowledge_cleanup) use safe hard-split chunking, while unsupported generic chat is rejected.
- **Cleanup safety**: delete is disabled; archive is preferred; canonical files are protected; auto cleanup archives only high-confidence targets.
- **Archive filtering**: archived files are excluded from merge candidates, cleanup scans, and auto cleanup selection.
- **Git safety**: only explicitly touched files are staged; unrelated staged files cause push refusal; git commit uses argument-based execution; path traversal guards are in place.
- **RAW/WIKI consistency verification**: the compile pipeline verifies WIKI existence after compile, forces recompile on missing files or classifier target changes, archives stale copies, and updates the manifest only after verified success.
- **Compile failure recovery**: if compile appears to fail but the WIKI file exists with matching metadata, the system treats it as recovered success.
- **Logging privacy**: logs capture the first command line, message length, and selected handler rather than full pasted content.

## Practical Use
- **Ingestion**: paste messy or structured input; the system preserves valid RAW, normalizes near-RAW, cleans messy input through Clean Up Source, or falls back to safe RAW capture if cleanup fails.
- **Duplicate resolution**: when a file exists, Hermes offers merge, overwrite with preview, or save as new version; the default avoids overwriting.
- **Large input**: use supported task types for chunked processing; avoid pasting massive content into generic chat.
- **Cleanup operations**: run cleanup to scan for duplicates and low-value notes; review grouped recommendations and confirm merges or archives; no destructive changes happen automatically.
- **Git operations**: pushes include only known touched files; do not stage unrelated changes before a knowledge push.

## Implementation Notes
- **Save-to-Knowledge resilience**:
  - Valid RAW is preserved exactly.
  - Near-RAW is normalized locally.
  - Messy input is cleaned through Clean Up Source.
  - Failed cleanup produces a safe RAW capture fallback.
  - All save writes require preview and confirm.
- **File-exists resolution**:
  - Options: merge with existing, overwrite with preview, save as new version.
  - Default safe behavior avoids overwriting.
- **Fuzzy pending command matching**:
  - Only runs when a pending state exists.
  - Examples accepted: "save as new version", "save as a new version", "save new version", "merge existing", "merge with existing knowledge", "overwrite file", "replace file", "confirm", "yes save", "cancel", "never mind".
- **Pending state checks cover**: ingestion preview, merge preview, cleanup preview, auto cleanup preview, mark superseded preview.
- **Intent routing hardening**:
  - Detection relies on the first command line where practical.
  - Prevents pasted content from triggering save, merge, cleanup, or split commands accidentally.
- **Chunking hardening**:
  - Central OpenRouter guard detects oversized prompts before model calls.
  - Long lines and blocks are hard-split safely.
  - Chunking logs include size, threshold, and task type.
  - Supported tasks: `wiki_compile`, `merge_knowledge`, `cleanup_processing`, `save_to_knowledge_cleanup`.
- **Cleanup agent hardening**:
  - Delete is disabled.
  - Archive is preferred.
  - Canonical files are protected.
  - Auto cleanup archives only safe high-confidence targets; low and medium confidence groups are skipped.
  - All write actions require preview and confirmation.
- **Git safety changes**:
  - Removed `git add .`.
  - Only explicit touched files are staged.
  - Unrelated staged files cause push refusal.
  - `git commit` uses argument-based execution instead of shell-string interpolation.
  - Path traversal guards protect file operations.
- **RAW/WIKI consistency pipeline**:
  - WIKI existence is verified after compile.
  - Missing WIKI files force recompile.
  - Classifier target changes force recompile.
  - Stale old WIKI copies are archived.
  - Manifest entries are updated only after verified compile.
  - False compile failures are recovered when WIKI metadata proves success.
- **Logging privacy**:
  - Route-level errors use safe metadata, message, and code.
  - Avoids logging full user body/source content.
- **Tested flows**:
  - Messy input saves successfully.
  - Structured RAW saves successfully.
  - Duplicate filename resolution works.
  - Save as new version works.
  - Compile result includes `wikiPath`.
  - False `compile_failed` response was fixed.
  - RAW file is created.
  - WIKI file is created.
  - Git push succeeds.
  - Preview-first behavior works.
  - Fuzzy pending commands work.

## Related
- [[save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575]]
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[save-to-knowledge-with-preview-filename-codex-web-app-quickstart-and-command-sty-dd39234d-4541-4723-a5e0-174691c08c95]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[save-to-knowledge-skill]]

## Source
- RAW: [[RAW/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9]]
