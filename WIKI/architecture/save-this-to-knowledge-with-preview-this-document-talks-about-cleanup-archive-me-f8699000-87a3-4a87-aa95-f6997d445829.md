---
title: Openwebui Save This To Knowledge With Preview This Document Talks About Cleanup Archive Me F8699000 87a3 4a87 Aa95 F6997d445829
source_raw: RAW/openwebui/save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829.md
compiled_wiki_path: WIKI/architecture/save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829.md
compiled_at: 2026-05-04T19:55:08.909Z
type: system-note
tags: [aiagentnerd, compiled, architecture, save, this, knowledge, with, preview]
---

# Openwebui Save This To Knowledge With Preview This Document Talks About Cleanup Archive Me F8699000 87a3 4a87 Aa95 F6997d445829

## Summary
An OpenWebUI chat log documenting an intent routing test and a knowledge ingestion pipeline failure. The test validates task-aware model routing and fallback behavior between `qwen/qwen-2.5-72b-instruct` and `moonshotai/kimi-k2.6`. A follow-up save attempt combining routing test structure with a cleanup/archive description failed during the RAW markdown cleanup step.

## Key Concepts
- Intent Routing Test
- Task-Aware Routing
- Specialist vs. Generalist Model Deployment
- Empty-Content Failure Mode
- `finishReason: length` Truncation
- Knowledge Ingestion Pipeline
- RAW Markdown Cleanup Validation

## Practical Use
- Validates that tasks tagged `wiki_compile`, `code`, `long_context`, and `background` route to the secondary specialist model
- Confirms automatic fallback to the primary model when the secondary returns empty content or truncates with `finishReason: length`
- Demonstrates a failure mode where the knowledge ingestion `Clean Up Source` step rejects malformed or invalid RAW markdown

## Implementation Notes
- **Source**: OpenWebUI chat export, ID `f8699000-87a3-4a87-aa95-f6997d445829`, exported `2026-05-05T02:45:01.528479`
- **Primary Model**: `qwen/qwen-2.5-72b-instruct` (generalist default and fallback target)
- **Secondary Model**: `moonshotai/kimi-k2.6` (specialist for complex and long-context tasks)
- **Routing Command**:
  ```sh
  python scripts/task_router.py --task_type=wiki_compile --model=moonshotai/kimi-k2.6
  ```
- **Fallback Command**:
  ```sh
  python scripts/task_router.py --task_type=wiki_compile --model=qwen/qwen-2.5-72b-instruct
  ```
- **Fallback Triggers**: Empty content from secondary model; `finishReason: length`
- **Pipeline Failure**: A second save attempt returned error `Clean Up Source returned invalid RAW markdown`, indicating the ingestion cleanup validator rejected the input
- **Decisions**:
  - Task-aware routing directs complex workloads to the more capable secondary model
  - Fallback mechanism provides operational resilience when the specialist model fails
  - `finishReason: length` is used as an explicit trigger for fallback invocation
- **Open Questions**:
  - How can fallback frequency be reduced?
  - Are there additional error conditions that should trigger fallback?
  - Can the secondary model be improved to handle complex tasks without failing?

## Related
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--2f69dc4a-1e47-4de3-855b-d2df003e689e]]
- [[merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--d5dbc08e-5438-420f-9daf-0f235ae7ac8f]]
- [[merge-this-with-existing-file-hermes-setup.md-with-preview-new-info-hermes-statu-0c8dcfde-a9bb-4cf4-b763-3a69efacd410]]
- [[clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]

## Source
- RAW: [[RAW/openwebui/save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
