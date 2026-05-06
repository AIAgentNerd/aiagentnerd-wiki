---
title: Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625
source_raw: RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_at: 2026-05-06T14:07:07.200Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, explainer, saved, c5f472f5, 9e28]
---

# Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625

## Summary
The AiAgentNerd knowledge system is a dual-layer architecture that transforms unstructured input into structured, evolving technical knowledge. A strict ingestion pipeline—input → RAW → compile → WIKI → Git → retrieval—ensures auditability and safety. The system supports local content splitting for large inputs, merge workflows to prevent duplication, and a cleanup agent to maintain quality over time. All destructive operations require explicit confirmation through a persistent pending state.

## Key Concepts
- **RAW Layer**: Source of truth; editable; may contain noise or partial structure; stores original or cleaned input
- **WIKI Layer**: Structured; optimized for reuse; compiled from RAW; not manually edited
- **Ingestion Pipeline**: Input → intent detection → optional cleaning → preview → pending state → user confirmation → RAW save → compile → WIKI generation → Git commit/push
- **Pending State**: Persistent, safe, single source of truth; never silently deleted; expires after a defined timeout
- **Local Splitting**: Large inputs are split locally (not via LLM) into chunks named `topic-part-N.md` to avoid token limits
- **Merge Workflow**: Recombines split chunks or related notes into canonical representations, deduplicating while preserving unique insights
- **Cleanup Agent**: Scans for duplicates, low-value notes, and fragmentation; recommends merge, archive, or ignore; never auto-deletes
- **Command Parsing**: Strict first-line-only parsing; no content scanning for commands to prevent accidental triggers
- **Git Integration**: Commits only touched files; avoids global staging; maintains clean history
- **Model Routing**: Selects appropriate model per task with safe fallbacks and retry limits

## Practical Use
- **Capture**: Paste raw input and issue `Clean this up and save it` or `Save this to knowledge with preview`, then reply `confirm` to finalize
- **Clean only**: Use `Clean this up` for transient formatting without saving
- **Merge multiple inputs**: Use `Merge these`, paste chunks, then `confirm merge`
- **Improve existing knowledge**: Use `Merge this with existing knowledge about <topic> with preview` or `Merge this with existing file <filename>.md with preview`, then confirm
- **Split large content**: Use `Split this into multiple notes` for inputs exceeding safe thresholds; system produces `topic-part-N.md` chunks for confirmation
- **Cleanup**: Run `cleanup knowledge` or `cleanup knowledge about <topic>` to review groups. Then:
  - `merge cleanup group 1 into canonical with preview` → `confirm cleanup merge`
  - `archive cleanup group 1` → `confirm archive`
  - `delete cleanup group 1` (restricted to high-confidence cases)
  - `cancel cleanup`
- **Daily flow**: Capture → Improve (merge with existing) → Combine (merge related ideas)
- **Safety**: Use preview for important content; prefer merge over duplicate; let the system choose categories; think in topics, not files

## Implementation Notes
- **Pipeline stages**: (1) Input received, (2) Intent detected, (3) Content optionally cleaned, (4) Preview generated, (5) Pending state created, (6) User confirms, (7) RAW file saved, (8) Compile process runs, (9) WIKI file generated, (10) Git commit and push
- **File paths**:
  - RAW storage: `/home/nerd/aiagentnerd-wiki/RAW/<category>/<filename>.md`
  - WIKI output: `<category>/<filename>.md`
  - Pending state: `/home/nerd/aiagentnerd-system/tmp/pending-ingestions/hermes-pending-ingestion.json`
- **Chunk naming convention**: `topic-part-1.md`, `topic-part-2.md`, `topic-part-3.md`
- **Command parsing rules**: Only the first line is evaluated for commands; the system does not scan message content for accidental triggers
- **Pending state requirements**: Must be persistent, safe, and the single source of truth; never silently deleted
- **Git requirements**: Commit only touched files; avoid global `git add`; maintain clean history
- **Model routing requirements**: Select model per task; fallback safely; avoid infinite retries
- **Edge cases handled**: Duplicate file names, conflicting categories, partial saves, interrupted processes, large batch operations
- **System constraints**: Avoid hidden failures, silent truncation, and inconsistent states; all destructive operations require explicit confirmation; archive is preferred over delete; backups are created before changes

## Related
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]
- [[cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[knowledge-cleanup-request-a247bbff-d697-4a97-8a17-1e56c851ba06]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625]]
