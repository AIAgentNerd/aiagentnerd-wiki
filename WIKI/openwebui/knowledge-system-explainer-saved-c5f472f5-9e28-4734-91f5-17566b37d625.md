---
title: Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625
source_raw: RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625.md
compiled_at: 2026-05-07T09:32:34.792Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, explainer, saved, c5f472f5, 9e28]
---

# Openwebui Knowledge System Explainer Saved C5f472f5 9e28 4734 91f5 17566b37d625

## Summary
This note captures a live system test of the AiAgentNerd knowledge ingestion pipeline, exercising RAW-to-WIKI compilation, large-content splitting, merge workflows, and cleanup behaviors. It documents the dual-layer knowledge architecture, strict command parsing, pending state safety mechanisms, and operational constraints including Git integration and model routing. The session includes a structured explainer, a deep-dive operational framework, and a repetitive stress test to verify local chunking and deterministic behavior.

## Key Concepts
- **RAW vs WIKI dual-layer architecture**: RAW is the editable source of truth; WIKI is compiled, structured, and not manually edited
- **Ingestion pipeline**: input → intent detection → optional cleaning → preview → pending state → user confirm → RAW save → compile → WIKI → Git → retrieval
- **Strict command parsing**: only the first line is evaluated for commands; content is never scanned for accidental triggers
- **Pending state system**: persistent, safe, single source of truth stored at `/home/nerd/aiagentnerd-system/tmp/pending-ingestions/hermes-pending-ingestion.json`; never silently deleted
- **Large content splitting**: detected early and split locally into chunks like `topic-part-1.md` without LLM processing; batch preview generated before confirmation
- **Merge workflow**: recombine split chunks or new info into canonical notes, removing duplication while preserving unique insights
- **Cleanup system**: scans all notes to detect duplicates, low-value content, and fragmentation; suggests merge, archive, or ignore; no automatic deletion
- **Safety model**: preview → confirm → save; archive preferred over delete; backups created before changes
- **Determinism**: explicit edge case handling; no hidden state changes, silent truncation, or hidden failures

## Practical Use
- **Ingesting new knowledge**: `Clean this up and save it` or `Save this to knowledge with preview` → review preview → `confirm`
- **Merging content**: `Merge these` for multiple chunks; `Merge this with existing knowledge about <topic> with preview` to update canonical notes; `Merge this with existing file <filename>.md with preview` for targeted updates
- **Splitting large inputs**: `Split this into multiple notes` triggers local chunking when content exceeds safe thresholds
- **Running cleanup**: `cleanup knowledge` or `cleanup knowledge about <topic>` generates groups (duplicate, low-value, similar topic); then `merge cleanup group N into canonical with preview` or `archive cleanup group N`
- **Confirming or canceling**: `confirm`, `cancel`, `confirm merge`, `cancel merge`, `confirm cleanup merge`, `confirm archive`, `cancel cleanup`
- **Daily flow**: capture raw input → merge with existing knowledge → combine related ideas → run periodic cleanup
- **System paths**: RAW files save to `/home/nerd/aiagentnerd-wiki/RAW/<category>/`; WIKI compiles to `WIKI/<category>/`; Git pushes to `github.com:AIAgentNerd/aiagentnerd-wiki.git`

## Implementation Notes
- **Pipeline stages**:
  1. Input received
  2. Intent detected from first line only
  3. Content optionally cleaned
  4. Preview generated
  5. Pending state written to `/home/nerd/aiagentnerd-system/tmp/pending-ingestions/hermes-pending-ingestion.json`
  6. User confirms via reply command
  7. RAW file saved to `/home/nerd/aiagentnerd-wiki/RAW/<category>/<filename>`
  8. Compile process runs (`compiled=1, skipped=0, failed=0` on success)
  9. WIKI file generated at `WIKI/<category>/<filename>`
  10. Git commit and push of only touched files to `github.com:AIAgentNerd/aiagentnerd-wiki.git`
- **Split behavior**: When inputs exceed safe thresholds, the system splits locally before LLM processing to avoid token limits and structured-output overhead. Chunks follow `topic-part-N.md` naming. Each chunk is saved as a separate RAW file and compiled individually.
- **Merge behavior**: After splitting, related chunks should be identified and consolidated into a canonical note. The system proposes the canonical target, merges content, removes duplication, and preserves unique insights.
- **Pending state requirements**: Must persist independently of success or failure in later stages. A pending action blocks new ingestion until confirmed or canceled.
- **Git constraints**: Only commit files touched by the current operation; avoid global staging (`git add .`) to maintain a clean history.
- **Model routing**: Select an appropriate model per task; implement safe fallbacks; avoid infinite retry loops.
- **Edge cases handled explicitly**: duplicate filenames, conflicting categories, partial saves, interrupted processes, and large batch operations.
- **Stress test observations**: The session included repetitive large blocks across six conceptual sections (ingestion, splitting, pending state, merging, cleanup, determinism) to verify that local chunking and pipeline safety behave deterministically under volume.

## Related
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]
- [[cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[knowledge-cleanup-request-a247bbff-d697-4a97-8a17-1e56c851ba06]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-explainer-saved-c5f472f5-9e28-4734-91f5-17566b37d625]]
