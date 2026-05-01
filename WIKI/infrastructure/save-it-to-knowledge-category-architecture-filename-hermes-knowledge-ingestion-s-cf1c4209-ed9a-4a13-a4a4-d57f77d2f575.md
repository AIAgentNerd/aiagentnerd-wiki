---
title: Openwebui Save It To Knowledge Category Architecture Filename Hermes Knowledge Ingestion S Cf1c4209 Ed9a 4a13 A4a4 D57f77d2f575
source_raw: RAW/openwebui/save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575.md
compiled_wiki_path: WIKI/infrastructure/save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575.md
compiled_at: 2026-05-01T19:50:07.079Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, save, it, knowledge, category, architecture]
---

# Openwebui Save It To Knowledge Category Architecture Filename Hermes Knowledge Ingestion S Cf1c4209 Ed9a 4a13 A4a4 D57f77d2f575

## Summary
The Hermes Knowledge Ingestion System is the internal workflow that accepts messy pasted text (SOURCE), cleans it into structured RAW markdown, and then saves, compiles, and pushes it to the AiAgentNerd wiki. It uses a multi-step pipeline with separate skills for cleaning and saving, supports preview and confirmation, category auto-routing, multi-note splitting, and fallback mechanisms. The system currently operates via Open WebUI, with a paused Telegram webhook attempt blocked by Cloudflare Access. It is a core part of the internal knowledge compilation loop and not yet a user-facing GoldieNerd feature.

## Key Concepts
- **SOURCE**: Unstructured input (chat logs, transcripts, notes)
- **RAW**: Cleaned, structured markdown archive stored under `RAW/<category>/`
- **WIKI**: Compiled reusable knowledge layer (final output)
- **Pipeline**: SOURCE → Clean Up Source → RAW → Save to Knowledge → `/api/wiki/ingest-raw` → Hermes compile → WIKI → Git push → Obsidian sync
- **Skills**: Clean Up Source (cleans SOURCE), Save to Knowledge (calls ingest endpoint), Multi-Note Splitting (splits long inputs)
- **Preview Before Save**: Pending previews stored at `/home/nerd/aiagentnerd-system/tmp/pending-ingestions/hermes-pending-ingestion.json`, expire after 30 min
- **Category Auto-Routing**: Helper `inferRawCategoryFromContent(content, fallback = "inbox")` maps content to categories: `chat, web, setup, architecture, apps, ideas, inbox`
- **Multi-Note Splitting**: Handler order: `handlePendingIngestionConfirmation` → `handleMultiNoteIngestionSkill` → `handleCleanUpSourceSkill` → `handleSaveToKnowledgeSkill` → normal LLM flow
- **Fallbacks**: Kimi model failures (empty content/truncation) cause fallback to Qwen for compilation; payload size limits (10MB) enforce splitting

## Practical Use
- **Open WebUI** is the current ingestion interface for both desktop and mobile.
- Workflow commands:
  - `Clean this up` – returns RAW only, no save/compile/push
  - `Save this to knowledge` – saves structured RAW, compiles, pushes
  - `Clean this up and save it` – cleans then auto-saves
  - `Save this to knowledge with preview` – stores pending preview; followed by `confirm save` or `cancel`
  - For large or multi-topic input: `Save this to knowledge with preview. Split into multiple notes if needed.` then `confirm save`
  - Rejects messy input unless Clean Up Source is used first (but automatic cleanup is now supported)
- Commands to manage Hermes:
  - `pm2 restart hermes`
  - `pm2 logs hermes --lines 80`
  - `pm2 status`
  - `node --check server.js` before restart
- Loading `.env`: `cd ~/aiagentnerd && set -a && source .env && set +a`
- Telegram webhook (currently broken due to Cloudflare Access):
  - Set: `curl -X POST "https://api.telegram.org/bot$TELEGRAM_BOT_TOKEN/setWebhook" -d "url=https://hermes.aiagentnerd.com/api/telegram/ingest" -d "secret_token=$TELEGRAM_BOT_SECRET_TOKEN"`
  - Check: `curl "https://api.telegram.org/bot$TELEGRAM_BOT_TOKEN/getWebhookInfo"`
  - Future: use `telegram.aiagentnerd.com` subdomain without Cloudflare Access
- Large payload handling: increased Express body limit to 10MB; graceful error responses for payload too large

## Implementation Notes
- **Ingest RAW Endpoint**: `POST /api/wiki/ingest-raw`
  - Validates category, filename (sanitized, no slashes, no `..`), non-empty markdown
  - Writes to `RAW/<category>/` in aiagentnerd-wiki repo
  - Supports `overwrite: true`, `dryRun: true`
  - Calls `/api/system-wiki/scan-and-compile` for compilation
  - Uses `execFile` for Git commands
  - Logs to `/home/nerd/aiagentnerd-system/logs/ingestion.log`
- **Save to Knowledge Skill**:
  - Detects save phrases, ignores negations (e.g., "don't save")
  - Extracts fenced or pasted RAW markdown
  - Infers category (default: `inbox`) and kebab-case filename
  - Rejects messy content unless Clean Up Source precedes it
  - Works via `/api/chat` and `/v1/chat/completions`
- **Clean Up Source Skill**:
  - Detects cleanup phrases, ignores negations
  - Processes messy source through an internal cleanup prompt, returns RAW only
  - Does not save/compile/push unless combined with save command
- **Multi-Note Splitting**:
  - Handler processes long/multi-topic sources into `notes[]` JSON
  - Batch preview stores `notes[]`; `confirm save` ingests each note via `/api/wiki/ingest-raw` individually
  - Known issue: batch save currently calls ingest once per note (single compile/Git commit would be optimal)
- **Telegram Ingestion**:
  - Endpoint: `POST /api/telegram/ingest` with `X-Telegram-Bot-Api-Secret-Token` verification
  - Allowed user: `TELEGRAM_ALLOWED_USER_ID`
  - Log: `/home/nerd/aiagentnerd-system/logs/telegram-ingestion.log`
  - Blocked because `hermes.aiagentnerd.com` uses Cloudflare Access; Telegram can't reach webhook; paused
- **Server Config** (`server.js`):
  - `express.json({ limit: "10mb" })`, `express.urlencoded({ extended: true, limit: "10mb" })`
  - Restart required after changes
- **Model Routing**:
  - During compilation, uses secondary model (Kimi) for `wiki_compile` tasks; falls back to Qwen on empty content or truncation (`finishReason: length`)

## Related
- [[clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
- [[knowledge-ingestion-system]]
- [[knowledge-ingestion-system]]
- [[hermes-knowledge-ingestion-system]]
- [[cloudflare-network]]

## Source
- RAW: [[RAW/openwebui/save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575]]
