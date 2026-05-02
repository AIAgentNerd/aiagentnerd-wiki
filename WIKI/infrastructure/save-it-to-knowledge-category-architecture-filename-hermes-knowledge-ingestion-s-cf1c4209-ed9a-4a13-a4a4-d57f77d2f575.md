---
title: Openwebui Save It To Knowledge Category Architecture Filename Hermes Knowledge Ingestion S Cf1c4209 Ed9a 4a13 A4a4 D57f77d2f575
source_raw: RAW/openwebui/save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575.md
compiled_wiki_path: WIKI/infrastructure/save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575.md
compiled_at: 2026-05-02T19:52:18.332Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, save, it, knowledge, category, architecture]
---

# Openwebui Save It To Knowledge Category Architecture Filename Hermes Knowledge Ingestion S Cf1c4209 Ed9a 4a13 A4a4 D57f77d2f575

## Summary
This note documents a real-world ingestion failure event where a user attempted to save a large RAW note (`hermes-knowledge-ingestion-system.md`) to the wiki. Multiple attempts failed due to model issues (empty responses, invalid split outputs, truncation). The note was eventually saved as a single truncated RAW file after the user explicitly requested a single-note save. This event highlights fragility in the multi-note splitting path and model reliability under large payloads.

## Key Concepts
- **Ingestion Pipeline**: SOURCE → Clean Up Source → RAW → Save to Knowledge → `/api/wiki/ingest-raw` → compile → Git push.
- **Multi-Note Splitting**: A handler that splits long sources into multiple RAW notes; failed repeatedly in this case.
- **Model Fallback**: The system attempted to use `deepseek/deepseek-v4-pro` for splitting, which returned empty content; no fallback to Qwen was observed for the split operation.
- **Truncation**: The model output was truncated (`finishReason: length`), causing the split to fail.
- **Single-Note Save**: The user eventually bypassed splitting and saved the note as a single truncated RAW file, which succeeded.

## Practical Use
- This event serves as a test case for ingestion system resilience.
- It reveals that the multi-note splitting path lacks robust fallback when the primary model fails.
- Operators should be aware that large notes may require manual intervention (e.g., splitting manually or saving as a single note) if the automatic split fails.
- The final successful save used a truncated version of the note, indicating that the system can accept incomplete content if the user forces a single-note save.

## Implementation Notes
- **Failure Sequence**:
  1. `Multi-note save failed: OpenRouter returned empty content for deepseek/deepseek-v4-pro`
  2. `Multi-note save failed: Split response did not include valid RAW notes` (multiple times)
  3. `Multi-note save failed: Model output was truncated. Please split the source into smaller chunks.`
- **Successful Save**: User sent a truncated version of the note with `Save this to knowledge` and explicit frontmatter; the system saved it as a single RAW file.
  - RAW path: `/home/nerd/aiagentnerd-wiki/RAW/architecture/hermes-knowledge-ingestion-system.md`
  - Compile result: `compiled=1, skipped=28, failed=0`
  - Git push: `ad0db78..516d78c main -> main`
- **Model Used for Split**: `deepseek/deepseek-v4-pro` (not the standard Kimi or Qwen). This model is not listed in the primary/secondary routing configuration, suggesting it was selected by the multi-note handler or OpenRouter default.
- **No Automatic Fallback**: The split handler did not fall back to Qwen when DeepSeek failed; it simply reported the error to the user.
- **Truncation Handling**: The system detected truncation and advised the user to split manually, but did not automatically retry with a different model or smaller chunk.

## Related
- [[clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
- [[save-to-knowledge-skill]]
- [[knowledge-ingestion-system]]
- [[knowledge-ingestion-system]]
- [[merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--2f69dc4a-1e47-4de3-855b-d2df003e689e]]

## Source
- RAW: [[RAW/openwebui/save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575]]
