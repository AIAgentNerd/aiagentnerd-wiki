---
title: Architecture Save To Knowledge Skill
source_raw: RAW/architecture/save-to-knowledge-skill.md
compiled_wiki_path: WIKI/architecture/save-to-knowledge-skill.md
compiled_at: 2026-05-05T06:36:20.408Z
type: system-note
tags: [aiagentnerd, compiled, architecture, save, knowledge, skill, git, workflow]
---

# Architecture Save To Knowledge Skill

## Summary
The "Save to Knowledge" skill enables users to submit raw knowledge notes directly to the AiAgentNerd system wiki. The note is saved to the RAW directory, compiled, and pushed to the Git repository, ensuring the knowledge is integrated into the system.

## Key Concepts
- **Save to Knowledge Skill**: User command to submit raw knowledge notes.
- **RAW Note Ingestion**: Notes are saved with YAML frontmatter in the RAW directory.
- **Compilation**: The system compiles the saved note and pushes changes to GitHub.
- **Git Push**: Ensures the compiled note is version-controlled and available in the wiki.

## Practical Use
- **User Command**: "Save this to knowledge" followed by a markdown block with the note.
- **Note Structure**: The note must include YAML frontmatter with `category`, `filename`, and `type` (usually `raw`).
- **Save Path**: The note is saved to `/home/nerd/aiagentnerd-wiki/RAW/<category>/<filename>`.
- **Compilation**: The system runs a compilation process that may include multi-note splitting or other steps.
- **Compile Stats**: The assistant reports the number of notes compiled, skipped, and failed.
- **Git Push**: The compiled note is pushed to the Git repository.

## Implementation Notes
- **Example Note**: The example note had `type: raw`, ensuring it bypassed the multi-note splitter.
- **Compilation Result**: The compilation step compiled 1 note, skipped 32, and failed 0.
- **No Commands Captured**: No specific commands were captured in this workflow.
- **Open Questions**:
  - What determines which notes get compiled vs. skipped?
  - What are the exact compilation steps?

## Related
- [[save-to-knowledge-skill]]
- [[save-this-to-knowledge-with-preview-----category-architecture-filename-hermes-kn-4debc305-26df-4725-a347-4effb3d3b3e5]]
- [[save-this-to-knowledge-with-preview-this-document-talks-about-cleanup-archive-me-f8699000-87a3-4a87-aa95-f6997d445829]]
- [[hermes-knowledge-system-full-architecture]]
- [[knowledge-ingestion-system]]

## Source
- RAW: [[RAW/architecture/save-to-knowledge-skill]]
