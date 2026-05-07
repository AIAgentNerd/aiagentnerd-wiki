---
title: Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625
source_raw: RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_at: 2026-05-07T06:48:26.680Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, explainer, saved, c5f472f5, 9e28]
---

# Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625

## Summary
AiAgentNerd uses a dual-layer RAW/WIKI architecture to ingest unstructured input, compile it into structured knowledge, and evolve it over time through merge and cleanup workflows. The system enforces strict safety via preview-confirm-save gates, persistent pending states, and local splitting for large content to avoid LLM token limits.

## Key Concepts
- **RAW Layer**: Source-of-truth storage for original or cleaned input. Editable, may contain noise or partial structure.
- **WIKI Layer**: Compiled, structured output optimized for reuse. Generated from RAW; not manually edited.
- **Ingestion Pipeline**: input → RAW → compile → WIKI → Git → retrieval
- **Pending State**: Persistent safety gate requiring explicit confirmation before any permanent operation. Never silently deleted.
- **Local Splitting**: Large inputs are split locally into chunks (e.g., `topic-part-1.md`) before LLM processing to avoid token limits and overload.
- **Merge Workflow**: Consolidates related chunks or existing notes into canonical representations, removing duplication while preserving unique insights.
- **Cleanup Workflow**: Scans for duplicates, low-value notes, and topic fragmentation. Recommends merge, archive, or ignore. No automatic deletion.
- **Command Parsing**: Strict first-line-only parsing; content body is never scanned for commands to prevent accidental triggers.

## Practical Use
- **Capture**: Paste raw input and issue a save command. The system auto-detects intent, proposes a category and filename, and generates a preview.
- **Preview Gate**: Review the structured preview, then confirm or cancel. No RAW or WIKI files are written until confirmation.
- **Large Content**: If input exceeds safe thresholds, use the split workflow. The system divides content locally, creates a batch preview, and saves multiple RAW parts for independent compilation.
- **Evolve**: Merge new information with existing knowledge rather than creating duplicates. Target specific topics or filenames for precise updates.
- **Maintain**: Run cleanup to surface duplicate groups, low-value notes, and similar topics. Merge into canonical notes or archive noise.
- **Safety Defaults**: Archive is preferred over delete. Backups are created before changes. Destructive actions require high-confidence thresholds.

## Implementation Notes
- **Compilation Steps**:
  1. Input received
  2. Intent detected via strict first-line command parsing
  3. Content optionally cleaned
  4. Preview generated
  5. Pending state written (e.g., `/home/nerd/aiagentnerd-system/tmp/pending-ingestions/hermes-pending-ingestion.json`)
  6. User confirms
  7. RAW file saved to `/home/nerd/aiagentnerd-wiki/RAW/<category>/<filename>.md`
  8. Compile process runs
  9. WIKI file generated
  10. Git commit and push (only touched files staged; avoid global staging)
- **Chunk Naming Convention**: `topic-part-1.md`, `topic-part-2.md`, etc.
- **Git Constraints**: Commit only modified files; maintain clean history; push to `github.com:AIAgentNerd/aiagentnerd-wiki.git`.
- **Model Routing**: Select appropriate model per task with safe fallbacks and no infinite retries.
- **Determinism Requirements**: Every input must lead to predictable behavior. Edge cases—duplicate filenames, conflicting categories, partial saves, interrupted processes, large batch operations—must be handled explicitly. No hidden failures, silent truncation, or inconsistent states.
- **Future Enhancements**: Automatic canonical builders, smarter merging, topic clustering, multi-user knowledge separation, permissions/roles, real-time dashboards, visual knowledge graphs.

## Related
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]
- [[cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[knowledge-cleanup-request-a247bbff-d697-4a97-8a17-1e56c851ba06]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625]]
