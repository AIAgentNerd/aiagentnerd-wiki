---
title: Openwebui Merge This With Existing Knowledge About Hermes Restart With Preview Hermes Can D5dbc08e 5438 420f 9daf 0f235ae7ac8f
source_raw: RAW/openwebui/merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--d5dbc08e-5438-420f-9daf-0f235ae7ac8f.md
compiled_wiki_path: WIKI/infrastructure/merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--d5dbc08e-5438-420f-9daf-0f235ae7ac8f.md
compiled_at: 2026-05-03T19:58:32.936Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, merge, this, with, existing, knowledge]
---

# Openwebui Merge This With Existing Knowledge About Hermes Restart With Preview Hermes Can D5dbc08e 5438 420f 9daf 0f235ae7ac8f

## Summary
This note documents the operational procedure for restarting the Hermes service using PM2, verifying process status after restart, and inspecting logs when failures occur. It also records the server's listening port and the raw wiki ingestion API endpoint.

## Key Concepts
- **PM2 Process Management**: Hermes runs as a managed PM2 process.
- **Service Restart**: Triggered with `pm2 restart hermes`.
- **Log Inspection**: Use `pm2 logs hermes` to review startup or runtime errors.
- **Status Verification**: Confirm process health after restart with `pm2 status`.
- **Server Port**: Hermes listens on port `3100`.
- **Raw Ingestion Endpoint**: `/api/wiki/ingest-raw` accepts raw content for the wiki ingestion pipeline.

## Practical Use
- Restart the Hermes service after deployments or configuration changes using `pm2 restart hermes`.
- If the service fails to start or behaves unexpectedly after restart, diagnose immediately with `pm2 logs hermes`.
- Verify the process is online and stable post-restart using `pm2 status`.
- Submit raw markdown notes to the ingestion pipeline via `POST /api/wiki/ingest-raw` on port `3100`.

## Implementation Notes
- **Port**: `3100`
- **API Route**: `/api/wiki/ingest-raw`
- **Process Manager**: PM2
- **Command Reference**:
  ```bash
  pm2 restart hermes
  pm2 logs hermes
  pm2 status
  ```
- Always check `pm2 status` after a restart to confirm the process is online and not in an errored or stopped state.

## Related
- [[merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--2f69dc4a-1e47-4de3-855b-d2df003e689e]]
- [[merge-this-with-existing-file-hermes-setup.md-with-preview-new-info-hermes-statu-0c8dcfde-a9bb-4cf4-b763-3a69efacd410]]
- [[clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]

## Source
- RAW: [[RAW/openwebui/merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--d5dbc08e-5438-420f-9daf-0f235ae7ac8f]]
