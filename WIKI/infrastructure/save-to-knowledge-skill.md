---
title: Architecture Save To Knowledge Skill
source_raw: RAW/architecture/save-to-knowledge-skill.md
compiled_wiki_path: WIKI/infrastructure/save-to-knowledge-skill.md
compiled_at: 2026-05-02T04:42:26.145Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, save, knowledge, skill, git, workflow]
---

# Architecture Save To Knowledge Skill

## Summary
The "Save to Knowledge" skill enables users to submit structured raw notes directly into the wiki’s ingestion pipeline. By sending a message containing a YAML-frontmatted markdown note, the system saves it to the RAW directory, compiles the note into the wiki, and pushes the result to git. This skill is the primary manual entry point for adding human‑curated knowledge or system documentation to AiAgentNerd's knowledge base.

## Key Concepts
- **Save to Knowledge** – a direct-user command that stores a raw note in the correct RAW location.
- **RAW note** – a markdown file with YAML frontmatter (`category`, `filename`, `type`) stored under `RAW/<category>/<filename>`.
- **Type: raw** – a frontmatter flag that bypasses the multi‑note splitter during compilation, treating the note as a final artifact.
- **Compilation step** – the system automatically runs the wiki compiler after saving, which may produce compiled wiki notes, and reports compile/skip/fail counts.
- **Git push** – after compilation, changes are pushed to the wiki’s git repository.

## Practical Use
1. A human user sends a message that begins with `Save this to knowledge` followed by a markdown block containing the frontmatter and body.
2. The assistant saves that content to `/home/nerd/aiagentnerd-wiki/RAW/<category>/<filename>`.
3. The assistant triggers the wiki compilation process (which can split multi‑note RAWs, skip already‑current notes, and produce compiled output).
4. The assistant reports the compile results: how many notes were compiled, skipped, and failed, and confirms the git push.

In the example captured, one note was compiled, 32 were skipped, and 0 failed.

## Implementation Notes
- **RAW storage path**: `/home/nerd/aiagentnerd-wiki/RAW/<category>/<filename>`
- **Bypass behaviour**: When `type: raw` is set in the frontmatter, the multi‑note splitter is skipped; the note is treated as a single final RAW note.
- The compile step yielded `compiled: 1`, `skipped: 32`, `failed: 0` in the observed case.  
  The criteria for compiling vs skipping are not documented in this note – they are an open question.
- The exact compilation steps (beyond possible multi‑note splitting) are not detailed here; they are part of the broader knowledge‑ingestion system.

## Related
- [[save-it-to-knowledge-category-architecture-filename-hermes-knowledge-ingestion-s-cf1c4209-ed9a-4a13-a4a4-d57f77d2f575]]
- [[knowledge-ingestion-system]]
- [[mobile-ingestion-and-hermes-skill]]
- [[clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
- [[knowledge-ingestion-system]]

## Source
- RAW: [[RAW/architecture/save-to-knowledge-skill]]
