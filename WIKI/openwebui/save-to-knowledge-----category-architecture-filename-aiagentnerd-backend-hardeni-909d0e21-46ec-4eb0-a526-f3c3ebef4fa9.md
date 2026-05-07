---
title: Openwebui Save To Knowledge Category Architecture Filename Aiagentnerd Backend Hardeni 909d0e21 46ec 4eb0 A526 F3c3ebef4fa9
source_raw: RAW/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9.md
compiled_wiki_path: WIKI/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9.md
compiled_at: 2026-05-07T07:56:39.021Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, save, knowledge, category, architecture, filename]
---

# Openwebui Save To Knowledge Category Architecture Filename Aiagentnerd Backend Hardeni 909d0e21 46ec 4eb0 A526 F3c3ebef4fa9

## Summary
Documents the debugging and hardening phase that stabilized the AiAgentNerd / Hermes backend knowledge system. The work moved ingestion, compilation, cleanup, and Git synchronization from a fragile prototype to a deterministic, production-grade pipeline built on preview-first safety, deterministic intent routing, active consistency verification, and resilient error recovery.

## Key Concepts
- **RAW as source of truth** — immutable captured input; WIKI is the derived, compiled usable layer
- **Preview-before-confirm** — all Save-to-Knowledge writes require explicit preview and user confirmation before any filesystem or Git change
- **Deterministic intent routing** — commands are recognized from the first line only; pasted body content cannot accidentally trigger actions
- **Pending state safety** — only one pending action may be active at a time; overlapping requests are blocked until the current one is confirmed or cancelled
- **Resilient ingestion** — valid RAW is preserved exactly; messy input is cleaned locally or via Clean Up Source; failed cleanup falls back to a safe RAW capture
- **File-exists resolution** — duplicate filenames offer safe choices: merge with existing, overwrite with preview, or save as a new version
- **Chunking guard** — central OpenRouter oversized-prompt detection with safe hard-splitting for supported long-context tasks
- **Cleanup safety** — delete is disabled; archive is preferred; canonical files are protected; auto-cleanup only archives high-confidence targets
- **Git safety** — stage only explicitly touched files; refuse push if unrelated staged files exist; use argument-based commits
- **RAW/WIKI consistency verification** — manifest is not blindly trusted; WIKI existence and metadata are verified after compile
- **Compile failure recovery** — if a compile reports failure but the WIKI file exists with matching metadata, treat as recovered success
- **Logging privacy** — log first command line and message length only; never store full pasted user content

## Practical Use
- **Core ingestion flow** — paste anything → preview → confirm → save RAW safely → compile into usable WIKI knowledge.
- **Duplicate handling** — when a target filename already exists, Hermes offers merge, overwrite with preview, or save as a new version. The default safe behavior avoids overwriting.
- **Fuzzy pending commands** — during an active pending state, informal phrases are understood without exact wording, e.g. `save as new version`, `merge existing`, `overwrite file`, `replace file`, `confirm`, `yes save`, `cancel`, `never mind`. Fuzzy matching only runs when a pending state exists.
- **Cleanup workflow** — run `cleanup knowledge` or `cleanup knowledge about <topic>`. Review grouped duplicates, low-value notes, and similar topics. Merge into canonical files or archive groups. No automatic deletion.
- **Archive filtering** — archived files are excluded from merge candidates, cleanup scans, and auto-cleanup selection to prevent repeated reprocessing.
- **Verified flows** — messy input saves, structured RAW saves, duplicate resolution, save-as-new-version, compile result includes `wikiPath`, false `compile_failed` recovery, RAW/WIKI creation, Git push, preview-first behavior, and fuzzy pending commands.

## Implementation Notes
- **Save-to-Knowledge resilience**
  - Valid RAW is preserved exactly.
  - Near-RAW input is normalized locally.
  - Messy input is routed through Clean Up Source.
  - Failed cleanup produces a safe RAW capture fallback.
  - All save writes require preview and confirmation.
- **Intent routing hardening**
  - Intent detection relies on the first command line where practical.
  - Prevents pasted source content from triggering save, merge, cleanup, or split commands.
- **Pending state safety**
  - Multiple active pending actions are prevented.
  - Checked states: ingestion preview, merge preview, cleanup preview, auto cleanup preview, mark superseded preview.
  - If a pending action already exists, the user must confirm or cancel it first.
- **Chunking hardening**
  - Oversized prompts are detected before model calls.
  - Supported chunking tasks: `wiki_compile`, `merge_knowledge`, `cleanup_processing`, `save_to_knowledge_cleanup`.
  - Unsupported generic chat is rejected with a clear message.
  - Long lines and blocks are hard-split safely.
  - Chunking logs include size, threshold, and task type.
- **Cleanup safety**
  - Delete is disabled.
  - Archive is preferred over delete.
  - Canonical files must not be archived by auto cleanup.
  - Auto cleanup only archives safe, high-confidence targets.
  - Low and medium confidence groups are skipped.
  - All write actions require preview and confirmation.
- **Git safety**
  - Removed `git add .`; only explicit touched files are staged.
  - Unrelated staged files cause push refusal.
  - `git commit` uses argument-based execution instead of shell-string interpolation.
  - Path traversal guards protect file operations.
- **RAW/WIKI consistency pipeline**
  - WIKI existence is verified after compile.
  - Missing WIKI files force recompile.
  - Classifier target changes force recompile.
  - Stale old WIKI copies are archived.
  - Manifest entries are updated only after verified compile.
- **Compile failure recovery**
  - If compile appears to fail but the WIKI file exists and metadata matches, Hermes treats the compile as recovered success and logs the mismatch.
- **Logging privacy**
  - Logs record the first command line instead of full pasted content.
  - Logs include message length and selected handler.
  - Route-level errors use safe metadata, message, and code only.

## Related
- [[save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575]]
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[save-to-knowledge-skill]]
- [[save-to-knowledge-skill]]

## Source
- RAW: [[RAW/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9]]
