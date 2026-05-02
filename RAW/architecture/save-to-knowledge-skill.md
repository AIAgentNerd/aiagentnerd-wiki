---
category: architecture
filename: save-to-knowledge-skill.md
type: raw
---# Save to Knowledge Skill

## Topics
- Save to Knowledge
- RAW note ingestion
- Compilation
- Git push

## Context
Chat history shows a user command "Save this to knowledge" followed by a raw markdown note with frontmatter. The assistant responds with confirmation, RAW path, compile stats, and git push.

## Key Concepts
- The "Save to Knowledge" skill allows users to submit raw knowledge notes directly for storage in the wiki.
- The note must include a YAML frontmatter with category, filename, and type (usually raw).
- The system saves the note to /home/nerd/aiagentnerd-wiki/RAW/<category>/<filename>.
- Then it runs a compilation process that may compile the saved note and push changes to github.
- The compilation result shows numbers: compiled, skipped, failed.

## Workflow / Steps
1. User sends message "Save this to knowledge" followed by a markdown block with the note.
2. Assistant saves the note to the RAW directory.
3. Assistant compiles the wiki (possibly triggering multi-note splitting or other compilation steps).
4. Assistant reports compile stats and git push result.

## Commands

### Primary Commands
```bash
# None captured.
```

### Supporting Commands
```bash
# None captured.
```

## Important Details
- The saved note in the example had type: raw, which ensures it bypasses the multi-note splitter.
- The compilation step compiled 1 note, skipped 32, and failed 0.

## Open Questions
- What determines which notes get compiled vs skipped?
- What are the exact compilation steps?

---
## Compiled Wiki
- WIKI: [[WIKI/infrastructure/save-to-knowledge-skill]]
- Last compiled: 2026-05-02T04:42:26.145Z
