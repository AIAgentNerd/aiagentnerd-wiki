---
title: Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68
source_raw: RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_wiki_path: WIKI/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68.md
compiled_at: 2026-05-09T17:35:19.351Z
type: system-note
tags: [aiagentnerd, compiled, uncategorized, knowledge, workflow, 9449977b, 1d49, 43b0]
---

# Openwebui Knowledge System Workflow 9449977b 1d49 43b0 B79f D135b85e0a68

## Summary
Operational reference for the AiAgentNerd knowledge ingestion and maintenance pipeline as exposed through the OpenWebUI chat interface. Documents the command vocabulary, preview-confirmation gate, merge workflows, cleanup agent behavior, and safety constraints that govern how raw input moves from capture to structured system memory.

## Key Concepts
- **Ingestion Pipeline**: Raw chat input → automatic structuring → preview → confirmation → storage in `WIKI/`
- **RAW / WIKI Duality**: Source material is captured into `RAW/`; compiled output is promoted to `WIKI/` with a `compiled_at` timestamp
- **Preview-Confirm-Save Gate**: All write operations require an explicit preview step and user confirmation; the pipeline does not currently expose a direct-save bypass
- **Cleanup Agent**: Maintenance process that scans the knowledge base for duplicates, near-duplicate topics, and low-value notes, grouping them with confidence scores and recommended actions
- **Canonical File**: Preferred target document when merging duplicates during cleanup
- **Fallback Behavior**: If automatic compilation fails, the system falls back to a safe raw capture preview rather than silently dropping or corrupting the input

## Practical Use
### Ingestion Commands
- `Clean this up and save it` — ingest and store after implicit compilation
- `Save this to knowledge with preview` — ingest with explicit preview step
- `Clean this up` — compile/clean only, do not persist
- `confirm` / `cancel` — approve or reject a pending preview

### Merge Workflows
- `Merge these` — combine multiple pasted chunks into one note
- `Merge this with existing knowledge about <topic> with preview` — topical merge against discovered candidates
- `Merge this with existing file <filename>.md with preview` — targeted merge into a specific file
- `confirm merge` / `cancel merge` — resolve a pending merge preview

### Content Splitting
- `Split this into multiple notes` — decompose large input into discrete notes

### Cleanup Commands
- `cleanup knowledge` — scan the entire knowledge base
- `cleanup knowledge about <topic>` — scan a scoped subset
- `merge cleanup group <n> into canonical with preview` — deduplicate a group into its canonical file
- `confirm cleanup merge` — approve a cleanup-driven merge
- `archive cleanup group <n>` — queue a group for archival
- `confirm archive` — approve archival
- `delete cleanup group <n>` — delete (restricted to high-confidence groupings only)
- `cancel cleanup` — abort the active cleanup session

### Daily Usage Pattern
1. **Capture**: `Clean this up and save it`
2. **Improve**: `Merge with existing knowledge about <topic>`
3. **Combine**: `Merge related ideas`

## Implementation Notes
- **Frontmatter Influence**: Users can prepend a metadata block with `category`, `filename`, and `type: raw` to guide routing and naming, but the system ultimately assigns taxonomy and final path.
- **Preview Expiration**: Previews are session-bound and can expire. If confirmation is delayed, the system responds with `No pending knowledge preview found. It may have expired; create a new preview first.`
- **No Direct-Save Bypass**: The internal compilation pipeline does not currently document a `--no-preview` flag or endpoint parameter to skip review. Adding one would require modifying the compilation service or CLI to accept a pre-approved flag.
- **Structured Output Schema**: Compiled notes are structured into `topics`, `context`, `key concepts`, `steps` (if procedural), `commands` (if operational), and `important details`.
- **Cleanup Output Format**: Returns grouped findings:
  - **duplicate group** — exact or near-exact matches
  - **similar topic group** — overlapping subject matter
  - **low-value group** — noisy or low-signal content
  Each group lists affected files, confidence scores, and recommended actions (`merge`, `archive`, `ignore`).
- **Safety Behaviors**:
  - No automatic deletions; every destructive action requires explicit confirmation
  - Archive is preferred over delete
  - Backups are created before changes
  - Delete actions are gated behind high-confidence thresholds

## Related
- [[knowledge-system-workflow-guide-af6c6ecf-58d0-42d7-ac3b-3766effa775c]]
- [[save-to-knowledge-skill]]
- [[hermes-knowledge-system-full-architecture]]
- [[save-to-knowledge-skill]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]

## Source
- RAW: [[RAW/openwebui/knowledge-system-workflow-9449977b-1d49-43b0-b79f-d135b85e0a68]]
