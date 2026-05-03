---
title: Openwebui Merge This With Existing File Hermes Setup.Md With Preview New Info Hermes Statu 0c8dcfde A9bb 4cf4 B763 3a69efacd410
source_raw: RAW/openwebui/merge-this-with-existing-file-hermes-setup.md-with-preview-new-info-hermes-statu-0c8dcfde-a9bb-4cf4-b763-3a69efacd410.md
compiled_wiki_path: WIKI/infrastructure/merge-this-with-existing-file-hermes-setup.md-with-preview-new-info-hermes-statu-0c8dcfde-a9bb-4cf4-b763-3a69efacd410.md
compiled_at: 2026-05-03T19:56:41.173Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, merge, this, with, existing, hermes]
---

# Openwebui Merge This With Existing File Hermes Setup.Md With Preview New Info Hermes Statu 0c8dcfde A9bb 4cf4 B763 3a69efacd410

## Summary
This note merges new information with the existing `hermes-setup.md` file. It provides an updated overview of the Hermes backend gateway service, including how to check its status using PM2.

## Key Concepts
- **Hermes**: The backend gateway service for AiAgentNerd.
- **PM2**: The process manager used to manage Hermes.
- **OpenRouter**: The LLM backend used by Hermes.
- **API Port**: Hermes exposes an API on port 3100.
- **Process Management**: Hermes is managed entirely via PM2 for process lifecycle.

## Practical Use
- **Checking Hermes Status**: Use the `pm2 status` command to check the status of the Hermes service.
- **Restarting Hermes**: Use the `pm2 restart hermes --update-env` command to restart the Hermes service with updated environment variables.
- **Viewing Logs**: Use the `pm2 logs hermes` command to view the logs of the Hermes service.

## Implementation Notes
- **Backend Directory**: `/home/nerd/aiagentnerd`
- **Wiki Directory**: `/home/nerd/aiagentnerd-wiki`
- **API Port**: 3100
- **PM2 Process Name**: `hermes`
- **Commands**:
  ```bash
  pm2 restart hermes --update-env
  pm2 logs hermes
  pm2 status
  ```

## Related
- [[merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--2f69dc4a-1e47-4de3-855b-d2df003e689e]]
- [[merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--d5dbc08e-5438-420f-9daf-0f235ae7ac8f]]
- [[clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[hermes-service-restart-and-troubleshooting-merged]]

## Source
- RAW: [[RAW/openwebui/merge-this-with-existing-file-hermes-setup.md-with-preview-new-info-hermes-statu-0c8dcfde-a9bb-4cf4-b763-3a69efacd410]]
