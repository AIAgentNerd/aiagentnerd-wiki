---
title: Architecture Mobile Ingestion And Hermes Skill
source_raw: RAW/architecture/mobile-ingestion-and-hermes-skill.md
compiled_wiki_path: WIKI/infrastructure/mobile-ingestion-and-hermes-skill.md
compiled_at: 2026-05-01T05:27:09.994Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, mobile, ingestion, hermes, skill, git]
status: archived
archived_at: 2026-05-05T06:33:49.390Z
reclassified_to: architecture/mobile-ingestion-and-hermes-skill.md
---

# Architecture Mobile Ingestion And Hermes Skill

## Summary
This note defines the canonical workflow for capturing knowledge on mobile (e.g., YouTube videos, research notes) and feeding it into the AiAgentNerd system. It establishes the immutable separation: mobile is for capture and structuring, the server is the source of truth, and the WIKI is compiled output only. The user-facing abstraction is a single “Save to my knowledge” action, hiding the RAW → compile → WIKI pipeline. A planned Hermes skill will automate this entire chain via a dedicated ingestion endpoint.

## Key Concepts
- **Capture Hierarchy**: Mobile → RAW (temporary storage) → Laptop/Server → RAW folder → Compile → WIKI → Retrieval.
- **User Abstraction**: Users must never see RAW, WIKI, or compiler terms; the product feels like “Remember this”.
- **Mobile Role**: Capture, prompt-based structuring, temporary storage—not persistent system storage or execution.
- **Server as Source of Truth**: All RAW files live on the server in `~/aiagentnerd-wiki/RAW/`; compilation and git push happen server-side.
- **Transcript-Based Ingestion**: YouTube transcripts produce the highest quality RAW; without a transcript, structured prompts extract key concepts, workflows, and tools.
- **Hermes “Save to Knowledge” Skill**: A future Hermes command that converts user input → structured RAW, generates filename/category, writes to RAW folder, triggers compile, pushes to Git, and returns confirmation.
- **Ingestion Endpoint**: A planned `POST /api/wiki/ingest-raw` endpoint that validates, sanitizes, writes the RAW file, runs `scan-and-compile`, pushes Git, and returns a result.

## Practical Use
### Mobile Capture Options
- **Primary**: ChatGPT with a structured YouTube→RAW prompt; store output temporarily in a Notes app “RAW INBOX” note.
- **Storage**: Apple Notes / Google Keep as the RAW inbox; batch-process on laptop.
- **Transfer**: Self-chat via Telegram/WhatsApp, notes app sync, or email draft.
- **Do NOT use**: Obsidian Mobile for direct integration with system RAW folders; ChatGPT as long-term storage (cluttered, not scalable).

### Workflow
1. On mobile: capture content, use ChatGPT to generate structured RAW.
2. Store RAW temporarily in Notes app or self-message.
3. On laptop: copy RAW into `~/aiagentnerd-wiki/RAW/<category>/<filename>.md`.
4. Run compile: `curl -X POST http://localhost:3100/api/system-wiki/scan-and-compile -H "Content-Type: application/json" -d '{}'`
5. Git sync: `cd ~/aiagentnerd-wiki && git add . && git commit -m "add file" && git push`

### Recommended RAW Creation Command
```bash
cat > ~/aiagentnerd-wiki/RAW/<category>/<filename>.md
```
(Paste content, then Ctrl+D)

### Product Direction
- User clicks “Save” → system stores, structures, and future responses improve.
- Under the hood: RAW → compile → WIKI → retrieval.

### Planned Hermes Skill Flow
1. User says: “Save this to my knowledge” with content.
2. Hermes constructs a `POST /api/wiki/ingest-raw` call with `{ "category": "web", "filename": "youtube-agent-routing.md", "content": "# …" }`.
3. Backend validates, sanitizes filename, writes RAW, triggers `scan-and-compile`, git pushes, returns success.

## Implementation Notes
### Current Commands
- Create RAW: `cat > ~/aiagentnerd-wiki/RAW/<category>/<filename>.md`
- Compile: `curl -X POST http://localhost:3100/api/system-wiki/scan-and-compile -H "Content-Type: application/json" -d '{}'`
- Git sync: `cd ~/aiagentnerd-wiki && git add . && git commit -m "add file" && git push`

### Sync Strategy
- **Do NOT use Obsidian Sync** – it bypasses Git, creates conflicts, and is unaware of compile.
- Use Git-based flow: Server → GitHub → Laptop Obsidian.

### Ingestion Endpoint (Future)
- **Endpoint**: `POST /api/wiki/ingest-raw`
- **Payload**:
  ```json
  {
    "category": "web",
    "filename": "youtube-agent-routing.md",
    "content": "# markdown content..."
  }
  ```
- **Backend Steps**: validate → sanitize filename → write RAW file → run `scan-and-compile` → git push → return result.
- **Curl (conceptual)**:
  ```bash
  curl -X POST http://localhost:3100/api/wiki/ingest-raw \
    -H "Content-Type: application/json" \
    -d '{...}'
  ```

### Mobile Template (Capture Layer)
```
RAW: <filename>

Source:
<link>

Key:
- ...

Steps:
- ...

Commands:
- ...

Decision:
- ...
```

### Rules
- Mobile = capture only
- Server = source of truth
- WIKI = output only
- Never edit WIKI directly
- Always go through RAW

## Related
- [[knowledge-ingestion-system]]
- [[hermes-setup]]
- [[knowledge-ingestion-system]]
- [[git-obsidian-setup]]
- [[deck]]

## Source
- RAW: [[RAW/architecture/mobile-ingestion-and-hermes-skill]]
