---
title: Hermes Setup
source_raw: hermes-setup.md
compiled_at: 2026-04-24T14:25:44.113Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, hermes, setup, api, pm2, openrouter]
---

# Hermes Setup

## Summary

Hermes is the backend gateway service for AiAgentNerd, managed by PM2 and listening on port 3100. It routes LLM requests through OpenRouter and handles wiki compilation, chat endpoints, and automation logic.

## Key Concepts

- Backend gateway service for AiAgentNerd
- PM2-managed process (`hermes`)
- OpenRouter integration for LLM API calls
- Wiki compilation pipeline
- Chat and automation API routes
- Exposes REST API on port 3100

## Details

The Hermes service runs from `/home/nerd/aiagentnerd` and references the wiki repository at `/home/nerd/aiagentnerd-wiki`. It operates as a persistent PM2 process, exposing API endpoints on port 3100. The service proxies LLM requests to OpenRouter and supports three primary functional areas: wiki compilation, chat route handling, and backend automation logic.

## Practical Notes

- **Restart service:** `pm2 restart hermes --update-env`
- **View logs:** `pm2 logs hermes`
- **Backend path:** `/home/nerd/aiagentnerd`
- **Wiki path:** `/home/nerd/aiagentnerd-wiki`
- **API base:** `http://localhost:3100`

## Related

- PM2 process management
- OpenRouter API integration
- AiAgentNerd backend architecture
- Wiki compilation pipeline

## Source

hermes-setup.md
