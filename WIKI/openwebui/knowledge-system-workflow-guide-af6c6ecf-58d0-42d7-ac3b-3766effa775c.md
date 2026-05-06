---
title: Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c
source_raw: RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c.md
compiled_at: 2026-05-06T15:04:24.939Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, af6c6ecf, 58d0, 42d7]
---

# Openwebui Knowledge System Workflow Guide Af6c6ecf 58d0 42d7 Ac3b 3766effa775c

## Summary
Operational guide for the AiAgentNerd knowledge ingestion, merge, and cleanup workflows. Describes how unstructured input is transformed into structured knowledge, the mandatory preview-confirm-save safety flow, and the cleanup agent’s deduplication and archival procedures.

## Key Concepts
- **Automatic ingestion**: accepts raw input (notes, transcripts, chat logs, ideas) and converts it into structured knowledge automatically
- **Structured output**: every entry is organized into topics, context, key concepts, steps, commands, and important details
- **Automatic organization**: system assigns a category, generates a filename, and routes the content to the correct storage location without manual filing
- **Merge workflow**: new information updates existing files rather than creating duplicates; knowledge evolves through iterative merges
- **Safety model**: all mutating operations follow preview → confirm → save; no automatic overwrites or deletions
- **Cleanup agent**: scans the knowledge base for duplicates, similar topics, and low-value notes; groups them for review with confidence scores and recommended actions (merge, archive, ignore)
- **Archive preference**: deletion is restricted to high-confidence cases; archive is the default cleanup action, with backups created before changes

## Practical Use
- **Ingestion commands**:
  - `Clean this up and save it` — process and store raw input
  - `Save this to knowledge with preview` — generate a preview before persisting
  - `Clean this up` — clean without saving
- **Merge commands**:
  - `Merge these` — combine multiple raw chunks into one entry
  - `Merge this with existing knowledge about <topic> with preview` — update a topic; if multiple files match, select by index (e.g., `merge 1`)
  - `Merge this with existing file <filename>.md with preview` — targeted merge into a specific file
  - `confirm merge` / `cancel merge` — finalize or abort
- **Split command**:
  - `Split this into multiple notes` — decompose large content into discrete entries
- **Cleanup commands**:
  - `cleanup knowledge` or `cleanup knowledge about <topic>` — initiate a scan
  - `merge cleanup group <N> into canonical with preview` — deduplicate a group into its canonical file
  - `archive cleanup group <N>` — archive a low-value group
  - `delete cleanup group <N>` — delete restricted to high-confidence cases only
  - `cancel cleanup` — abort the cleanup session
- **Confirmation commands**: `confirm`, `cancel`, `confirm archive`, `confirm cleanup merge`
- **Daily workflow**: capture → improve → combine
- **Operational guidance**:
  - Prefer merge over duplicate; always update instead of re-saving
  - Let the system decide categories
  - Use preview for important content
  - Think in topics, not files
  - Keep input raw and let the system handle cleanup

## Implementation Notes
- **Category routing**: when unspecified, inputs default to `inbox`; otherwise they route to assigned categories (e.g., `concepts`)
- **Filename generation**: derived from content title or topic (e.g., `aiagentnerd-knowledge-system-explainer-and-workflow.md`)
- **Raw capture fallback**: if automatic cleaning fails, the system stores a `type: raw` preview under the `inbox` category
- **Preview expiration**: knowledge previews are transient; delayed confirmation may require regeneration before saving
- **Cleanup group metadata**: each group includes file references, confidence score, and recommended action
- **Safety constraints**: no automatic deletion; archive preferred over delete; backups created before merge/archive; user confirmation required for all mutations

## Related
- [[knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
