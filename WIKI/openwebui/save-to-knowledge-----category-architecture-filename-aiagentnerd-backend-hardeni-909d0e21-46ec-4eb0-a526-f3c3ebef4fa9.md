---
title: Openwebui Save To Knowledge Category Architecture Filename Aiagentnerd Backend Hardeni 909d0e21 46ec 4eb0 A526 F3c3ebef4fa9
source_raw: RAW/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9.md
compiled_wiki_path: WIKI/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9.md
compiled_at: 2026-05-07T06:54:27.665Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, save, knowledge, category, architecture, filename]
---

# Openwebui Save To Knowledge Category Architecture Filename Aiagentnerd Backend Hardeni 909d0e21 46ec 4eb0 A526 F3c3ebef4fa9

## Summary
This note documents the debugging and hardening phase that moved the AiAgentNerd / Hermes backend knowledge system from a fragile prototype to a deterministic, production-grade ingestion and compilation pipeline. The hardened system enforces preview-before-confirm on all writes, treats RAW as immutable source of truth, actively verifies WIKI consistency instead of trusting the manifest, and restricts Git operations to explicitly touched files. The core behavioral guarantee is: paste anything → preview → confirm → save safely → compile into usable knowledge.

## Key Concepts
- **RAW is source of truth**; WIKI is the compiled, usable knowledge layer derived from RAW
- **Preview-before-confirm** is enforced on all Save-to-Knowledge writes; no destructive action runs automatically
- **Resilient ingestion**: valid RAW is preserved exactly, near-RAW is normalized locally, messy input is cleaned through Clean Up Source, and failed cleanup falls back to a safe RAW capture
- **Deterministic intent routing** based on the first command line; pasted body content is treated as data, not commands
- **Pending state safety**: only one active pending action is allowed at a time; fuzzy command matching is enabled only when a pending state exists
- **Chunking guard**: oversized prompts are detected before model calls; supported tasks are chunked, unsupported generic chat is rejected with a clear message
- **Cleanup safety**: delete is disabled; archive is preferred; canonical files are protected; auto-cleanup is limited to safe, high-confidence targets
- **Archive filtering**: archived files are excluded from merge candidates, cleanup scans, and auto-cleanup selection
- **Git safety**: explicit file staging only (`git add .` removed); argument-based commit execution; path traversal guards; push refused if unrelated staged files exist
- **RAW/WIKI consistency verified actively**: WIKI existence is checked post-compile, missing files force recompile, classifier target changes force recompile, stale copies are archived, and manifest entries are updated only after verified compile
- **Compile failure recovery**: if a compile signals failure but the WIKI file exists with matching metadata, the system treats it as recovered success and logs the mismatch
- **Logging privacy**: logs record only the first command line and message length; full pasted user content is omitted; route-level errors expose only safe metadata, message, and code

## Practical Use
- **Standard ingestion flow**: paste input → system classifies and previews RAW → user confirms → saves RAW → compiles WIKI → pushes to Git
- **File collision resolution**: when a file already exists, the operator can merge with existing, overwrite with preview, or save as a new version; the default safe behavior avoids overwriting
- **Fuzzy pending commands**: during an active pending state, variants like `save as new version`, `merge existing`, `overwrite file`, `confirm`, `cancel`, and `never mind` are understood without exact wording
- **Cleanup workflow**: run a cleanup scan → review duplicate, similar, or low-value groups → preview merge or archive → confirm; low and medium confidence groups are skipped automatically
- **Large input handling**: chunking is automatically applied to `wiki_compile`, `merge_knowledge`, `cleanup_processing`, and `save_to_knowledge_cleanup`; other oversized generic chat is rejected
- **Operator constraints**: deletion is disabled in cleanup; Git pushes include only known touched files; commands cannot be triggered by pasted body content unless the first line is a command

## Implementation Notes
- **Intent routing**: the parser inspects only the first line for commands such as `save`, `merge`, `cleanup`, `split`, `confirm`, and `cancel`. Multi-line pasted content is ignored for command detection, reducing accidental execution risk.
- **Pending state checks**: active pending states cover ingestion preview, merge preview, cleanup preview, auto cleanup preview, and mark superseded preview. If a pending action exists, new requests are blocked until the user confirms or cancels.
- **Chunking hardening**: a central OpenRouter guard detects oversized prompts before model calls. Long lines and blocks are hard-split safely. Chunking logs include original size, threshold, and task type. Supported tasks are explicitly allow-listed; unsupported long inputs receive an actionable rejection message.
- **Cleanup agent behavior**: the Knowledge Cleanup Agent is restricted to archive-only actions. Auto-cleanup operates only on high-confidence targets. Canonical files must not be archived by auto cleanup. All write actions require a preview and explicit confirmation.
- **Git operations**: `git add .` was removed. Only explicitly touched files are staged. `git commit` uses argument-based execution instead of shell-string interpolation. Path traversal guards validate file paths. The push step is refused if unrelated staged files are detected.
- **Compile pipeline verification**: after compilation, the system verifies WIKI file existence. Missing WIKI files force a recompile. Classifier target changes also force a recompile. Stale old WIKI copies are archived before overwrite. Manifest entries are updated only after a verified compile. False `compile_failed` responses are recovered when WIKI metadata proves success.
- **Logging behavior**: route handlers log the first command line and payload length. They avoid embedding the full user message body. Error responses include safe metadata, a public message, and an error code.
- **Tested and confirmed flows**: messy input save, structured RAW save, duplicate filename resolution, save as new version, compile result includes `wikiPath`, false `compile_failed` fix, RAW file creation, WIKI file creation, Git push success, preview-first behavior, and fuzzy pending commands.

## Related
- [[save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575]]
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[save-to-knowledge-skill]]
- [[save-to-knowledge-skill]]

## Source
- RAW: [[RAW/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9]]
