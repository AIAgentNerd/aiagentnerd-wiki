---
title: Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625
source_raw: RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_at: 2026-05-09T18:29:39.354Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, explainer, saved, c5f472f5, 9e28]
---

# Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625

## Summary
The AiAgentNerd knowledge system is a dual-layer ingestion and compilation pipeline that transforms raw user input into structured, versioned wiki artifacts. This note documents the system’s architecture, ingestion stages, split/merge workflows for oversized content, cleanup procedures, safety mechanisms, and operational constraints as demonstrated in live system interactions.

## Key Concepts
- **Dual-layer architecture**: RAW layer (editable source of truth, may contain noise) and WIKI layer (structured, compiled, optimized for reuse, not manually edited)
- **Pipeline flow**: input → intent detection → optional clean → preview → pending state → user confirmation → RAW save → compile → WIKI generation → Git commit/push
- **Strict command parsing**: only the first input line is evaluated for commands; message bodies are never scanned for accidental triggers
- **Pending state safety**: persistent, single-source-of-truth preview state that is never silently deleted; operations expire if not confirmed (e.g., TTL observed in session)
- **Local splitting for large content**: inputs exceeding safe thresholds are split locally into chunks without LLM overload; chunks follow `topic-part-N.md` naming
- **Merge workflow**: recombine split chunks or related notes into a canonical file, removing duplication while preserving unique insights
- **Cleanup workflow**: scan the knowledge base for duplicates, low-value notes, and topic fragmentation; recommend merge, archive, or ignore with no automatic deletion
- **Safety defaults**: preview → confirm → save; archive preferred over delete; backups created before destructive changes
- **Git hygiene**: commit only touched files, avoid global staging, maintain clean history
- **Determinism requirement**: explicit edge-case handling; system must avoid hidden failures, silent truncation, and inconsistent state changes

## Practical Use
- **Ingest raw input**: paste content and trigger `Clean this up and save it` or `Save this to knowledge with preview`
- **Preview before commit**: always review the generated preview and confirm to prevent accidental overwrites; cancel if the structure is wrong
- **Handle large inputs**: use `Split this into multiple notes` when content exceeds safe token thresholds; the system batches previews and saves multiple RAW files independently
- **Recombine split knowledge**: after splitting, use merge workflows to consolidate chunks into a canonical note rather than leaving fragmented files
- **Improve existing knowledge**: prefer `Merge this with existing knowledge about <topic> with preview` or merge into a specific filename instead of creating duplicates
- **Run cleanup**: invoke `cleanup knowledge` or `cleanup knowledge about <topic>` to surface duplicate groups, low-value groups, and similar-topic groups
- **Act on cleanup suggestions**: merge a group into its canonical note (`merge cleanup group N into canonical with preview`), archive noise (`archive cleanup group N`), or delete only when restricted high-confidence criteria are met
- **Daily flow**: capture → improve (merge) → maintain (cleanup)

## Implementation Notes
- **RAW storage path**: `/home/nerd/aiagentnerd-wiki/RAW/<category>/<filename>.md`
- **Compiled WIKI path**: mirrors category structure under the WIKI root
- **Pending state file**: `/home/nerd/aiagentnerd-system/tmp/pending-ingestions/hermes-pending-ingestion.json`
- **Git remote**: `github.com:AIAgentNerd/aiagentnerd-wiki.git`
- **Chunk naming convention during split**: `topic-part-1.md`, `topic-part-2.md`, etc.
- **Compiler output structure**: compiled notes include topics, context, key concepts, steps, commands, and important details derived from RAW input
- **Explicitly handled edge cases**: duplicate filenames, conflicting categories, partial saves, interrupted processes, and large batch operations
- **Model routing behavior**: select task-appropriate models with safe fallback and avoid infinite retries
- **Compile status logging**: operations emit counters (`compiled=1, skipped=0, failed=0`) and target wiki paths for observability

## Related
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]
- [[cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[knowledge-cleanup-request-a247bbff-d697-4a97-8a17-1e56c851ba06]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625]]
