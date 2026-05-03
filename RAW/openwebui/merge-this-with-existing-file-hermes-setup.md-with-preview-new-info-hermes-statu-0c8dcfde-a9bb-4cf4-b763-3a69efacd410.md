# Merge this with existing file hermes-setup.md with preview
New info:
Hermes status can be checked with pm2 status.

source: openwebui
openwebui_chat_id: 0c8dcfde-a9bb-4cf4-b763-3a69efacd410
created_at: 1777812793
updated_at: 1777812921
exported_at: 2026-05-04T02:45:01.581537

---

## USER

Merge this with existing file hermes-setup.md with preview
New info:
Hermes status can be checked with pm2 status.

## ASSISTANT

---
category: setup
filename: hermes-setup-merged.md
type: raw
---

# Hermes Setup

## Topics
- Hermes
- PM2
- OpenRouter
- Backend gateway
- Process management

## Context
Hermes is the backend gateway service for AiAgentNerd. It runs under PM2, listens on port 3100, and connects to OpenRouter for LLM calls. It supports wiki compilation, chat routes, and automation logic.

## Key Concepts
- Hermes exposes an API on port 3100
- Uses OpenRouter as the LLM backend
- Managed entirely via PM2 for process lifecycle
- Serves as the central integration point for the AiAgentNerd system

## Important Details
- Backend directory: `/home/nerd/aiagentnerd`
- Wiki directory: `/home/nerd/aiagentnerd-wiki`
- Process manager: PM2
- API port: 3100
- PM2 process name: `hermes`
- Restart command: `pm2 restart hermes --update-env`
- Logs command: `pm2 logs hermes`
- Status command: `pm2 status`

## Commands
```bash
pm2 restart hermes --update-env
pm2 logs hermes
pm2 status
```

---
## Compiled Wiki
- WIKI: [[WIKI/infrastructure/merge-this-with-existing-file-hermes-setup.md-with-preview-new-info-hermes-statu-0c8dcfde-a9bb-4cf4-b763-3a69efacd410]]
- Last compiled: 2026-05-03T19:56:41.173Z
