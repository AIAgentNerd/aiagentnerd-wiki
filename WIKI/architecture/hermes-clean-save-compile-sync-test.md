---
title: Architecture Hermes Clean Save Compile Sync Test
source_raw: RAW/architecture/hermes-clean-save-compile-sync-test.md
compiled_wiki_path: WIKI/architecture/hermes-clean-save-compile-sync-test.md
compiled_at: 2026-05-09T13:17:32.357Z
type: system-note
tags: [aiagentnerd, compiled, architecture, hermes, clean, save, compile, sync]
---

# Architecture Hermes Clean Save Compile Sync Test

## Summary
A test note validating the native Hermes clean-save-compile-sync workflow. Rough knowledge pasted into Workspace is automatically processed into RAW format, compiled into structured WIKI notes, and synchronized to the Git repository.

## Key Concepts
- **Hermes workflow**: clean-save-compile-sync pipeline for knowledge management
- **Workspace**: Entry point for rough, unprocessed knowledge
- **Memory**: System component that transforms workspace content into RAW and compiled WIKI formats
- **Git sync**: Final stage pushing compiled wiki notes to version control

## Practical Use
- Paste unstructured or draft knowledge into the Hermes Workspace for automated processing
- Verify end-to-end flow from raw input to structured, version-controlled wiki output
- Use as a reference test case when debugging the save-compile-sync pipeline

## Implementation Notes
- Workflow stages: Workspace input → RAW generation → WIKI compilation → Git synchronization
- Triggered by native Hermes operations rather than manual file editing
- Designed to reduce friction in capturing and persisting system knowledge

## Related
- [[hermes-mcp-save-compile-test]]
- [[lets-try-again-save-this-to-knowledge-with-preview-random-test-about-systems-architecture]]
- [[clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
- [[hermes-full-native-memory-pipeline-test]]
- [[raw-test]]

## Source
- RAW: [[RAW/architecture/hermes-clean-save-compile-sync-test]]
