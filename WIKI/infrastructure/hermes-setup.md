---
title: Setup Hermes Setup
source_raw: RAW/setup/hermes-setup.md
compiled_wiki_path: WIKI/infrastructure/hermes-setup.md
compiled_at: 2026-04-30T10:02:42.733Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, hermes, setup, api, pm2, openrouter]
---

# Setup Hermes Setup

## Summary
Hermes is the backend gateway for AiAgentNerd. It serves as the central hub for LLM interactions via OpenRouter and runs as a persistent PM2 process on port 3100, enabling wiki compilation, chat routes, and automation logic.

## Key Concepts
- **Backend Gateway**: Hermes handles all LLM requests and routes for the AiAgentNerd system.
- **PM2 Process Manager**: The gateway is managed as a PM2 process named `hermes`, providing reliability and easy restart.
- **OpenRouter Integration**: All LLM calls go through OpenRouter, allowing model selection and routing.
- **Port 3100**: The API is exposed on localhost port 3100.
- **Workspace Awareness**: The process operates from `/home/nerd/aiagentnerd` and references the wiki at `/home/nerd/aiagentnerd-wiki`.

## Practical Use
- **Restart Hermes**:
  ```
  pm2 restart hermes --update-env
  ```
- **Monitor logs**:
  ```
  pm2 logs hermes
  ```
- **Verify service**: Check port 3100 is listening (`curl localhost:3100/health` or similar).
- **File system context**: Any relative paths inside Hermes resolv to `/home/nerd/aiagentnerd`.

## Implementation Notes
- **Installation directory**: `/home/nerd/aiagentnerd`
- **Wiki directory**: `/home/nerd/aiagentnerd-wiki`
- **PM2 process name**: `hermes`
- **API port**: `3100`
- **LLM provider**: OpenRouter (the gateway abstracts provider details behind the `/chat` and `/wiki-compile` endpoints)
- **Supported routes**:
  - `/chat` – standard LLM chat
  - `/wiki-compile` – triggers wiki document compilation
  - Additional automation endpoints as needed
- **Resilience**: PM2 ensures the process restarts on failure; environment variables can be updated via `--update-env`.

## Related
- [[hermes-setup]]
- [[deck]]
- [[acr-dashboard-ui-b5cd7aa5-335b-4342-8461-29717600d1fa]]
- [[acr-overview-da74bd9b-66f7-4705-a7f5-11c50645f812]]
- [[agent-control-room-acr-fb05e0f0-c846-45b2-9728-dd7bd55af8ca]]

## Source
- RAW: [[RAW/setup/hermes-setup]]
