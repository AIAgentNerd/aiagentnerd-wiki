---
title: Docs Aiagentnerd Master Notes
source_raw: RAW/docs/aiagentnerd-master-notes.md
compiled_wiki_path: WIKI/architecture/aiagentnerd-master-notes.md
compiled_at: 2026-05-05T06:37:31.469Z
type: system-note
tags: [aiagentnerd, compiled, architecture, master, cloudflare, networking, ssh, git]
---

# Docs Aiagentnerd Master Notes

## Summary
This note outlines the architecture and workflow for setting up and maintaining an Obsidian-based knowledge system for the AiAgentNerd project. It covers the structure of the Obsidian vault, the process of converting raw content into structured wiki notes, and the integration of this system with Hermes for automated knowledge management.

## Key Concepts
- **Obsidian Vault**: The central repository for structured knowledge, organized into `raw/` and `wiki/` folders.
- **Raw vs Wiki**: `raw/` stores unprocessed content, while `wiki/` contains cleaned, structured notes.
- **Core Memory**: A small, always-injected memory block for essential project facts.
- **Operating Rules**: Behavioral guidelines and system conventions for Hermes.
- **Selective Wiki Retrieval**: Hermes retrieves only relevant wiki notes for context.
- **Session Recall**: Historical context from past sessions, used as a fallback.
- **Memory Builder**: A function that assembles prompt context from different memory layers.
- **Router**: A classifier that decides which memory layer to use based on the task.
- **Writeback Layer**: Hermes can write new structured notes back to the wiki when useful.

## Practical Use
- **Folder Structure**:
  - `raw/`: Stores unprocessed content.
  - `wiki/`: Contains structured, reusable knowledge.
  - `index.md`: Navigation system for the wiki.
  - `log.md`: Activity and history log.
- **Note Structure**:
  - Each note follows a standard template with sections like `Key Insight`, `What it is`, `Mental Model`, `Setup / Steps`, `Why it matters`, and `Connections`.
- **Git Sync**:
  - Local changes are committed and pushed to GitHub.
  - The server pulls changes to keep the wiki in sync.
- **Hermes Integration**:
  - Hermes reads from the `wiki/` folder and can write back new notes.
  - The `loadWiki` function in `server.js` loads relevant wiki content into Hermes prompts.
- **Document Updates**:
  - Update the existing raw file and track versions.
  - Only update relevant wiki notes when changes are made.

## Implementation Notes
- **Core Memory**:
  - Stored in `wiki/agents/core-memory.md`.
  - Injected into every prompt to provide essential project facts.
- **Operating Rules**:
  - Defined in `wiki/agents/operating-rules.md` and `wiki/agents/agent-roles.md`.
  - Injected into every prompt to enforce behavior and conventions.
- **Selective Wiki Retrieval**:
  - Hermes retrieves only relevant notes based on the task.
  - Example: For a question about the X Post App, Hermes retrieves `wiki/apps/x-post-app.md`.
- **Session Recall**:
  - Used for historical context when the wiki does not contain the required information.
- **Memory Builder**:
  - Assembles prompt context from core memory, operating rules, and relevant wiki notes.
- **Router**:
  - Decides which memory layer to use based on the task type.
- **Writeback Layer**:
  - Hermes can write new structured notes to the wiki, but only for durable knowledge.
- **Git Setup**:
  - Initialize the Obsidian vault as a Git repository.
  - Sync changes between the laptop and server using Git.
- **Document Conversion**:
  - Convert Word files to Markdown and store in `raw/docs/`.
  - Process and integrate into the wiki as structured notes.

## Related
- [[cloudflare-network]]
- [[cloudflare-network]]
- [[ssh-ports]]
- [[knowledge-ingestion-system]]
- [[mobile-ingestion-and-hermes-skill]]

## Source
- RAW: [[RAW/docs/aiagentnerd-master-notes]]
