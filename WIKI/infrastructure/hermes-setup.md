---
title: Hermes Setup
source_raw: RAW/hermes-setup.md
compiled_wiki_path: WIKI/infrastructure/hermes-setup.md
compiled_at: 2026-04-24T14:38:15.741Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, hermes, setup, api, pm2, openrouter]
---

# Hermes Setup

## Summary
Hermes is the backend gateway service for AiAgentNerd, managed by PM2 and listening on port 3100. It routes LLM requests through OpenRouter and handles wiki compilation, chat endpoints, and automation logic.

## Key Concepts
- PM2-managed Node.js backend process
- OpenRouter integration for LLM API calls
- Port 3100 API gateway
- Wiki compilation pipeline
- Chat and automation route handling

## Details
Hermes operates as the central backend gateway within the AiAgentNerd infrastructure. The service runs as a PM2 process named `hermes` and exposes its API on port 3100. It proxies or handles LLM requests via OpenRouter and supports core backend functions including wiki compilation, chat routes, and automation logic.

Key paths:
- Backend source: `/home/nerd/aiagentnerd`
- Wiki storage: `/home/nerd/aiagentnerd-wiki`

## Practical Notes
- Restart service: `pm2 restart hermes --update-env`
- View logs: `pm2 logs hermes`
- Ensure PM2 is running and the `hermes` process is registered in the ecosystem config
- API available internally on port 3100

## Source
- RAW: [[RAW/hermes-setup]]

## Related
- [[hermes-setup]]
- [[backlink-test]]
- [[cloudflare-network]]
- [[git-obsidian-setup]]
- [[Networking Ports and IPs]]
