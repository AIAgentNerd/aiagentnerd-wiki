---
title: Architecture Aiagentnerd Backend Hardening Summary
source_raw: RAW/architecture/aiagentnerd-backend-hardening-summary.md
compiled_wiki_path: WIKI/architecture/aiagentnerd-backend-hardening-summary.md
compiled_at: 2026-05-05T06:56:28.221Z
type: system-note
tags: [aiagentnerd, compiled, architecture, backend, hardening, summary, git, hermes]
---

# Architecture Aiagentnerd Backend Hardening Summary

## Summary
This note summarizes the debugging and hardening phase for the AiAgentNerd / Hermes backend knowledge system. The goal was to transform the system from a fragile prototype into a reliable, production-grade backend capable of ingesting messy or structured input, previewing changes, saving RAW files, compiling WIKI files, and maintaining knowledge consistency over time.

## Key Concepts
- **Core Product Behavior**: Paste anything, preview it, confirm it, save it safely, and make it usable knowledge.
- **RAW**: The source of truth.
- **WIKI**: The compiled, usable knowledge layer.
- **Preview Before Confirm**: All Save-to-Knowledge writes now follow a preview before confirm flow.
- **Deterministic Intent Routing**: Intent detection relies on the first command line to prevent accidental command execution.
- **Safe Cleanup Actions**: Cleanup actions are preview-first and archive-first, ensuring no destructive actions run automatically.
- **RAW/WIKI Consistency**: Consistency is actively verified instead of blindly trusting the manifest.
- **Git Operations**: Only touched files are staged, and path traversal guards protect file operations.
- **Logging Privacy**: Logs avoid storing full pasted content and use safe metadata.

## Practical Use
- **Reliable Ingestion**: The system can handle messy or structured input without failing easily.
- **File-Exists Resolution**: When a file already exists, Hermes offers safe choices: merge with existing, overwrite with preview, or save as a new version.
- **Fuzzy Pending Commands**: Pending commands are understood with fuzzy matching, preventing accidental command execution.
- **Pending State Safety**: Multiple active pending actions are prevented from overwriting each other.
- **Intent Routing Hardening**: Commands are deterministic, and pasted content is treated as content.
- **Chunking Hardening**: Large input handling is more stable, with clear rejection of unsupported tasks.
- **Cleanup Safety**: Delete is disabled, and archive is preferred. Canonical files are protected.
- **Archive Filtering**: Archived files are excluded from merge candidates, cleanup scans, and auto cleanup selection.
- **Git Safety**: Git operations are safer, with only touched files staged and path traversal guards in place.
- **RAW/WIKI Consistency**: The compile pipeline verifies consistency, and false compile failures can be recovered.
- **Logging Privacy**: Logs are safer, reducing sensitive content exposure.

## Implementation Notes
- **Save-to-Knowledge Resilience**:
  - Valid RAW is preserved exactly.
  - Near-RAW is normalized locally.
  - Messy input is cleaned through Clean Up Source.
  - Failed cleanup produces a safe RAW capture fallback.
  - All save writes require preview and confirm.
- **File-Exists Resolution**:
  - Hermes offers safe choices when a file already exists: merge with existing, overwrite with preview, or save as a new version.
- **Fuzzy Pending Commands**:
  - Fuzzy matching is used for pending commands, preventing accidental command execution.
- **Pending State Safety**:
  - Pending state checks cover ingestion preview, merge preview, cleanup preview, auto cleanup preview, and mark superseded preview.
- **Intent Routing Hardening**:
  - Intent detection relies on the first command line to prevent accidental command execution.
- **Chunking Hardening**:
  - Oversized prompts are detected before model calls.
  - Supported tasks use chunking, and unsupported generic chat is rejected with a clear message.
  - Long lines and blocks are hard-split safely.
- **Cleanup Safety**:
  - Delete is disabled, and archive is preferred.
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
  - False compile failures can be recovered when WIKI metadata proves success.
- **Compile Failure Recovery**:
  - The system handles cases where compile appears to fail but WIKI output actually exists.
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
