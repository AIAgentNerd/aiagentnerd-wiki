---
title: Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625
source_raw: RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_at: 2026-05-07T10:35:19.476Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, explainer, saved, c5f472f5, 9e28]
---

# Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625

## Summary
The AiAgentNerd knowledge system uses a dual-layer architecture (RAW and WIKI) to ingest, structure, compile, and evolve knowledge over time. It enforces strict safety through preview/confirmation workflows, handles large content via local splitting, and maintains quality through merge and cleanup agents. The pipeline moves from raw input through automated compilation to structured wiki output with Git versioning, operating as a continuously learning external memory system.

## Key Concepts
- **RAW Layer**: Source of truth for all knowledge inputs. Editable, may contain noise or partial structure, stores original or cleaned input before compilation.
- **WIKI Layer**: Structured output optimized for reuse. Compiled from RAW via automated pipeline. Not manually edited.
- **Ingestion Pipeline**: `input → RAW → compile → WIKI → Git → retrieval`
- **Intent Detection**: Commands are parsed strictly from the first line only; content is never scanned to prevent accidental triggers.
- **Preview/Confirmation Safety**: All destructive or permanent operations require explicit user confirmation via a preview step. No irreversible actions occur automatically.
- **Pending State**: Persistent, safe, single source of truth for unconfirmed operations. Never silently deleted.
- **Large Content Splitting**: Content exceeding safe thresholds is split locally into chunks (e.g., `topic-part-1.md`) without LLM processing, then compiled individually.
- **Merge Workflow**: Combines related chunks or new information into existing knowledge, proposing canonical notes, removing duplication, and preserving unique insights.
- **Cleanup Agent**: Scans the knowledge base for duplicates, low-value notes, and similar topics. Suggests merge, archive, or ignore actions. No automatic deletion; archive preferred over delete.
- **Git Integration**: Commits only touched files, avoids global staging, and maintains clean history.

## Practical Use
- **Daily Capture**: Paste raw input and run `Clean this up and save it` or `Save this to knowledge with preview`, then confirm to persist.
- **Improvement**: Use `Merge this with existing knowledge about <topic> with preview` to evolve canonical notes rather than creating duplicates. Target specific files with `Merge this with existing file <filename>.md with preview`.
- **Large Content**: Use `Split large content` to break inputs into multiple RAW files automatically when thresholds are exceeded.
- **Maintenance**: Run `cleanup knowledge` or `cleanup knowledge about <topic>` to review duplicate groups, low-value groups, and similar topic groups.
- **Cleanup Actions**: Merge groups into canonical files (`merge cleanup group 1 into canonical with preview`), archive noise (`archive cleanup group 1`), or cancel. Restricted deletion is available only for high-confidence cases.
- **Confirmation Commands**: `confirm`, `cancel`, `confirm merge`, `cancel merge`, `confirm cleanup merge`, `confirm archive`.

## Implementation Notes
- **10-Step Ingestion Process**:
  1. Input received
  2. Intent detected (first line only)
  3. Content optionally cleaned
  4. Preview generated
  5. Pending state created
  6. User confirms
  7. RAW file saved
  8. Compile process runs
  9. WIKI file generated
  10. Git commit and push
- **Storage Paths**:
  - RAW: `/home/nerd/aiagentnerd-wiki/RAW/<category>/<filename>.md`
  - Pending state: `/home/nerd/aiagentnerd-system/tmp/pending-ingestions/hermes-pending-ingestion.json`
  - Wiki compiled path example: `concepts/aiagentnerd-knowledge-system-explainer-and-workflow.md`
  - Git remote: `github.com:AIAgentNerd/aiagentnerd-wiki.git`
- **Split Workflow**: Detects large inputs early to avoid LLM token limits and structured output costs. Splits locally, creates batch previews, saves multiple RAW files, and compiles each independently.
- **Merge Workflow**: After splitting, chunks should be recombined into a final canonical note to eliminate redundancy and create a high-quality artifact.
- **Safety Constraints**:
  - No automatic deletion
  - Archive preferred over delete
  - Backups created before changes
  - No silent truncation or hidden failures
- **Model Routing**: Selects appropriate model per task with safe fallback and avoids infinite retries.
- **Edge Cases Handled**: Duplicate filenames, conflicting categories, partial saves, interrupted processes, large batch operations.
- **Determinism**: Every input should lead to predictable behavior with explicit edge case handling and no hidden state changes.
- **Future Enhancements**: Automatic canonical builders, smarter merging, topic clustering, multi-user knowledge separation, permissions and roles, real-time dashboards, visual knowledge graphs.

## Related
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]
- [[cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[knowledge-cleanup-request-a247bbff-d697-4a97-8a17-1e56c851ba06]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625]]
