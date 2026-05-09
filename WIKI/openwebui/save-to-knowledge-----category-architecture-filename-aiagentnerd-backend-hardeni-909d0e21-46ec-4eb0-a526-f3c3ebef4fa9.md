---
title: Openwebui Save To Knowledge Category Architecture Filename Aiagentnerd Backend Hardeni 909d0e21 46ec 4eb0 A526 F3c3ebef4fa9
source_raw: RAW/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9.md
compiled_wiki_path: WIKI/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9.md
compiled_at: 2026-05-09T17:09:31.592Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, save, knowledge, category, architecture, filename]
---

# Openwebui Save To Knowledge Category Architecture Filename Aiagentnerd Backend Hardeni 909d0e21 46ec 4eb0 A526 F3c3ebef4fa9

## Summary
This note captures the hardening phase that moved the AiAgentNerd / Hermes backend knowledge system from a fragile prototype to a deterministic, production-grade ingestion and compilation engine. The work focused on making the core loop—paste, preview, confirm, save RAW, compile WIKI, sync Git—resilient, safe, and self-healing while eliminating accidental data loss, unintended command execution, and noisy logging.

## Key Concepts
- **RAW is the source of truth**; WIKI is a compiled, usable derived layer.
- **Preview-before-confirm** is enforced for all Save-to-Knowledge writes.
- **Deterministic intent routing** uses the first command line only, preventing pasted content from accidentally triggering save, merge, cleanup, or split.
- **Pending state safety** allows only one active pending action at a time; fuzzy natural-language commands (e.g., “save as new version”, “merge existing”) are accepted only when a pending state exists.
- **File-exists resolution** offers merge, overwrite-with-preview, or save-as-new-version; the default is safe preview-first behavior.
- **Chunking guard** intercepts oversized prompts before OpenRouter model calls for supported tasks; unsupported generic chat is rejected.
- **Cleanup safety**: delete is disabled; archive is preferred; canonical files are protected; auto-cleanup only archives high-confidence targets.
- **Archive filtering** excludes archived files from merge candidates, cleanup scans, and auto-cleanup selection.
- **Git safety**: only explicitly touched files are staged; `git add .` removed; unrelated staged files block push; commits use argument-based execution; path traversal guards active.
- **RAW/WIKI consistency verification** replaces blind manifest trust with post-compile existence checks, forced recompiles for missing or reclassified files, and stale-copy archiving.
- **Compile failure recovery** detects false negatives by checking WIKI file existence and metadata.
- **Logging privacy** logs first command line, message length, and handler metadata rather than full user content.

## Practical Use
- **Ingestion**: paste structured or messy input; valid RAW is preserved exactly, near-RAW is normalized locally, and messy input is cleaned via Clean Up Source with a safe RAW-capture fallback if cleanup fails.
- **Duplicate handling**: when a target filename already exists, the operator is prompted to merge with existing, overwrite with preview, or save as a new version.
- **Pending commands**: during a pending save state, operators can respond with natural variants such as `save as new version`, `merge existing`, `overwrite file`, `confirm`, `cancel`, or `never mind`.
- **Cleanup workflow**: run `cleanup knowledge` or `cleanup knowledge about <topic>` to receive grouped recommendations (duplicate, low-value, similar). Operators then preview and confirm merges into canonical files or archive actions. No automatic deletion occurs.
- **Large input handling**: chunking auto-activates for `wiki_compile`, `merge_knowledge`, `cleanup_processing`, and `save_to_knowledge_cleanup`; other oversized generic chat is rejected with a clear message.

## Implementation Notes
- **Intent Routing Hardening**: intent detection is anchored to the first command line so that pasted source bodies are treated as content, reducing accidental command execution.
- **Pending State Checks**: the system blocks new actions if any pending action already exists across ingestion preview, merge preview, cleanup preview, auto cleanup preview, or mark-superseded preview.
- **Chunking**: a central OpenRouter guard detects prompt size against thresholds before model calls; long lines and blocks are hard-split safely; chunking logs record size, threshold, and task type.
- **Cleanup Agent**: scans the entire knowledge base and groups duplicates, similar topics, and low-value notes. Low- and medium-confidence groups are skipped. All writes require preview and confirmation; backups are created before changes.
- **Git Operations**: `git add .` was removed. Only known touched files are staged. `git commit` uses argument-based execution instead of shell-string interpolation. Unrelated staged files cause push refusal. Path traversal guards protect file operations.
- **Compile Pipeline**:
  - Verifies WIKI existence after compile.
  - Missing WIKI files trigger forced recompile.
  - Classifier target changes trigger forced recompile.
  - Stale old WIKI copies are archived.
  - Manifest entries update only after a verified compile.
  - False compile failures are recovered when WIKI metadata proves success.
- **Logging**: route-level errors return safe metadata, message, and code; full pasted user body/source content is omitted from logs.
- **System Rules**:
  - RAW is the source of truth; WIKI is derived from RAW.
  - Save-to-Knowledge always uses preview then confirm.
  - No destructive cleanup action runs automatically.
  - Delete is disabled; archive is preferred.
  - Canonical files must not be archived by auto cleanup.
  - Git pushes only include known touched files.
  - Logs should not contain full pasted user content.
- **Tested & Verified Flows**: messy input save, structured RAW save, duplicate filename resolution, save as new version, compile result includes `wikiPath`, false `compile_failed` response fix, RAW/WIKI file creation, Git push success, preview-first behavior, and fuzzy pending commands.

## Related
- [[save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575]]
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[save-to-knowledge-with-preview-filename-codex-web-app-quickstart-and-command-sty-dd39234d-4541-4723-a5e0-174691c08c95]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[save-to-knowledge-skill]]

## Source
- RAW: [[RAW/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9]]
