---
title: Architecture Aiagentnerd Backend Hardening Summary
source_raw: RAW/architecture/aiagentnerd-backend-hardening-summary.md
compiled_wiki_path: WIKI/architecture/aiagentnerd-backend-hardening-summary.md
compiled_at: 2026-05-05T07:19:32.798Z
type: system-note
tags: [aiagentnerd, compiled, architecture, backend, hardening, summary, git, hermes]
---

# Architecture Aiagentnerd Backend Hardening Summary

## Summary
This note summarizes the debugging and hardening phase for the AiAgentNerd / Hermes backend knowledge system. The goal was to transform the system from a fragile prototype into a deterministic, safe, production-grade backend capable of reliably ingesting messy or structured input, previewing changes, saving RAW files, compiling WIKI files, pushing to Git, and maintaining knowledge system consistency over time.

## Key Concepts
- **Core Product Behavior**: Paste anything, preview it, confirm it, save it safely, and make it usable knowledge.
- **RAW**: The source of truth.
- **WIKI**: The compiled, usable knowledge layer.
- **Save-to-Knowledge**: All writes now follow a preview before confirm flow.
- **Intent Routing**: Deterministic and command-driven.
- **Cleanup Actions**: Safe, preview-first, and archive-first.
- **RAW/WIKI Consistency**: Actively verified.
- **Git Operations**: Stage only touched files.
- **Logging Privacy**: Avoid storing full pasted content.

## Practical Use
- **Reliable Ingestion**: User input no longer fails easily; the system handles valid RAW, near-RAW, and messy input.
- **File-Exists Resolution**: Hermes offers safe choices when a file already exists (merge, overwrite, save as new version).
- **Fuzzy Pending Commands**: Pending commands are understood with fuzzy matching.
- **Pending State Safety**: Prevents multiple active pending actions from overwriting each other.
- **Intent Routing Hardening**: Commands are deterministic, and pasted content is treated as content.
- **Chunking Hardening**: Large input handling is more stable with central OpenRouter guard.
- **Cleanup Safety**: Delete is disabled, and archive is preferred.
- **Archive Filtering**: Archived files are excluded from merge candidates, cleanup scans, and auto cleanup selection.
- **Git Safety**: Git operations are safer with explicit staging and path traversal guards.
- **RAW/WIKI Consistency**: Compile pipeline verifies consistency.
- **Compile Failure Recovery**: Handles cases where compile appears to fail but WIKI output exists.
- **Logging Privacy**: Logs first command line instead of full pasted content.

## Implementation Notes
- **Save-to-Knowledge Resilience**:
  - Valid RAW is preserved exactly.
  - Near-RAW is normalized locally.
  - Messy input is cleaned through Clean Up Source.
  - Failed cleanup produces a safe RAW capture fallback.
  - All save writes require preview and confirm.
- **File-Exists Resolution**:
  - Hermes offers safe choices: merge with existing, overwrite with preview, save as new version.
  - Default safe behavior avoids overwriting and uses preview-first resolution.
- **Fuzzy Pending Commands**:
  - Examples understood: "save as new version", "merge with existing", "overwrite file", "confirm", "cancel".
  - Fuzzy matching only runs when a pending state exists.
- **Pending State Safety**:
  - Checks cover ingestion preview, merge preview, cleanup preview, auto cleanup preview, and mark superseded preview.
  - Prevents multiple active pending actions.
- **Intent Routing Hardening**:
  - Commands are detected from the first command line.
  - Pasted content is treated as content.
  - Reduces accidental execution risk.
- **Chunking Hardening**:
  - Oversized prompts are detected before model calls.
  - Supported tasks use chunking; unsupported generic chat is rejected.
  - Long lines and blocks are hard-split safely.
  - Chunking logs show size, threshold, and task type.
- **Cleanup Safety**:
  - Delete is disabled; archive is preferred.
  - Canonical files are protected.
  - Auto cleanup only archives safe high-confidence targets.
  - Low and medium confidence groups are skipped.
  - All write actions require preview and confirmation.
- **Archive Filtering**:
  - Archived files are excluded from merge candidates, cleanup scans, and auto cleanup selection.
- **Git Safety**:
  - Removed `git add .`.
  - Only explicit touched files are staged.
  - Unrelated staged files cause push refusal.
  - Git commit uses argument-based execution.
  - Path traversal guards protect file operations.
- **RAW/WIKI Consistency**:
  - WIKI existence is verified after compile.
  - Missing WIKI files force recompile.
  - Classifier target changes force recompile.
  - Stale old WIKI copies are archived.
  - Manifest entries are updated only after verified compile.
  - False compile failures can be recovered.
- **Compile Failure Recovery**:
  - If the WIKI file exists and metadata matches, Hermes treats the compile as recovered success and logs the mismatch.
- **Logging Privacy**:
  - Logs first command line instead of full pasted content.
  - Logs message length and selected handler.
  - Avoids full user body/source content.
  - Route-level errors use safe metadata, message, and code.

## Related
- [[knowledge-ingestion-system]]
- [[mobile-ingestion-and-hermes-skill]]
- [[knowledge-ingestion-system]]
- [[mobile-ingestion-and-hermes-skill]]
- [[aiagentnerd-master-notes]]

## Source
- RAW: [[RAW/architecture/aiagentnerd-backend-hardening-summary]]
