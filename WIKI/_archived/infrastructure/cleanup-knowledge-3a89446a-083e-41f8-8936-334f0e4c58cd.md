---
title: Openwebui Cleanup Knowledge 3a89446a 083e 41f8 8936 334f0e4c58cd
source_raw: RAW/openwebui/cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd.md
compiled_wiki_path: WIKI/infrastructure/cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd.md
compiled_at: 2026-05-03T20:07:30.178Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, cleanup, knowledge, 3a89446a, 083e, 41f8]
status: archived
archived_at: 2026-05-05T08:22:42.826Z
reclassified_to: architecture/cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd.md
---

# Openwebui Cleanup Knowledge 3a89446a 083e 41f8 8936 334f0e4c58cd

## Summary
Knowledge cleanup report generated via OpenWebUI chat `3a89446a-083e-41f8-8936-334f0e4c58cd`. The scan identified 20 candidate groups of duplicate, overlapping, or low-value files across the `RAW/` and `WIKI/` hierarchies. Default behavior was report-only; Group 1 was subsequently archived after explicit user confirmation.

## Key Concepts
- **Knowledge Cleanup**: Automated deduplication and quality review of RAW source files and compiled WIKI notes
- **Candidate Groups**: Clusters of files flagged for merge, archive, or canonical selection
- **Canonical Preference Rules**: RAW sources preferred over compiled WIKI; non-archived files prioritized; cleaner titles and better categories favored
- **Low-Value Noise**: Files classified as discardable without merge (e.g., empty or placeholder chats)
- **Report-Only Mode**: Default behavior does not modify files until explicitly confirmed

## Practical Use
- Use cleanup reports to identify duplicates between `RAW/` inputs and `WIKI/` compiled outputs
- Review canonical suggestions before merging; some carry low confidence and require user choice
- Execute archive commands for confirmed low-value groups to reduce noise
- Preserve RAW sources as canonical when duplicates exist between RAW and compiled WIKI versions

## Implementation Notes
- **Chat ID**: `3a89446a-083e-41f8-8936-334f0e4c58cd`
- **Groups found**: 20
- **Group 1 archived**: `RAW/openwebui/new-chat-fba354d7-5e23-430f-a0de-89635cec202b.md` (classification: `low_value_noise`, confidence: high)
- **Common duplicate patterns**:
  - RAW vs WIKI versions of the same note (e.g., `knowledge-ingestion-system`, `hermes-setup`, `cloudflare-network`)
  - Multi-path WIKI duplicates (e.g., `deck.md` appearing in `WIKI/apps/`, `WIKI/concepts/`, and `WIKI/services/`)
  - Identical `index.md` files across multiple WIKI categories
  - Near-duplicate OpenWebUI chat exports (e.g., `AionUi Chat Exchange` series)
- **Canonical confidence levels**: high, medium, low (user choice required for low-confidence suggestions)
- **Command flow**: `archive cleanup group 1` → `confirm archive` → archive executed

## Related
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[knowledge-cleanup-request-a247bbff-d697-4a97-8a17-1e56c851ba06]]
- [[merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--2f69dc4a-1e47-4de3-855b-d2df003e689e]]
- [[merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--d5dbc08e-5438-420f-9daf-0f235ae7ac8f]]

## Source
- RAW: [[RAW/openwebui/cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
