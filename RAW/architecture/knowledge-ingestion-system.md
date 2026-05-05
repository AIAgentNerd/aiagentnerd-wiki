# Knowledge Ingestion Workflow (Operational) — AiAgentNerd

## Topics
- ingestion
- raw
- wiki
- hermes
- workflow
- automation

---

## Context

This workflow ensures that all valuable knowledge from chats, PDFs, and other sources becomes persistent, structured system knowledge.

Goal:
- No backlog
- High signal knowledge
- Immediate capture after work

---

## Core Workflow


Chat / Content
↓
Generate RAW (ChatGPT)
↓
Save RAW on server
↓
Compile via Hermes
↓
Git push
↓
Obsidian sync


---

## Step-by-Step Execution

### 1. Generate RAW

In ChatGPT:


Turn this into RAW


Result:
- Suggested filename
- Structured RAW content

---

### 2. Create RAW file on server

```bash
cat > ~/aiagentnerd-wiki/RAW/<category>/<filename>.md

Example:

cat > ~/aiagentnerd-wiki/RAW/chat/hermes-api-setup.md

Paste RAW content → then press:

CTRL + D
3. Compile into WIKI
curl -X POST http://localhost:3100/api/system-wiki/scan-and-compile \
  -H "Content-Type: application/json" \
  -d '{}'
4. Push to Git
cd ~/aiagentnerd-wiki
git add .
git commit -m "add <filename>"
git push
5. Sync in Obsidian (Laptop)
Open vault
Pull changes (or auto-sync)
Check WIKI output
Commands (Primary)
cat > ~/aiagentnerd-wiki/RAW/<category>/<filename>.md

curl -X POST http://localhost:3100/api/system-wiki/scan-and-compile \
  -H "Content-Type: application/json" \
  -d '{}'

cd ~/aiagentnerd-wiki
git add .
git commit -m "update"
git push
Commands (Alternatives)
Using nano editor
nano ~/aiagentnerd-wiki/RAW/<category>/<filename>.md
Handling Long Chats
Option A — Selective extraction (default)

Copy only:

steps
commands
errors
decisions
Option B — Chunking

Split chat into parts:

Part 1 → process
Part 2 → process
Part 3 → process

Then merge using merge prompt.

Option C — Dump RAW
cat > ~/aiagentnerd-wiki/RAW/chat/long-chat.md

Paste everything → refine later if needed.

Command Handling Strategy
Commands (Primary)
working version
matches current system
used successfully
Commands (Alternatives)
failed attempts
experimental versions
different environments
Decision

Always include:

Selected command
Reason
Example
Commands (Primary)
pm2 start server.js --name hermes
Commands (Alternatives)
node server.js
Decision
Selected: PM2 version
Why:
persistent process
production-ready
File Structure
RAW/
├── chat/
├── web/
├── setup/
├── architecture/
├── apps/
Rules
Do NOT edit WIKI files
Always edit RAW → recompile
Use clear filenames
Prefer structured RAW for important topics
Daily Operating Rule

If it took more than 5 minutes to figure out → create RAW

Batch Workflow (Optional)
Select 5–10 chats
Generate RAW files
Save all
Compile once
Decisions
Use manual file creation (no alias yet)
Use structured RAW for important knowledge
Use dump RAW for speed when needed
Use merge workflow for consolidation
Related
[[knowledge-system-wiki]]
[[knowledge-raw-to-wiki]]
[[memory-system-design]]
Raw Notes
Speed > perfection
Capture immediately after work
Canonical files created via merge

---
## Compiled Wiki
- WIKI: [[WIKI/architecture/knowledge-ingestion-system]]
- Last compiled: 2026-05-05T06:31:48.703Z
