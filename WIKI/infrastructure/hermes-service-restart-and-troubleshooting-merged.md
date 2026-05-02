---
title: Inbox Hermes Service Restart And Troubleshooting Merged
source_raw: RAW/inbox/hermes-service-restart-and-troubleshooting-merged.md
compiled_wiki_path: WIKI/infrastructure/hermes-service-restart-and-troubleshooting-merged.md
compiled_at: 2026-05-02T10:42:09.799Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, hermes, service, restart, troubleshooting, merged]
---

# Inbox Hermes Service Restart And Troubleshooting Merged

## Summary
This note aggregates open follow-up questions regarding Hermes service restart and troubleshooting. It identifies gaps in documentation around PM2 resurrection, port verification, endpoint testing, and automatic startup configuration.

## Key Concepts
- **Hermes service** is managed by **PM2**.
- **Port 3100** is the designated listening port for the Hermes backend.
- The **`/api/wiki/ingest-raw`** endpoint is used for raw note ingestion testing.
- **Automatic restart on server reboot** requires PM2 startup hooks.

## Practical Use
The following tasks remain undocumented and must be added to complete the restart/troubleshooting workflow:
- Provide the exact **PM2 resurrect** and **start** commands that were omitted from the merge.
- **Verify Hermes is listening on port 3100** after a restart (specific command or check).
- **Test the `/api/wiki/ingest-raw` endpoint** easily (e.g., `curl` example).
- **Configure PM2 to automatically restart Hermes on server reboot** (startup script or `pm2 startup` instructions).

## Implementation Notes
- No concrete steps yet; these are open implementation tasks derived from missing documentation.

## Related
- [[hermes-service-restart-and-troubleshooting]]
- [[hermes-setup]]
- [[knowledge-ingestion-system]]
- [[mobile-ingestion-and-hermes-skill]]
- [[hermes-setup]]

## Source
- RAW: [[RAW/inbox/hermes-service-restart-and-troubleshooting-merged]]
