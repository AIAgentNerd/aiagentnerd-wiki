---
title: Architecture Knowledge Ingestion System
source_raw: RAW/architecture/knowledge-ingestion-system.md
compiled_wiki_path: WIKI/architecture/knowledge-ingestion-system.md
compiled_at: 2026-05-05T06:31:48.703Z
type: system-note
tags: [aiagentnerd, compiled, architecture, knowledge, ingestion, git, api, hermes]
---

# Architecture Knowledge Ingestion System

## Summary
This note outlines the knowledge ingestion workflow for AiAgentNerd, ensuring that valuable information from chats, PDFs, and other sources is captured, structured, and integrated into the system wiki.

## Key Concepts
- **Ingestion**: Process of converting raw content into structured system knowledge.
- **RAW**: Unprocessed, structured content generated from various sources.
- **Wiki**: The internal technical wiki where structured knowledge is stored.
- **Hermes**: The system responsible for compiling RAW content into the wiki.
- **Automation**: Workflow steps to ensure consistent and timely knowledge capture.

## Practical Use
- **Generate RAW**: Use ChatGPT to convert unstructured content into structured RAW format.
- **Save RAW on Server**: Create RAW files on the server using the `cat` command.
- **Compile via Hermes**: Use the Hermes API to compile RAW content into the wiki.
- **Git Push**: Commit and push changes to the `aiagentnerd-wiki` repository.
- **Obsidian Sync**: Sync the updated wiki content in the Obsidian vault.

## Implementation Notes
### Step-by-Step Execution

1. **Generate RAW**
   - In ChatGPT, use the prompt "Turn this into RAW" to generate structured RAW content.
   - Example:
     ```bash
     cat > ~/aiagentnerd-wiki/RAW/chat/hermes-api-setup.md
     ```

2. **Create RAW file on server**
   - Use the `cat` command to create and save RAW content to the appropriate directory.
   - Example:
     ```bash
     cat > ~/aiagentnerd-wiki/RAW/chat/hermes-api-setup.md
     ```
   - Press `CTRL + D` to save the content.

3. **Compile into WIKI**
   - Use the Hermes API to compile RAW content into the wiki.
   - Example:
     ```bash
     curl -X POST http://localhost:3100/api/system-wiki/scan-and-compile \
       -H "Content-Type: application/json" \
       -d '{}'
     ```

4. **Push to Git**
   - Commit and push changes to the `aiagentnerd-wiki` repository.
   - Example:
     ```bash
     cd ~/aiagentnerd-wiki
     git add .
     git commit -m "add hermes-api-setup.md"
     git push
     ```

5. **Sync in Obsidian (Laptop)**
   - Open the Obsidian vault and pull the latest changes.
   - Check the WIKI output to ensure the content is correctly compiled.

### Handling Long Chats
- **Selective Extraction**: Copy only essential steps, commands, errors, and decisions.
- **Chunking**: Split long chats into manageable parts and process each part separately.
- **Dump RAW**: Save the entire chat and refine it later if needed.

### Command Handling Strategy
- **Primary Commands**: Use commands that are working, match the current system, and have been used successfully.
- **Alternative Commands**: Document failed attempts, experimental versions, and commands for different environments.
- **Decision**: Always include the selected command and the reason for the selection.
  - Example:
    ```bash
    Commands (Primary)
    pm2 start server.js --name hermes
    Commands (Alternatives)
    node server.js
    Decision
    Selected: PM2 version
    Why:
    persistent process
    production-ready
    ```

### File Structure
- **RAW Directory**:
  - `RAW/`
    - `chat/`
    - `web/`
    - `setup/`
    - `architecture/`
    - `apps/`

### Rules
- Do not edit WIKI files directly; always edit RAW files and recompile.
- Use clear and descriptive filenames.
- Prefer structured RAW for important topics.
- Create RAW files for any task that took more than 5 minutes to figure out.

### Batch Workflow (Optional)
- Select 5-10 chats, generate RAW files, save all, and compile once.

## Related
- [[knowledge-ingestion-system]]
- [[hermes-knowledge-ingestion-system]]
- [[hermes-knowledge-ingestion-system]]
- [[hermes-knowledge-system-full-architecture]]
- [[mobile-ingestion-and-hermes-skill]]

## Source
- RAW: [[RAW/architecture/knowledge-ingestion-system]]
