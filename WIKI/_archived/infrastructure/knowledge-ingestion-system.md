---
title: Architecture Knowledge Ingestion System
source_raw: RAW/architecture/knowledge-ingestion-system.md
compiled_wiki_path: WIKI/infrastructure/knowledge-ingestion-system.md
compiled_at: 2026-04-30T16:01:10.207Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, knowledge, ingestion, git, api, hermes]
status: archived
archived_at: 2026-05-05T06:31:48.717Z
reclassified_to: architecture/knowledge-ingestion-system.md
---

# Architecture Knowledge Ingestion System

## Summary
The knowledge ingestion workflow converts valuable insights from chats, PDFs, and other sources into persistent, structured system knowledge for the AiAgentNerd wiki. It follows a pipeline: capture content → generate a RAW note → save it to the `RAW/` folder on the server → compile it into a clean WIKI note via Hermes → push to Git → sync to Obsidian. The goal is to eliminate backlog and ensure no knowledge is lost, especially from interactions that take more than a few minutes to figure out.

## Key Concepts
- **RAW as source of truth**: All editing happens in the `RAW/` folder; WIKI files must never be edited directly.
- **Compile step**: Hermes processes RAW notes into polished, structured WIKI notes via the `scan-and-compile` API.
- **Git-driven sync**: The wiki is stored in a Git repository; pushing changes makes them available for Obsidian.
- **Category-based filing**: RAW files are placed in subdirectories like `chat/`, `web/`, `setup/`, `architecture/`, `apps/`.
- **5‑minute rule**: If something took more than 5 minutes to figure out, immediately create a RAW note.
- **Batch processing**: Multiple RAW files can be created at once and compiled in a single API call.
- **Long‑chat handling**: Large conversations can be captured selectively (key steps, commands, errors, decisions) or chunked and merged.

## Practical Use
**End‑to‑end ingestion flow:**
1. In ChatGPT, produce structured RAW content (suggested filename + content).
2. On the Nerd server, create the RAW file:
   ```bash
   cat > ~/aiagentnerd-wiki/RAW/<category>/<filename>.md
   ```
   Paste content, then press `Ctrl+D` to save.
3. Trigger compilation via Hermes:
   ```bash
   curl -X POST http://localhost:3100/api/system-wiki/scan-and-compile \
     -H "Content-Type: application/json" \
     -d '{}'
   ```
4. Push to the Git repository:
   ```bash
   cd ~/aiagentnerd-wiki
   git add .
   git commit -m "add <filename>"
   git push
   ```
5. Open the Obsidian vault and pull changes (or rely on auto‑sync) to see the compiled WIKI output.

**Alternative file creation** uses `nano` instead of `cat`.

**Handling large conversations:**
- **Selective extraction**: Copy only steps, commands, errors, and decisions.
- **Chunking**: Split into parts, process each, then merge using a merge prompt.
- **Dump RAW**: Capture everything in one file and refine later.

**Command handling strategy**: Always document the working command as “Commands (Primary)”, any failed/experimental variants as “Commands (Alternatives)”, and include the reason for the chosen command.

## Implementation Notes
- **File structure**:
  ```
  RAW/
  ├── chat/
  ├── web/
  ├── setup/
  ├── architecture/
  ├── apps/
  ```
- **API endpoint**: `POST http://localhost:3100/api/system-wiki/scan-and-compile` (Hermes) triggers the compile process.
- **Git repository**: `~/aiagentnerd-wiki` on the Nerd server.
- **Obsidian sync**: The vault pulls changes after Git push; ensure the vault’s remote points to the same repository.
- **Rule enforcement**: Never edit a WIKI file directly. All changes must flow through RAW → compile.
- **Daily operating rule**: “If it took more than 5 minutes to figure out → create RAW.”
- **Batch workflow**: Create multiple RAW files, then run a single compile command to process all at once.

## Related
- [[hermes-setup]]
- [[knowledge-ingestion-system]]
- [[git-obsidian-setup]]
- [[deck]]
- [[acr-dashboard-ui-b5cd7aa5-335b-4342-8461-29717600d1fa]]

## Source
- RAW: [[RAW/architecture/knowledge-ingestion-system]]
