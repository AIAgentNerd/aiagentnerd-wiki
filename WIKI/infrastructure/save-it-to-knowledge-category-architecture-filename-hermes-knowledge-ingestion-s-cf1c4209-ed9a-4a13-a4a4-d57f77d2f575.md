---
title: Openwebui Save It To Knowledge Category Architecture Filename Hermes Knowledge Ingestion S Cf1c4209 Ed9a 4a13 A4a4 D57f77d2f575
source_raw: RAW/openwebui/save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575.md
compiled_wiki_path: WIKI/infrastructure/save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575.md
compiled_at: 2026-05-03T20:09:28.322Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, save, it, knowledge, category, architecture]
---

# Openwebui Save It To Knowledge Category Architecture Filename Hermes Knowledge Ingestion S Cf1c4209 Ed9a 4a13 A4a4 D57f77d2f575

## Summary
The Hermes Knowledge Ingestion System is an internal AiAgentNerd workflow that converts messy pasted sources—chat logs, transcripts, notes, or copied text—into structured RAW markdown, compiles them into clean WIKI notes, and pushes changes to Git for Obsidian sync. It is exposed through Open WebUI via the **Clean Up Source** and **Save to Knowledge** skills, with support for preview mode, automatic category routing, and multi-note splitting. A Telegram ingestion webhook was implemented but is currently paused because Cloudflare Access blocks Telegram from reaching `hermes.aiagentnerd.com`.

## Key Concepts
- **SOURCE → RAW → WIKI Pipeline**: Messy input is cleaned into structured RAW markdown, then compiled into reusable WIKI knowledge.
- **Clean Up Source Skill**: Converts messy pasted text into structured RAW markdown without saving or compiling.
- **Save to Knowledge Skill**: Saves structured RAW via the ingest endpoint, triggers compilation, Git push, and Obsidian sync.
- **Preview Mode**: Stages a pending preview for user confirmation before ingestion; previews expire after 30 minutes.
- **Category Auto-Routing**: Infers category from content (allowed: `chat`, `web`, `setup`, `architecture`, `apps`, `ideas`, `inbox`) with fallback to `inbox`.
- **Multi-Note Splitting**: Splits long or multi-topic sources into separate focused RAW notes with batch preview and confirmation.
- **Telegram Ingestion**: Paused webhook bot; blocked by Cloudflare Access on the main Hermes domain.

## Practical Use
- **Clean only**: Say *“Clean this up”* → Hermes returns structured RAW, no save.
- **Save structured RAW**: Say *“Save this to knowledge”* with pasted RAW → saves, compiles, pushes.
- **Clean and save**: Say *“Clean this up and save it”* → chains cleanup then ingestion automatically.
- **Preview workflow**: Add *“with preview”* to stage the ingestion, then confirm with `confirm save` or abort with `cancel`.
- **Multi-note workflow**: Say *“Save this to knowledge with preview. Split into multiple notes if needed.”* then `confirm save` to ingest the batch.
- **Payload limits**: If you hit `PayloadTooLargeError`, split the source into smaller chunks (Express limit is 10 MB).
- **After code changes**: Always restart Hermes after modifying `server.js`. Validate first with `node --check server.js`.

## Implementation Notes
- **Ingest RAW Endpoint**: `POST /api/wiki/ingest-raw`
  - Validates category, filename, and non-empty markdown content.
  - Sanitizes filename (blocks slashes and `..`); writes only under `RAW/<category>/`.
  - Supports `overwrite:true` and `dryRun:true`.
  - Calls `/api/system-wiki/scan-and-compile` after saving.
  - Uses `execFile` for Git commands; pushes to `github.com:AIAgentNerd/aiagentnerd-wiki.git`.
  - Appends JSONL events to `/home/nerd/aiagentnerd-system/logs/ingestion.log`.
- **Skill Handler Order**:
  1. `handlePendingIngestionConfirmation`
  2. `handleMultiNoteIngestionSkill`
  3. `handleCleanUpSourceSkill`
  4. `handleSaveToKnowledgeSkill`
  5. Normal LLM flow
- **Save to Knowledge Skill Behavior**:
  - Detects explicit save phrases and ignores negated requests (e.g., *“don’t save to knowledge”*).
  - Extracts fenced or pasted RAW markdown.
  - Infers safe kebab-case `.md` filename.
  - Rejects messy/unstructured content unless Clean Up Source is used first.
  - Works through both `/api/chat` and `/v1/chat/completions`.
- **Clean Up Source Skill Behavior**:
  - Detects cleanup phrases and rejects negated requests.
  - Sends messy source through an internal cleanup prompt.
  - Returns structured RAW only; does not save/compile/push unless save intent is explicit.
- **Pending Preview Storage**: `/home/nerd/aiagentnerd-system/tmp/pending-ingestions/hermes-pending-ingestion.json` (expires after 30 minutes).
- **Express Payload Limits** (in `server.js`):
  ```javascript
  app.use(express.json({ limit: "10mb" }));
  app.use(express.urlencoded({ extended: true, limit: "10mb" }));
  ```
  Graceful error response:
  ```json
  { "success": false, "error": "payload_too_large", "message": "Input too large. Please split the source into smaller chunks." }
  ```
- **Category Routing Rules**:
  - `setup`: installation, PM2, Nginx, Cloudflare, SSH, ports, cron, backups
  - `architecture`: system design, pipelines, repo structure, endpoints, memory design
  - `apps`: Open WebUI, Mission Control, Deck, X app, Telegram bot
  - `web`: articles, YouTube transcripts, public webpages, research sources
  - `chat`: important conversation summaries
  - `ideas`: product ideas, future features, naming, brainstorming
  - `inbox`: unclear or mixed material
- **Telegram Webhook**: `POST /api/telegram/ingest`
  - Verifies `X-Telegram-Bot-Api-Secret-Token` and `TELEGRAM_ALLOWED_USER_ID`.
  - Commands: `/clean`, `/save`, `/preview`, `/confirm`, `/cancel`.
  - Logs to `/home/nerd/aiagentnerd-system/logs/telegram-ingestion.log`.
  - **Status**: Paused. Likely blocked by Cloudflare Access on `hermes.aiagentnerd.com`.
  - **Planned fix**: Use a separate webhook-only subdomain such as `telegram.aiagentnerd.com` without Cloudflare Access, relying on the Telegram secret token and allowed user ID for security.
- **Operational Commands**:
  ```bash
  pm2 restart hermes
  pm2 logs hermes --lines 80
  pm2 status
  cd ~/aiagentnerd && set -a && source .env && set +a
  ```
- **Telegram Webhook Management**:
  ```bash
  curl -X POST "https://api.telegram.org/bot$TELEGRAM_BOT_TOKEN/setWebhook" \
    -d "url=https://hermes.aiagentnerd.com/api/telegram/ingest" \
    -d "secret_token=$TELEGRAM_BOT_SECRET_TOKEN"
  curl "https://api.telegram.org/bot$TELEGRAM_BOT_TOKEN/getWebhookInfo"
  ```

## Related
- [[clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
- [[save-to-knowledge-skill]]
- [[knowledge-ingestion-system]]
- [[cleanup-knowledge-3a89446a-083e-41f8-8936-334f0e4c58cd]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]

## Source
- RAW: [[RAW/openwebui/save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575]]
