---
title: Concepts Hermes Native Auto Pipeline Test
source_raw: RAW/concepts/hermes-native-auto-pipeline-test.md
compiled_wiki_path: WIKI/concepts/hermes-native-auto-pipeline-test.md
compiled_at: 2026-05-09T13:43:28.661Z
type: system-note
tags: [aiagentnerd, compiled, concepts, hermes, native, auto, pipeline, workflow]
---

# Concepts Hermes Native Auto Pipeline Test

## Summary
This note records a test of the combined save-and-compile MCP workflow within the Hermes native auto pipeline. It exists to validate that the integrated automation step can persist RAW content and trigger wiki compilation in a single pass.

## Key Concepts
- **Hermes native auto pipeline**: The automation pipeline orchestrated by Hermes for processing system notes.
- **Save+compile MCP workflow**: A combined Model Context Protocol workflow that first saves RAW content and then compiles it into the internal wiki format.
- **Pipeline validation**: Testing the end-to-end integration of persistence and compilation steps.

## Practical Use
- Serves as a smoke test to confirm the MCP save-and-compile sequence executes without errors.
- Used to verify Hermes automation behavior before applying the pipeline to operational or curated knowledge.

## Implementation Notes
- This is a minimal concept test; no specific commands, file paths, configuration values, or error messages are provided in the source.
- The test focuses on the integration boundary between the save (RAW persistence) and compile (wiki generation) phases.

## Related
- [[hermes-full-native-memory-pipeline-test]]
- [[hermes-native-memory-test]]
- [[hermes-knowledge-system-full-architecture]]
- [[aiagentnerd-knowledge-system-explainer-and-workflow]]
- [[deck]]

## Source
- RAW: [[RAW/concepts/hermes-native-auto-pipeline-test]]
