---
title: Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625
source_raw: RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_at: 2026-05-07T10:13:47.790Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, explainer, saved, c5f472f5, 9e28]
---

# Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625

## Summary
The AiAgentNerd knowledge system uses a dual-layer architecture (RAW/WIKI) to transform unstructured input into structured, evolving knowledge. RAW serves as the editable source of truth while WIKI provides compiled, read-only structured output. The system enforces strict safety through a persistent pending state, explicit confirmation gates, and deterministic command parsing.

## Key Concepts
- **Dual-layer architecture**: RAW layer (source of truth, editable, may contain noise) and WIKI layer (structured, compiled, optimized for reuse, not manually edited)
- **Ingestion pipeline**: input → RAW → compile → WIKI → Git → retrieval
- **Intent detection**: commands parsed strictly from the first line only; no content scanning for commands to prevent accidental triggers
- **Pending state**: persistent, acts as single source of truth for unconfirmed operations; never silently deleted; survives stage failures
- **Preview-confirm-save gate**: no irreversible action occurs without explicit user confirmation
- **Split workflow**: large inputs detected early, split locally without LLM overload, processed as chunks (e.g., `topic-part-1.md`)
- **Merge workflow**: identifies related chunks or notes, proposes canonical versions, consolidates content, removes duplication while preserving unique insights
- **Cleanup system**: scans for duplicates, low-value notes, and fragmentation; recommends merge, archive, or ignore; archive preferred over deletion; no automatic deletion
- **Model routing**: selects appropriate model per task with safe fallbacks; avoids infinite retries

## Practical Use
- **Capture**: paste raw input; use `Clean this up and save it` for automatic ingestion, or `Save this to knowledge with preview` to review before committing
- **Clean only**: `Clean this up` returns structured output without saving
- **Merge**: `Merge these` for multiple chunks; `Merge this with existing knowledge about <topic> with preview` to update canonical notes; `Merge this with existing file <filename>.md with preview` for targeted updates
- **Split**: `Split this into multiple notes` triggers local chunking when content exceeds safe thresholds
- **Confirm/Cancel**: `confirm`, `cancel`, `confirm merge`, `cancel merge` gate all destructive operations
- **Cleanup**: `cleanup knowledge` or `cleanup knowledge about <topic>` scans for duplicates, low-value notes, and similar topics; review grouped results (files, confidence, recommendation) then use `merge cleanup group <n> into canonical with preview`, `archive cleanup group <n>`, or `cancel cleanup`
- **Safety**: archive is preferred over delete; backups created before changes; no automatic deletion

## Implementation Notes
- **File paths**: RAW notes stored at `/home/nerd/aiagentnerd-wiki/RAW/<category>/<filename>`; compiled WIKI notes mapped to `<category>/<filename>`; system pending state stored at `/home/nerd/aiagentnerd-system/tmp/pending-ingestions/hermes-pending-ingestion.json`
- **Git target**: `github.com:AIAgentNerd/aiagentnerd-wiki.git`
- **Ingestion pipeline** (10 steps): receive input → detect intent → optional clean → generate preview → create pending state → user confirms → save RAW → compile → generate WIKI → Git commit/push
- **Chunk naming convention**: `topic-part-1.md`, `topic-part-2.md`, etc.
- **Command parsing**: strict first-line evaluation only; no content scanning for commands
- **Pending state requirements**: persistent; safe; single source of truth; never silently deleted; survives independent of later stage success/failure
- **Git constraints**: commit only touched files; avoid global staging; maintain clean history
- **Model routing**: select model per task; fallback safely; avoid infinite retries
- **Edge cases**: duplicate filenames, conflicting categories, partial saves, interrupted processes, large batch operations
- **Anti-patterns**: hidden failures, silent truncation, inconsistent states

## Related
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]
- [[cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[knowledge-cleanup-request-a247bbff-d697-4a97-8a17-1e56c851ba06]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625]]
