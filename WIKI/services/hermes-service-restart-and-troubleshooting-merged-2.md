---
title: Inbox Hermes Service Restart And Troubleshooting Merged 2
source_raw: RAW/inbox/hermes-service-restart-and-troubleshooting-merged-2.md
compiled_wiki_path: WIKI/services/hermes-service-restart-and-troubleshooting-merged-2.md
compiled_at: 2026-05-02T10:48:38.600Z
type: system-note
tags: [aiagentnerd, compiled, services, hermes, service, restart, troubleshooting, merged]
---

# Inbox Hermes Service Restart And Troubleshooting Merged 2

## Summary
This note documents procedures for restarting and troubleshooting the Hermes service, which is managed via pm2. It covers checking service status, configuring automatic restarts on failure, viewing recent logs, and ensuring Hermes starts automatically after a server reboot.

## Key Concepts
- Hermes runs as a pm2-managed process.
- `pm2 status` provides the current state of all managed processes.
- Automatic restart can be configured to recover from crashes without manual intervention.
- Logs are accessible via `pm2 logs` and stored in `~/.pm2/logs/`.
- A startup script (`pm2 startup`) ensures Hermes is relaunched on system boot.

## Practical Use
- Check if Hermes is running: `pm2 status`
- View recent Hermes logs (last 50 lines): `pm2 logs hermes --lines 50`
- Restart Hermes manually: `pm2 restart hermes`
- Stop Hermes: `pm2 stop hermes`
- Enable automatic restart on crash: ensure the process configuration includes `autorestart: true` and appropriate `max_restarts` and `restart_delay` values.
- Make Hermes start on server reboot: run `pm2 startup` (follow the printed command) then `pm2 save` to persist the current process list.

## Implementation Notes
- pm2 process file (e.g., `ecosystem.config.js`) should include:
  ```js
  {
    name: 'hermes',
    script: 'path/to/hermes.js',
    autorestart: true,
    max_restarts: 10,
    restart_delay: 5000,
    watch: false
  }
  ```
- Log files: `~/.pm2/logs/hermes-out.log` (stdout) and `~/.pm2/logs/hermes-error.log` (stderr).
- To tail logs continuously: `pm2 logs hermes`
- To check only error logs: `pm2 logs hermes --err`
- After a crash, pm2 will attempt to restart up to `max_restarts` times within the `restart_delay` window; if exceeded, the process is stopped.

## Related
- [[hermes-service-restart-and-troubleshooting-merged]]
- [[hermes-service-restart-and-troubleshooting]]
- [[hermes-setup]]
- [[deck]]
- [[hermes-knowledge-ingestion-system]]

## Source
- RAW: [[RAW/inbox/hermes-service-restart-and-troubleshooting-merged-2]]
