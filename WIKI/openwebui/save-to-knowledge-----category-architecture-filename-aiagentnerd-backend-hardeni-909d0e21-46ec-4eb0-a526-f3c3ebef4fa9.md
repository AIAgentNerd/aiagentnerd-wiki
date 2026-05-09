---
title: Openwebui Save To Knowledge Category Architecture Filename Aiagentnerd Backend Hardeni 909d0e21 46ec 4eb0 A526 F3c3ebef4fa9
source_raw: RAW/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9.md
compiled_wiki_path: WIKI/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9.md
compiled_at: 2026-05-09T18:11:20.593Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, save, knowledge, category, architecture, filename]
---

# Openwebui Save To Knowledge Category Architecture Filename Aiagentnerd Backend Hardeni 909d0e21 46ec 4eb0 A526 F3c3ebef4fa9

## Summary
This note documents the hardening phase that moved the AiAgentNerd / Hermes backend knowledge system from a fragile prototype to a deterministic, production-grade ingestion and compilation pipeline. It establishes the core contract that RAW is the source of truth, WIKI is the compiled usable layer, and all writes require preview and confirmation. Key improvements include resilient Save-to-Knowledge flows, deterministic intent routing, pending state safety, chunked large-input handling, archive-first cleanup, safer Git operations, active RAW/WIKI consistency verification, and privacy-hardened logging.

## Key Concepts
- **RAW as source of truth**; WIKI is the derived compiled knowledge layer
- **Preview-before-confirm** enforced on all Save-to-Knowledge writes
- **Command-driven intent routing** using first-line detection to avoid accidental execution from pasted content
- **Pending state safety**: only one active pending action at a time across ingestion preview, merge preview, cleanup preview, auto cleanup preview, and mark superseded preview
- **Fuzzy pending commands**: natural language confirmations accepted (e.g., `save as new version`, `merge existing`, `overwrite file`, `cancel`, `never mind`)
- **OpenRouter chunking guard** for oversized prompts on supported tasks
- **Archive-first cleanup**; deletion is disabled
- **Explicit Git staging** (`git add .` removed); unrelated staged files cause push refusal
- **Post-compile verification** of RAW/WIKI consistency instead of trusting the manifest blindly
- **Compile failure recovery** when WIKI output exists and metadata matches despite a reported failure
- **Privacy logging**: log first command line and metadata, never full pasted user content

## Practical Use
- **Core workflow**: paste input → preview → confirm → save RAW safely → compile into usable WIKI → sync to Git
- **File-exists resolution** offers merge with existing, overwrite with preview, or save as new version; default avoids overwriting and uses preview-first resolution
- **Fuzzy command matching** only runs inside an active pending state to prevent accidental execution
- **Archived files excluded** from merge candidates, cleanup scans, and auto cleanup selection to prevent reprocessing
- **Canonical files protected** from auto cleanup
- **Git operations** stage only explicitly touched files and use argument-based commit execution instead of shell-string interpolation
- **Path traversal guards** protect all file operations

## Implementation Notes
- **Save-to-Knowledge resilience**: valid RAW is preserved exactly; near-RAW is normalized locally; messy input is cleaned through Clean Up Source; failed cleanup produces a safe RAW capture fallback
- **Intent routing hardening**: commands are detected from the first line so pasted source content is treated as content, not commands
- **Chunking behavior**: oversized prompts detected before model calls; supported tasks use chunking (`wiki_compile`, `merge_knowledge`, `cleanup_processing`, `save_to_knowledge_cleanup`); unsupported generic chat is rejected with a clear message. Long lines and blocks are hard-split safely; chunking logs show size, threshold, and task type
- **Cleanup safety**: auto cleanup archives only high-confidence targets; low and medium confidence groups are skipped. All write actions require preview and confirmation
- **RAW/WIKI consistency**: WIKI existence is verified after compile; missing WIKI files force recompile; classifier target changes force recompile; stale old WIKI copies are archived; manifest entries are updated only after verified compile
- **Compile failure recovery**: if the WIKI file exists and its metadata matches the expected output, the system treats the compile as recovered success and logs the discrepancy
- **Logging**: logs first command line, message length, and selected handler; route-level errors expose only safe metadata, message, and code
- **Tested and confirmed flows**: messy input save, structured RAW save, duplicate filename resolution, save as new version, compile result includes `wikiPath`, false `compile_failed` response fix, RAW/WIKI file creation, Git push success, preview-first behavior, fuzzy pending commands

## Related
- [[save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575]]
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[save-to-knowledge-with-preview-filename-codex-web-app-quickstart-and-command-sty-dd39234d-4541-4723-a5e0-174691c08c95]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[save-to-knowledge-skill]]

## Source
- RAW: [[RAW/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9]]
