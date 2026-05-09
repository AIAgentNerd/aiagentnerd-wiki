---
title: Architecture Hermes Clean Save Compile Sync Test
source_raw: RAW/architecture/hermes-clean-save-compile-sync-test.md
compiled_wiki_path: WIKI/architecture/hermes-clean-save-compile-sync-test.md
compiled_at: 2026-05-09T14:02:08.565Z
type: system-note
tags: [aiagentnerd, compiled, architecture, hermes, clean, save, compile, sync]
---

# Architecture Hermes Clean Save Compile Sync Test

## Summary
Validates the native Hermes clean-save-compile-sync workflow. Tests the full pipeline from rough Workspace input through RAW generation, WIKI compilation, and Git synchronization.

## Key Concepts
- **Clean-save-compile-sync**: Hermes native workflow for processing rough knowledge into structured system memory
- **Workspace**: Input area for unparsed, informal builder notes
- **RAW**: Intermediate machine format before compilation
- **WIKI**: Final compiled and structured internal documentation state
- **Git sync**: Persistence layer for version-controlled wiki storage

## Practical Use
- Paste rough knowledge into Workspace to trigger automated RAW capture, compilation, and Git sync.
- Ensures informal notes are transformed into structured, versioned system memory without manual formatting.

## Implementation Notes
- Pipeline stages: Workspace → RAW → WIKI → Git
- Compiled artifacts are written to the architecture path in the wiki repository
- Intended for system and architecture notes that require persistence and versioning

## Related
- [[hermes-mcp-save-compile-test]]
- [[lets-try-again-save-this-to-knowledge-with-preview-random-test-about-systems-architecture]]
- [[clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
- [[hermes-full-native-memory-pipeline-test]]
- [[raw-test]]

## Source
- RAW: [[RAW/architecture/hermes-clean-save-compile-sync-test]]
