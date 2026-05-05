---
title: Openwebui Cleanup Knowledge 3a89446a 083e 41f8 8936 334f0e4c58cd
source_raw: RAW/openwebui/cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd.md
compiled_wiki_path: WIKI/architecture/cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd.md
compiled_at: 2026-05-05T08:22:42.809Z
type: system-note
tags: [aiagentnerd, compiled, architecture, cleanup, knowledge, 3a89446a, 083e, 41f8]
---

# Openwebui Cleanup Knowledge 3a89446a 083e 41f8 8936 334f0e4c58cd

## Summary
A knowledge-cleanup scan of the AiAgentNerd knowledge base identified 20 candidate groups containing duplicate, near-duplicate, or low-value files across `RAW` and `WIKI` directories. The system defaulted to report-only mode; one low-value group was archived after explicit operator confirmation. Remaining groups require manual review to reconcile canonical versions and archive redundant originals.

## Key Concepts
- **Knowledge Cleanup Scan**: automated deduplication analysis comparing filenames, titles, topics, and content overlap across raw and compiled wiki files.
- **Candidate Group**: a cluster of files flagged as duplicates or near-duplicates requiring resolution.
- **Canonical Selection Rules**: prefer RAW sources over compiled WIKI; prefer non-archived files; prefer best-category matches; prefer cleaner titles.
- **Low-Value Noise**: ephemeral content lacking system value (e.g., empty `new-chat` stubs) recommended for deletion or archiving.
- **Report-Only Mode**: default behavior that surfaces recommendations without modifying files until an operator confirms each action.

## Practical Use
- Use this report to guide manual deduplication of the knowledge base.
- Archive low-value noise immediately after review (e.g., empty chat stubs).
- For each duplicate group, verify the canonical suggestion; merge any unique content from duplicates into the canonical file, then archive the duplicate originals.
- Review low-confidence canonical suggestions carefully before merging, as some clusters contain overlapping pairwise comparisons with divergent recommendations.
- Reconcile the `deck` and AionUI chat-exchange clusters manually, since pairwise scans produced intermediate suggestions that consolidate into a single canonical only in the full-cluster analysis.

## Implementation Notes
- **Scan scope**: 20 groups detected across `RAW/openwebui`, `RAW/quarantine`, `RAW/architecture`, `RAW/setup`, `RAW/docs`, `RAW/aionui`, `RAW/inbox`, and multiple `WIKI/` categories.
- **Classification signals**: duplicate filenames, near-duplicate titles, similar topics, overlapping commands/endpoints/paths, and OpenWebUI filename penalties.
- **Actioned group**:
  - Group 1 (`low_value_noise`): `RAW/openwebui/new-chat-fba354d7-5e23-430f-a0de-89635cec202b.md` was archived successfully after operator confirmation.
- **Pending canonical selections** (high confidence unless noted):
  - `RAW/openwebui/roman-gladiator-fun-fact-3e49211f-16ba-4be9-ac9d-a02ef2ce0617.md`
  - `RAW/openwebui/vocabulary-fill-in-practice-f67d0798-14ad-4737-8865-7aeac8ab9903.md`
  - `RAW/architecture/knowledge-ingestion-system.md`
  - `RAW/setup/hermes-setup.md`
  - `RAW/docs/aiagentnerd-master-notes.md`
  - `RAW/architecture/mobile-ingestion-and-hermes-skill.md`
  - `RAW/architecture/cloudflare-network.md`
  - `RAW/concepts/deck.md` (consolidated from multi-way cluster)
  - `RAW/architecture/hermes-knowledge-ingestion-system.md`
  - `RAW/inbox/hermes-service-restart-and-troubleshooting.md`
  - `WIKI/architecture/index.md` (medium confidence; supersedes other `index.md` files)
  - AionUI chat exchanges: pairwise suggestions diverge; operator must select the canonical from `2026-04-30T09-33-08-023Z-7d152c30-ef2e-4ac0-9288-8bb570a37193.md`, `2026-04-30T09-34-03-702Z-97bba13e-8095-4f44-995d-1398af93b407.md`, `2026-04-30T09-34-15-091Z-4d760d59-a6b6-4af0-b0ef-5d2e6ffe86cf.md`, or `2026-04-30T09-34-36-567Z-d73099b8-3211-482e-9359-93eff9d39801.md`.
- **Recommended action pattern**: merge content from duplicates into the selected canonical, then archive the duplicate originals.

## Related
- [[cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[knowledge-cleanup-request-a247bbff-d697-4a97-8a17-1e56c851ba06]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]

## Source
- RAW: [[RAW/openwebui/cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
