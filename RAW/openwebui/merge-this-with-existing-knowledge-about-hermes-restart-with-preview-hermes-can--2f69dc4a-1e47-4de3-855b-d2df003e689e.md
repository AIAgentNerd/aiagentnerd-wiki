# Merge this with existing knowledge about Hermes restart with preview  
Hermes can also be checked with pm2 status after restart.

source: openwebui
openwebui_chat_id: 2f69dc4a-1e47-4de3-855b-d2df003e689e
created_at: 1777723816
updated_at: 1777724027
exported_at: 2026-05-03T02:45:01.905326

---

## USER

Merge this with existing knowledge about Hermes restart with preview  
Hermes can also be checked with pm2 status after restart.

## ASSISTANT

Multiple possible merge targets found.
Reply with merge 1, select 1, or the exact filename.

[1] hermes-service-restart-and-troubleshooting.md
   Path: RAW/inbox/hermes-service-restart-and-troubleshooting.md
   Title: Hermes Service Restart and Troubleshooting
   Confidence: medium
   Match: keyword overlap 7
[2] hermes-setup.md
   Path: RAW/setup/hermes-setup.md
   Title: Hermes Setup
   Confidence: medium
   Match: category, keyword overlap 7
[3] mobile-ingestion-and-hermes-skill.md
   Path: RAW/architecture/mobile-ingestion-and-hermes-skill.md
   Title: Mobile Ingestion Workflow + Hermes “Save to Knowledge” Skill
   Confidence: low
   Match: keyword overlap 5
[4] hermes-knowledge-ingestion-system.md
   Path: RAW/architecture/hermes-knowledge-ingestion-system.md
   Title: Hermes Knowledge Inestion System
   Confidence: low
   Match: keyword overlap 3
[5] aiagentnerd-master-notes.md
   Path: RAW/docs/aiagentnerd-master-notes.md
   Title: 🧠 Rule to remember
   Confidence: medium
   Match: keyword overlap 9

## USER

merge 2

## ASSISTANT

---
category: setup
filename: hermes-setup-merged.md
type: raw
---

# Hermes Setup

Hermes is the backend gateway for AiAgentNerd. It runs through PM2 as the hermes process and listens on port 3100. It connects to OpenRouter for LLM calls and supports wiki compilation, chat routes, and automation logic.

## Important Details
- backend folder: `/home/nerd/aiagentnerd`
- wiki folder: `/home/nerd/aiagentnerd-wiki`
- process manager: PM2
- restart command: `pm2 restart hermes --update-env`
- logs command: `pm2 logs hermes`
- API port: 3100
- status check: `pm2 status`

## USER

merge 1

## ASSISTANT

No pending merge candidates. Please run a merge request first.

---
## Compiled Wiki
- WIKI: [[WIKI/infrastructure/merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--2f69dc4a-1e47-4de3-855b-d2df003e689e]]
- Last compiled: 2026-05-02T19:49:53.249Z
