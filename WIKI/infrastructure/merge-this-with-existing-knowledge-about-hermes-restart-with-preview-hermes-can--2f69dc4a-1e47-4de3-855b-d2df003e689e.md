---
title: Openwebui Merge This With Existing Knowledge About Hermes Restart With Preview Hermes Can 2f69dc4a 1e47 4de3 855b D2df003e689e
source_raw: RAW/openwebui/merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--2f69dc4a-1e47-4de3-855b-d2df003e689e.md
compiled_wiki_path: WIKI/infrastructure/merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--2f69dc4a-1e47-4de3-855b-d2df003e689e.md
compiled_at: 2026-05-02T19:49:53.249Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, merge, this, with, existing, knowledge]
---

# Openwebui Merge This With Existing Knowledge About Hermes Restart With Preview Hermes Can 2f69dc4a 1e47 4de3 855b D2df003e689e

## Summary
After restarting the Hermes backend via PM2, you can quickly verify it is running by checking the process status with `pm2 status`.

## Key Concepts
- **Hermes** is the backend gateway for AiAgentNerd, managed by PM2.
- **PM2 `status` command** lists all managed processes and their current states (online, errored, stopped, etc.).
- Post‑restart verification prevents unnoticed failures: the restart command itself may succeed even if the process later crashes.

## Practical Use
- After running `pm2 restart hermes --update-env`, immediately issue:
  ```bash
  pm2 status
  ```
- Confirm that the `hermes` process shows `status: online`. If it is not online, check logs with `pm2 logs hermes`.

## Implementation Notes
- Run these commands on the server where Hermes is deployed (currently `nerd@nerd-server`).
- The PM2 process name (`hermes`) is case‑sensitive.
- Typical output includes pid, name, mode, status, uptime, cpu, and memory – look primarily at the **status** column.

## Related
- [[clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
- [[save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575]]
- [[knowledge-ingestion-system]]
- [[save-to-knowledge-skill]]
- [[knowledge-ingestion-system]]

## Source
- RAW: [[RAW/openwebui/merge-this-with-existing-knowledge-about-hermes-restart-with-preview-hermes-can--2f69dc4a-1e47-4de3-855b-d2df003e689e]]
