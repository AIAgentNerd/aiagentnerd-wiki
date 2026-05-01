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
```

## Important Details
- Server runs on port 3100.
- API endpoint: `/api/wiki/ingest-raw`.

## Open Questions
- None captured.

---
## Compiled Wiki
- WIKI: [[WIKI/infrastructure/hermes-service-restart-and-troubleshooting]]
- Last compiled: 2026-05-01T14:20:06.145Z
