---
title: Openwebui Clean This Up And Save It Ok So Basically You Need To Restart Hermes Using Pm2 R 1218946d 06ba 47ad A3b4 08b528bc7143
source_raw: RAW/openwebui/clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143.md
compiled_wiki_path: WIKI/infrastructure/clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143.md
compiled_at: 2026-05-01T19:48:24.096Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, clean, this, up, save, it]
---

# Openwebui Clean This Up And Save It Ok So Basically You Need To Restart Hermes Using Pm2 R 1218946d 06ba 47ad A3b4 08b528bc7143

## Summary
This note captures the essential operational commands for managing the Hermes service, which runs on port 3100 and is managed via pm2. It also documents the API endpoint used for raw wiki ingestion.

## Key Concepts
- Hermes service: the core backend process for AiAgentNerd
- pm2: process manager used to keep Hermes running and manage restarts
- Port 3100: the port on which Hermes listens for API requests
- `/api/wiki/ingest-raw`: the API endpoint for ingesting raw wiki content

## Practical Use
- Restart Hermes after configuration changes or crashes: `pm2 restart hermes`
- Monitor Hermes logs for errors or activity: `pm2 logs hermes`
- The API endpoint `/api/wiki/ingest-raw` is used to submit raw markdown notes for compilation into the system wiki

## Implementation Notes
- Hermes is managed as a pm2 process named `hermes`
- The server binds to port 3100
- The ingestion endpoint is a POST endpoint at `/api/wiki/ingest-raw` (exact request format not captured here)
- Use `pm2 restart hermes` to apply changes; if the service fails, inspect logs with `pm2 logs hermes`

## Related
- [[acr-dashboard-ui-b5cd7aa5-335b-4342-8461-29717600d1fa]]
- [[acr-overview-da74bd9b-66f7-4705-a7f5-11c50645f812]]
- [[agent-control-room-acr-fb05e0f0-c846-45b2-9728-dd7bd55af8ca]]
- [[aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504]]
- [[current-model-info-b2c3571b-712e-4f82-8396-34b87b7f16d7]]

## Source
- RAW: [[RAW/openwebui/clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
