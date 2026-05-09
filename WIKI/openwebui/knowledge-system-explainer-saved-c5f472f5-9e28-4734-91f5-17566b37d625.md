---
title: Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625
source_raw: RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_at: 2026-05-09T13:23:47.726Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, explainer, saved, c5f472f5, 9e28]
---

# Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625

## Summary
The AiAgentNerd knowledge system automates ingestion, structuring, and long-term maintenance of unstructured input through a dual-layer RAW/WIKI architecture. A strict confirm-then-save pipeline with persistent pending states, local content splitting, and periodic cleanup ensures safe, deterministic evolution of the knowledge base.

## Key Concepts
- **RAW Layer**: Editable source of truth. Stores original or cleaned input under `aiagentnerd-wiki/RAW/<category>/`.
- **WIKI Layer**: Compiled, structured output optimized for reuse. Stored under `aiagentnerd-wiki/WIKI/<category>/`. Not manually edited.
- **Ingestion Pipeline**: Input → intent detection → optional cleanup → preview generation → pending state → user confirmation → RAW save → compile → WIKI generation → Git commit/push.
- **Command Parsing**: Strict first-line evaluation only; commands are not inferred from message body to prevent accidental triggers.
- **Pending State**: Persistent singleton record (e.g., `aiagentnerd-system/tmp/pending-ingestions/hermes-pending-ingestion.json`) that blocks new ingestion until resolved. Never silently deleted.
- **Local Splitting**: Large inputs are split locally without LLM processing to avoid token limits. Chunks follow `topic-part-N.md` naming.
- **Merge Workflow**: Recombines split chunks or integrates new information into existing canonical notes, deduplicating while preserving unique insights.
- **Cleanup Agent**: Scans the knowledge base for duplicates, low-value notes, and topic fragmentation. Recommends merge, archive, or ignore. No automatic deletion.
- **Safety Guarantees**: Preview → confirm → save. Archive preferred over delete. Backups before destructive changes.
- **Git Discipline**: Only touched files are committed; global staging is avoided to maintain clean history.
- **Model Routing**: Selects models per task with safe fallbacks and finite retry limits.

## Practical Use
- **Capturing Knowledge**: Paste raw input and issue a save command. Use `with preview` to review categorization, filename, and structure before confirming.
- **Updating Knowledge**: Merge new content into existing notes by topic or filename rather than creating duplicates.
- **Maintenance**: Run `cleanup knowledge` or `cleanup knowledge about <topic>` to review suggested merges and archives. Confirm or cancel grouped actions individually.
- **Large Content**: If splitting occurs, confirm the batch save, then use the merge workflow to produce a canonical consolidated note.
- **Control Commands**: `confirm`, `cancel`, `confirm merge`, `cancel merge`, `archive cleanup group N`, `merge cleanup group N into canonical with preview`.
- **Constraints**:
  - WIKI files must not be edited directly; changes flow through RAW recompilation or merge.
  - Categories and filenames are system-generated to maintain consistency.
  - A pending action must be resolved before initiating a new one.

## Implementation Notes
- **Repository Structure**:
  - RAW source: `aiagentnerd-wiki/RAW/<category>/<filename>.md`
  - Compiled wiki: `aiagentnerd-wiki/WIKI/<category>/<filename>.md`
  - System memory/logs: `aiagentnerd-system`
- **Git Integration**: Commits are pushed to `github.com:AIAgentNerd/aiagentnerd-wiki.git` only after successful compilation.
- **Edge Cases**:
  - Duplicate filenames and conflicting categories are handled during ingestion.
  - Interrupted processes and partial saves are recoverable via the pending state.
  - Large batch operations are chunked to prevent model overload.
- **Error Avoidance**:
  - No hidden failures or silent truncation.
  - No inconsistent states between RAW and WIKI.
  - Infinite retries are explicitly prevented.
- **Planned Enhancements**: Automatic canonical note builders, smarter semantic merging, topic clustering, multi-user separation with permissions, real-time dashboards, and visual knowledge graphs.

## Related
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]
- [[cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[knowledge-cleanup-request-a247bbff-d697-4a97-8a17-1e56c851ba06]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625]]
