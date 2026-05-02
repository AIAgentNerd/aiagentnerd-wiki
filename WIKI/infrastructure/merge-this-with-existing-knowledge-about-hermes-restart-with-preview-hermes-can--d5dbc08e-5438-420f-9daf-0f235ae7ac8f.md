---
title: Openwebui Merge This With Existing Knowledge About Hermes Restart With Preview Hermes Can D5dbc08e 5438 420f 9daf 0f235ae7ac8f
source_raw: RAW/openwebui/merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--d5dbc08e-5438-420f-9daf-0f235ae7ac8f.md
compiled_wiki_path: WIKI/infrastructure/merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--d5dbc08e-5438-420f-9daf-0f235ae7ac8f.md
compiled_at: 2026-05-02T19:50:31.638Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, merge, this, with, existing, knowledge]
---

# Openwebui Merge This With Existing Knowledge About Hermes Restart With Preview Hermes Can D5dbc08e 5438 420f 9daf 0f235ae7ac8f

## Summary
This note documents the operational procedures for restarting and troubleshooting the Hermes service using PM2. It covers the essential commands, the server's listen port and API endpoint, and the recommended verification step after a restart.

## Key Concepts
- Hermes is managed via PM2 process manager
- Restart command: `pm2 restart hermes`
- Verification after restart: `pm2 status`
- Log inspection: `pm2 logs hermes`
- Hermes listens on port 3100
- The raw ingestion API endpoint is `/api/wiki/ingest-raw`

## Practical Use
- Operators use these commands to restart Hermes when needed and to quickly diagnose failures
- After a restart, always run `pm2 status` to confirm the process came back up correctly

## Implementation Notes
- Hermes service name in PM2: `hermes`
- Restart: `pm2 restart hermes`
- Check logs: `pm2 logs hermes`
- Verify status: `pm2 status`
- Server configuration:
  - Port: `3100`
  - Ingest endpoint: `/api/wiki/ingest-raw`

## Related
- [[merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--2f69dc4a-1e47-4de3-855b-d2df003e689e]]
- [[clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
- [[save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575]]
- [[knowledge-ingestion-system]]
- [[save-to-knowledge-skill]]

## Source
- RAW: [[RAW/openwebui/merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--d5dbc08e-5438-420f-9daf-0f235ae7ac8f]]
