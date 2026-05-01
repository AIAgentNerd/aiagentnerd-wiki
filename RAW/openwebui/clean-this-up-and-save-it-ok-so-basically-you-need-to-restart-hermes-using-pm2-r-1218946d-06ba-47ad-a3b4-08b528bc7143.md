# Clean this up and save it
ok so basically you need to restart hermes using pm2 restart hermes
then if it fails you check logs with pm2 logs hermes
also server runs on port 3100 and api endpoint is /api/wiki/ingest-raw

source: openwebui
openwebui_chat_id: 1218946d-06ba-47ad-a3b4-08b528bc7143
created_at: 1777645159
updated_at: 1777648461
exported_at: 2026-05-02T02:45:01.115646

---

## USER

Clean this up and save it
ok so basically you need to restart hermes using pm2 restart hermes
then if it fails you check logs with pm2 logs hermes
also server runs on port 3100 and api endpoint is /api/wiki/ingest-raw

## ASSISTANT

Saved to Knowledge.
Category: inbox
Filename: hermes-service-restart-and-troubleshooting.md
RAW path: /home/nerd/aiagentnerd-wiki/RAW/inbox/hermes-service-restart-and-troubleshooting.md
Compile: compiled=1, skipped=27, failed=0
Git: To github.com:AIAgentNerd/aiagentnerd-wiki.git
   f55c904..4c04974  main -> main

## USER

clean this up and svae it . Hermes runs on port 3100. Restart with pm2 restart hermes. Check logs with pm2 logs hermes.

## ASSISTANT

---
category: setup
filename: hermes-service-management.md
type: raw
---# Hermes Service Management

## Topics
- Hermes
- pm2
- service management
- port 3100

## Context
This source provides operational commands for managing the Hermes service, which runs on port 3100 and is managed via pm2. It also includes a note to clean up and save something (likely a file or configuration).

## Key Concepts
- Hermes runs on port 3100.
- pm2 is used for process management.
- Restart and log commands are available.

## Workflow / Steps
1. Restart Hermes: `pm2 restart hermes`
2. Check logs: `pm2 logs hermes`

## Commands

### Primary Commands
```bash
pm2 restart hermes
pm2 logs hermes
```

### Supporting Commands
```bash
# None captured.
```

## Important Details
- Hermes service listens on port 3100.
- Use pm2 for process control.

## Open Questions
- None captured.

---
## Compiled Wiki
- WIKI: [[WIKI/infrastructure/clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
- Last compiled: 2026-05-01T19:48:24.096Z
