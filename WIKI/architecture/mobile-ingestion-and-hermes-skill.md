---
title: Architecture Mobile Ingestion And Hermes Skill
source_raw: RAW/architecture/mobile-ingestion-and-hermes-skill.md
compiled_wiki_path: WIKI/architecture/mobile-ingestion-and-hermes-skill.md
compiled_at: 2026-05-05T06:33:49.385Z
type: system-note
tags: [aiagentnerd, compiled, architecture, mobile, ingestion, hermes, skill, git]
---

# Architecture Mobile Ingestion And Hermes Skill

## Summary
Defines the end-to-end mobile knowledge capture pipeline and the planned Hermes “Save to Knowledge” automation skill. Mobile devices handle capture and lightweight structuring, while the Nerd server remains the sole source of truth for RAW storage, compilation, and Git-backed Obsidian sync. The design explicitly abstracts RAW/WIKI/compile mechanics from users behind a simple “Save this to my knowledge” product interface.

## Key Concepts
- **Mobile = capture only**: Phones and tablets ingest content (e.g., YouTube, research) and structure it into RAW form; compilation and execution stay on the server.
- **Server as source of truth**: RAW files live in `~/aiagentnerd-wiki/RAW/<category>/`; the WIKI is read-only compiled output.
- **Product abstraction**: Users must not be exposed to “RAW”, “WIKI”, or “compile”; the interaction should feel like a single save/remember action.
- **Transcript-first ingestion**: YouTube content processed from transcripts produces the highest-fidelity RAW notes and avoids hallucination; without transcripts, use structured extraction for key concepts, workflows, and tools.
- **Git-only sync**: Obsidian Sync is prohibited for the system vault because it bypasses Git, creates conflicts, and ignores the compile step. Sync must follow Server → Git → Local Obsidian.
- **Hermes ingestion endpoint**: A planned `POST /api/wiki/ingest-raw` endpoint to automate RAW creation, compilation, and Git push.

## Practical Use
- **Mobile capture flow**: Consume content → generate structured RAW via ChatGPT or template → stage temporarily in a synced Notes app “RAW INBOX” (preferred) or Telegram/WhatsApp self-chat → transfer to laptop → save to server RAW folder → compile → push to Git.
- **YouTube ingestion**: Paste a link into ChatGPT mobile with a YouTube→RAW prompt; prefer transcript-based extraction when available.
- **Capture template**: Each mobile entry should include `RAW: <filename>`, Source link, Key points, Steps, Commands, and Decisions.
- **ChatGPT as temporary storage**: One chat per RAW note titled `RAW: <filename>` is acceptable for immediate structuring, but do not use ChatGPT as the primary inbox; use a Notes app for batching and longevity.
- **Server-side workflow**: Create the RAW file with the terminal, trigger compilation via the Hermes API, then run the standard Git add/commit/push sequence.

## Implementation Notes
- **RAW file creation (selected method)**: Use `cat > ~/aiagentnerd-wiki/RAW/<category>/<filename>.md` for speed and consistency; avoid UI-dependent editors.
- **Compilation endpoint**: `POST http://localhost:3100/api/system-wiki/scan-and-compile` with an empty JSON body triggers the compile pipeline.
- **Git sync commands**:
  ```bash
  cd ~/aiagentnerd-wiki
  git add .
  git commit -m "add <filename>"
  git push
  ```
- **Obsidian sync constraint**: Do not enable Obsidian Sync on the system vault. The canonical flow is server repository → GitHub → local Obsidian vault pull.
- **Ingestion API specification**: A future `POST /api/wiki/ingest-raw` endpoint will accept:
  ```json
  {
    "category": "web",
    "filename": "youtube-agent-routing.md",
    "content": "# markdown..."
  }
  ```
  Backend flow: validate payload → sanitize filename → write to `~/aiagentnerd-wiki/RAW/<category>/<filename>.md` → trigger compilation → Git push → return confirmation.
- **Build order**: Implement the ingestion endpoint first, then expose it as a Hermes skill so users can paste content and invoke “Save this to my knowledge.”
- **Guardrails**: Never edit WIKI files directly. All changes must flow through RAW → compile.

## Related
- [[mobile-ingestion-and-hermes-skill]]
- [[knowledge-ingestion-system]]
- [[knowledge-ingestion-system]]
- [[hermes-knowledge-ingestion-system]]
- [[hermes-knowledge-ingestion-system]]

## Source
- RAW: [[RAW/architecture/mobile-ingestion-and-hermes-skill]]
