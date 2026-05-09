---
title: Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625
source_raw: RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_at: 2026-05-09T18:39:52.007Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, explainer, saved, c5f472f5, 9e28]
---

# Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625

## Summary
Explanation of the AiAgentNerd knowledge system's dual-layer architecture (RAW/WIKI), ingestion pipeline, and operational workflows for splitting, merging, and cleaning up knowledge over time. The system transforms unstructured input into structured, evolving knowledge with mandatory preview/confirm safety gates.

## Key Concepts
- **RAW Layer**: Source of truth, editable, may contain noise or partial structure. Stores original or cleaned input.
- **WIKI Layer**: Structured, optimized for reuse, compiled from RAW, not manually edited.
- **Pipeline**: `input → RAW → compile → WIKI → Git → retrieval`.
- **Safety Pattern**: Preview → confirm → save. No irreversible action without user confirmation.
- **Split Workflow**: Large inputs detected early, split locally into chunks (e.g., `topic-part-1.md`), processed independently without LLM overload.
- **Merge Workflow**: Combines related chunks or updates existing knowledge into canonical notes, removing duplication while preserving unique insights.
- **Cleanup System**: Scans for duplicates, low-value notes, and fragmentation. Suggests merge, archive, or ignore. No automatic deletion.
- **Pending State**: Persistent, safe, single source of truth for unconfirmed operations. Never silently deleted.

## Practical Use
- **Daily Capture**: Paste raw input, optionally clean, save with preview. Let the system choose category and filename.
- **Improve Knowledge**: Merge new information with existing notes rather than creating duplicates.
- **Maintain**: Run cleanup to identify duplicates and low-value content. Review groups and confirm merge or archive actions.
- **Large Inputs**: Use split workflow for content exceeding safe thresholds; system creates batch previews for confirmation before saving multiple RAW files.
- **Command Safety**: Commands are parsed strictly from the first line only; content is never scanned for accidental triggers.
- **Confirmation Commands**: `confirm`, `cancel`, `confirm merge`, `cancel merge`, `confirm cleanup merge`, `confirm archive`.

## Implementation Notes
- **Ingestion Steps**: 1) receive input, 2) detect intent, 3) optionally clean, 4) generate preview, 5) create pending state, 6) user confirms, 7) save RAW file, 8) compile, 9) generate WIKI, 10) Git commit and push.
- **Chunk Naming Convention**: `topic-part-1.md`, `topic-part-2.md`, etc.
- **Git Behavior**: Only commits touched files; avoids global staging; maintains clean history.
- **Model Routing**: Selects appropriate model per task with safe fallback; avoids infinite retries.
- **Safety Behaviors**: Archive preferred over delete; backups created before changes; pending state persists independently of downstream success or failure.
- **Anti-Patterns Avoided**: Hidden failures, silent truncation, inconsistent states, hidden state changes.
- **Edge Cases Handled**: Duplicate filenames, conflicting categories, partial saves, interrupted processes, large batch operations.
- **Pending State Storage**: Persisted in `aiagentnerd-system` under `tmp/pending-ingestions/` (e.g., `hermes-pending-ingestion.json`).
- **File Paths**: RAW stored under `aiagentnerd-wiki/RAW/<category>/<filename>.md`; compiled WIKI output stored at corresponding wiki path.

## Related
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]
- [[cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[knowledge-cleanup-request-a247bbff-d697-4a97-8a17-1e56c851ba06]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625]]
