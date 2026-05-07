---
title: Openwebui Save To Knowledge Category Architecture Filename Aiagentnerd Backend Hardeni 909d0e21 46ec 4eb0 A526 F3c3ebef4fa9
source_raw: RAW/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9.md
compiled_wiki_path: WIKI/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9.md
compiled_at: 2026-05-07T05:57:05.525Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, save, knowledge, category, architecture, filename]
---

# Openwebui Save To Knowledge Category Architecture Filename Aiagentnerd Backend Hardeni 909d0e21 46ec 4eb0 A526 F3c3ebef4fa9

## Summary
This note documents the debugging and hardening phase that moved the AiAgentNerd / Hermes backend knowledge system from a fragile prototype to a deterministic, production-grade ingestion and compilation pipeline. The work focused on resilient input handling, safe preview-confirm workflows, deterministic intent routing, Git safety, and verified RAW-to-WIKI consistency. The result is a self-healing knowledge engine that reliably ingests messy or structured input, compiles it into usable knowledge, and maintains consistency over time without destructive automation.

## Key Concepts
- **RAW as source of truth**: all compiled WIKI knowledge is derived from immutable RAW captures.
- **Preview-then-confirm**: every write action—save, merge, cleanup, overwrite—requires explicit user confirmation after preview.
- **Deterministic intent routing**: command detection relies on the first input line so pasted content does not accidentally trigger actions.
- **Pending state safety**: only one pending action (ingestion, merge, cleanup, auto-cleanup, mark-superseded) may exist at a time; new requests must resolve the current one first.
- **Resilient ingestion**: valid RAW is preserved exactly, near-RAW is normalized locally, messy input is cleaned, and failed cleanup falls back to a safe RAW capture.
- **Archive-first cleanup**: delete is disabled; auto-cleanup only archives high-confidence targets and protects canonical files.
- **Git safety**: only explicitly touched files are staged; unrelated staged changes block push; commits use argument-based execution.
- **Verified consistency**: the compile pipeline verifies WIKI file existence after compilation and forces recompile on mismatch rather than trusting the manifest blindly.
- **Logging privacy**: logs capture the first command line, message length, and handler metadata—never full user pasted content.

## Practical Use
- **Core workflow**: paste any input (notes, transcripts, chat output, ideas) → the system previews the normalized RAW → confirm → save safely → compile into usable WIKI knowledge.
- **Handling messy vs structured input**: valid RAW is preserved exactly; near-RAW is normalized locally; messy input is cleaned automatically. If cleanup fails, the system falls back to a safe RAW capture so nothing is lost.
- **Resolving filename collisions**: when saving content whose filename already exists, Hermes presents a preview-first choice: merge with existing, overwrite with preview, or save as new version. The default is to avoid overwriting.
- **Large input handling**: oversized prompts are intercepted by an OpenRouter guard. If the task is a supported chunking type (`wiki_compile`, `merge_knowledge`, `cleanup_processing`, `save_to_knowledge_cleanup`), the content is split and processed safely. Generic chat that exceeds limits is rejected with a clear message.
- **Knowledge cleanup**: run `cleanup knowledge` or `cleanup knowledge about <topic>` to scan for duplicates, similar topics, and low-value notes. Review the grouped preview, then merge into a canonical file or archive. Auto-cleanup only touches high-confidence groups and never deletes.
- **Recovering compiles**: if a compile appears to fail but the WIKI file exists with matching metadata, the system recovers the success state automatically and logs the discrepancy for review.
- **Daily safety constraints**: never assume manifest state is correct—WIKI existence is verified. Git pushes only include known touched files. Logs never contain full pasted user content.

## Implementation Notes
- **Save-to-Knowledge resilience**: valid RAW is preserved exactly; near-RAW is normalized locally; messy input is routed through Clean Up Source; failed cleanup produces a safe RAW capture fallback. All save writes require preview and confirm.
- **File-exists resolution**: when a file already exists, Hermes offers three explicit choices: `merge with existing`, `overwrite with preview`, or `save as new version`. The default safe behavior avoids overwriting.
- **Fuzzy pending commands**: during an active pending state, the system understands variations such as `save as new version`, `save as a new version`, `save new version`, `merge existing`, `merge with existing knowledge`, `overwrite file`, `replace file`, `confirm`, `yes save`, `cancel`, and `never mind`. Fuzzy matching is only active when a pending state exists.
- **Pending state safety**: the system prevents multiple concurrent pending actions. Checked states include: `ingestion preview`, `merge preview`, `cleanup preview`, `auto cleanup preview`, and `mark superseded preview`. If a pending action exists, Hermes requires the user to confirm or cancel it first.
- **Intent routing hardening**: intent detection relies on the first command line of input. This prevents pasted source content from accidentally triggering `save`, `merge`, `cleanup`, or `split`.
- **Chunking hardening**: a central OpenRouter guard detects oversized prompts before model calls. Supported chunking task types are: `wiki_compile`, `merge_knowledge`, `cleanup_processing`, and `save_to_knowledge_cleanup`. Unsupported generic chat is rejected with a clear message. Long lines and blocks are hard-split safely; chunking logs record size, threshold, and task type.
- **Cleanup safety**: delete is disabled. Archive is preferred. Canonical files are protected. Auto-cleanup only archives safe high-confidence targets; low and medium confidence groups are skipped. All write actions require preview and confirmation.
- **Archive filtering**: archived files are excluded from merge candidates, cleanup scans, and auto-cleanup selection.
- **Git safety changes**:
  - Removed `git add .`
  - Only explicit touched files are staged
  - Unrelated staged files cause push refusal
  - `git commit` uses argument-based execution instead of shell-string interpolation
  - Path traversal guards protect file operations
- **RAW/WIKI consistency verification**:
  - WIKI existence is verified after compile
  - Missing WIKI files force recompile
  - Classifier target changes force recompile
  - Stale old WIKI copies are archived
  - Manifest entries are updated only after verified compile
- **Compile failure recovery**: if compilation reports failure but the WIKI file exists and its metadata matches, Hermes treats the compile as recovered success and logs the mismatch.
- **Logging privacy**: logs record the first command line instead of full pasted content, plus message length and selected handler. Route-level errors use safe metadata, message, and code. Full user body/source content is avoided.
- **Tested flows confirmed**: messy input save, structured RAW save, duplicate filename resolution, save-as-new-version, compile result includes `wikiPath`, false `compile_failed` response fix, RAW file creation, WIKI file creation, Git push success, preview-first behavior, and fuzzy pending commands.

## Related
- [[save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575]]
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[save-to-knowledge-skill]]
- [[save-to-knowledge-skill]]

## Source
- RAW: [[RAW/openwebui/save-to-knowledge-----category-architecture-filename-aiagentnerd-backend-hardeni-909d0e21-46ec-4eb0-a526-f3c3ebef4fa9]]
