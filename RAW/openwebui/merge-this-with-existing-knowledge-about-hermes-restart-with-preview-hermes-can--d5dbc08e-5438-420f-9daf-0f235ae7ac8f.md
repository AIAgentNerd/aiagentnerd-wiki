# Merge this with existing knowledge about Hermes restart with preview  
Hermes can also be checked with pm2 status after restart.

source: openwebui
openwebui_chat_id: d5dbc08e-5438-420f-9daf-0f235ae7ac8f
created_at: 1777724326
updated_at: 1777724368
exported_at: 2026-05-03T02:45:01.905435

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

merge 1

## ASSISTANT

---
category: inbox
filename: hermes-service-restart-and-troubleshooting-merged-3.md
type: raw
---

# Hermes Service Restart and Troubleshooting

## Topics
- Hermes
- PM2
- Server Configuration

## Context
Brief instructions for restarting the Hermes service using PM2, checking logs on failure, and noting the server's port and API endpoint.

## Key Concepts
- Hermes is managed via PM2 process manager.
- Restart command: `pm2 restart hermes`.
- Log inspection command: `pm2 logs hermes`.
- Server listens on port 3100.
- API endpoint for raw ingestion: `/api/wiki/ingest-raw`.

## Workflow / Steps
1. Restart Hermes using `pm2 restart hermes`.
2. If the restart fails, check logs with `pm2 logs hermes`.

## Commands

### Primary Commands
```bash
pm2 restart hermes
```

### Supporting Commands
```bash
pm2 logs hermes
pm2 status
```

## Important Details
- Server runs on port 3100.
- API endpoint: `/api/wiki/ingest-raw`.
- After restart, verify Hermes status with `pm2 status`.

## Open Questions

---
## Compiled Wiki
- WIKI: [[WIKI/infrastructure/merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--d5dbc08e-5438-420f-9daf-0f235ae7ac8f]]
- Last compiled: 2026-05-02T19:50:31.638Z
