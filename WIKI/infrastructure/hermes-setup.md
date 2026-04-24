---
title: Hermes Setup
source_raw: hermes-setup.md
compiled_at: 2026-04-24T14:15:08.447Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, hermes, setup, api, pm2, openrouter]
---

# Hermes Setup

## Summary
Hermes is the AiAgentNerd backend gateway. Managed by PM2 as the `hermes` process, it listens on port 3100 and proxies LLM requests to OpenRouter while handling wiki compilation, chat routes, and automation logic.

## Key Concepts
- **PM2-managed gateway**: Core backend process running under PM2
- **OpenRouter proxy**: LLM API calls routed through OpenRouter
- **Port 3100**: Internal API listener
- **Wiki compilation**: Backend service for processing wiki content
- **Chat and automation**: API routes for chat and automation logic

## Details
The application root is `/home/nerd/aiagentnerd`. Wiki content is maintained separately at `/home/nerd/aiagentnerd-wiki`.

## Practical Notes
- Restart service: `pm2 restart hermes --update-env`
- Tail logs: `pm2 logs hermes`
- Verify PM2 daemon is running before issuing process commands

## Related
- PM2 process management
- OpenRouter API configuration
- AiAgentNerd backend architecture
- Wiki compilation pipeline

## Source
hermes-setup.md
