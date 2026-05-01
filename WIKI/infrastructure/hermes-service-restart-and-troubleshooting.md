---
title: Inbox Hermes Service Restart And Troubleshooting
source_raw: RAW/inbox/hermes-service-restart-and-troubleshooting.md
compiled_wiki_path: WIKI/infrastructure/hermes-service-restart-and-troubleshooting.md
compiled_at: 2026-05-01T14:20:06.145Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, hermes, service, restart, troubleshooting, api]
---

# Inbox Hermes Service Restart And Troubleshooting

## Summary
Practical instructions for restarting the Hermes service via PM2, checking logs on failure, and verifying the API endpoint for raw wiki ingestion. This is a maintenance reference for the AiAgentNerd system operator.

## Key Concepts
- Hermes runs as a PM2-managed process on the nerd-server.
- The standard restart command is `pm2 restart hermes`.
- Failure investigation uses `pm2 logs hermes`.
- The service listens on port 3100 and exposes the `/api/wiki/ingest-raw` endpoint for raw note ingestion.

## Practical Use
- Restart Hermes after configuration changes, deployment, or when the service becomes unresponsive.
- If a restart results in an error or the service does not come up, immediately inspect the logs.
- Verify the API endpoint `http://localhost:3100/api/wiki/ingest-raw` is reachable after startup.

## Implementation Notes
- **PM2 process name**: `hermes`
- **Restart command**:
  ```bash
  pm2 restart hermes
  ```
- **Logs command**:
  ```bash
  pm2 logs hermes
  ```
- **Listening port**: `3100`
- **API endpoint**: `/api/wiki/ingest-raw` (full URL: `http://<server>:3100/api/wiki/ingest-raw`)

No further configuration steps are required; PM2 handles process resurrection and logs.

## Related
- [[hermes-setup]]
- [[knowledge-ingestion-system]]
- [[mobile-ingestion-and-hermes-skill]]
- [[hermes-setup]]
- [[deck]]

## Source
- RAW: [[RAW/inbox/hermes-service-restart-and-troubleshooting]]
