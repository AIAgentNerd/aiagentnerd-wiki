---
title: Openwebui Cleanup Knowledge About Deck Deeec384 5ce3 477e 884a Aff13904a4ad
source_raw: RAW/openwebui/cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad.md
compiled_wiki_path: WIKI/architecture/cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad.md
compiled_at: 2026-05-05T06:55:35.302Z
type: system-note
tags: [aiagentnerd, compiled, architecture, cleanup, knowledge, about, deck, deeec384]
---

# Openwebui Cleanup Knowledge About Deck Deeec384 5ce3 477e 884a Aff13904a4ad

## Summary
Record of two automated knowledge-base cleanup scans—one targeting Deck documentation and one general wiki scan. Each pass identified 20 candidate duplicate groups across RAW and WIKI hierarchies, recommended canonical sources, and classified low-value noise. An attempted archive of Deck cleanup group 6 failed on confirmation with no pending action found.

## Key Concepts
- **Knowledge cleanup report**: automated deduplication scan across RAW and WIKI paths
- **Deck duplicates**: overlapping docs in `RAW/concepts/deck.md`, `WIKI/apps/deck.md`, `WIKI/concepts/deck.md`, and `WIKI/services/deck.md`
- **RAW source preference**: canonical selection rule preferring RAW sources over compiled WIKI notes
- **Low-value noise**: classification for chat exchanges and unneeded exports that should be deleted rather than merged
- **Failed archive action**: staged archive for group 6 did not persist; confirmation returned `No pending archive action found`

## Practical Use
- Use this log to guide manual deduplication of Deck and related system docs
- Canonical Deck source should be `RAW/concepts/deck.md` per system recommendation (high confidence)
- Group 6 archive (`WIKI/services/deck.md` into `WIKI/apps/deck.md`) failed and requires manual follow-up or re-run
- Merge other identified duplicates into their RAW canonicals and archive compiled copies

## Implementation Notes
- Cleanup tool ran in default **report-only** mode; no files were modified automatically
- **First pass** (`cleanup knowledge about Deck`): 20 candidate groups
- **Second pass** (`cleanup knowledge`): 20 candidate groups
- **Deck duplicate findings**:
  - Primary recommendation: keep `RAW/concepts/deck.md` as canonical (RAW preferred, category: concepts, confidence: high)
  - Group 6: `WIKI/apps/deck.md` vs `WIKI/services/deck.md` → recommend keeping `WIKI/apps/deck.md` (confidence: medium)
- **Archive failure sequence**:
  1. User: `archive cleanup group 6`
  2. Assistant: `Archive staged for cleanup group 6. Reply: confirm archive`
  3. User: `confirm archive`
  4. Assistant: `No pending archive action found`
- **Other high-confidence duplicates to resolve**:
  - `RAW/architecture/knowledge-ingestion-system.md` ← merge `WIKI/infrastructure/knowledge-ingestion-system.md`, `WIKI/architecture/knowledge-ingestion-system.md`
  - `RAW/setup/hermes-setup.md` ← merge `WIKI/infrastructure/hermes-setup.md`
  - `RAW/docs/aiagentnerd-master-notes.md` ← merge `WIKI/concepts/aiagentnerd-master-notes.md`
  - `RAW/architecture/mobile-ingestion-and-hermes-skill.md` ← merge `WIKI/infrastructure/mobile-ingestion-and-hermes-skill.md`
  - `RAW/architecture/cloudflare-network.md` ← merge `WIKI/infrastructure/cloudflare-network.md`
  - `RAW/architecture/hermes-knowledge-ingestion-system.md` ← merge `WIKI/services/hermes-knowledge-ingestion-system.md`
  - `RAW/inbox/hermes-service-restart-and-troubleshooting.md` ← merge `WIKI/infrastructure/hermes-service-restart-and-troubleshooting.md`
  - Category `index.md` files duplicated across `WIKI/agents/`, `WIKI/apps/`, `WIKI/architecture/`, `WIKI/concepts/`, `WIKI/infrastructure/`, `WIKI/services/`, `WIKI/workflows/` — second pass suggests `WIKI/architecture/index.md` as canonical
- **Low-value items flagged for deletion/archival** (do not merge):
  - `RAW/aionui/2026-04-30T09-33-08-023Z-7d152c30-ef2e-4ac0-9288-8bb570a37193.md`
  - `RAW/aionui/2026-04-30T09-34-03-702Z-97bba13e-8095-4f44-995d-1398af93b407.md`
  - `RAW/aionui/2026-04-30T09-34-15-091Z-4d760d59-a6b6-4af0-b0ef-5d2e6ffe86cf.md`
  - `RAW/aionui/2026-04-30T09-34-36-567Z-d73099b8-3211-482e-9359-93eff9d39801.md`
  - `RAW/openwebui/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504.md`
  - `RAW/openwebui/new-chat-fba354d7-5e23-430f-a0de-89635cec202b.md`
  - `RAW/openwebui/save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575.md`
  - `RAW/quarantine/openwebui-random/roman-gladiator-fun-fact-3e49211f-16ba-4be9-ac9d-a02ef2ce0617.md`
  - `RAW/quarantine/openwebui-random/vocabulary-fill-in-practice-f67d0798-14ad-4737-8865-7aeac8ab9903.md`

## Related
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
- [[knowledge-cleanup-request-a247bbff-d697-4a97-8a17-1e56c851ba06]]

## Source
- RAW: [[RAW/openwebui/cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
