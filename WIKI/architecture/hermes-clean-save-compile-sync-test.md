---
title: Architecture Hermes Clean Save Compile Sync Test
source_raw: RAW/architecture/hermes-clean-save-compile-sync-test.md
compiled_wiki_path: WIKI/architecture/hermes-clean-save-compile-sync-test.md
compiled_at: 2026-05-09T13:07:33.612Z
type: system-note
tags: [aiagentnerd, compiled, architecture, hermes, clean, save, compile, sync]
---

# Architecture Hermes Clean Save Compile Sync Test

## Summary
A test note for the native Hermes clean-save-compile-sync workflow. Validates that rough knowledge entered in the Workspace is converted by Memory into RAW, compiled into structured WIKI format, and synchronized to Git.

## Key Concepts
- **Hermes clean-save-compile-sync**: End-to-end pipeline for ingesting rough notes into version-controlled system memory
- **Workspace**: Initial capture surface for unstructured builder knowledge
- **Memory**: System layer that transforms Workspace input into RAW notes
- **RAW → WIKI compilation**: Structured processing of unformatted notes into clean internal documentation
- **Git sync**: Final stage publishing compiled wiki content to the repository

## Practical Use
- Verify pipeline functionality by tracing a note from Workspace through RAW compilation to WIKI and Git
- Use as a reference artifact when onboarding or debugging the knowledge ingestion flow
- Confirm that architectural notes are correctly categorized and persisted

## Implementation Notes
- Source context: `hermes-workspace`
- Target category: `architecture`
- This is a validation artifact; it contains no production configuration, commands, or operational logic

## Related
- [[hermes-mcp-save-compile-test]]
- [[lets-try-again-save-this-to-knowledge-with-preview-random-test-about-systems-architecture]]
- [[clean-this-up-and-save-it-ok-so-basically-you-need-to-restart-hermes-using-pm2-r-1218946d-06ba-47ad-a3b4-08b528bc7143]]
- [[hermes-full-native-memory-pipeline-test]]
- [[raw-test]]

## Source
- RAW: [[RAW/architecture/hermes-clean-save-compile-sync-test]]
