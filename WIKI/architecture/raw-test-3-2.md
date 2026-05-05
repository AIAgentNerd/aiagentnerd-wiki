---
title: Architecture Raw Test 3 2
source_raw: RAW/architecture/raw-test-3-2.md
compiled_wiki_path: WIKI/architecture/raw-test-3-2.md
compiled_at: 2026-05-05T03:37:11.746Z
type: system-note
tags: [aiagentnerd, compiled, architecture, 3, 2, git]
---

# Architecture Raw Test 3 2

## Summary
This note documents the Phase 6 Smoke Test, which verifies the consistency between RAW and WIKI content in the AiAgentNerd system. It ensures that the compilation process accurately preserves the original content.

## Key Concepts
- **Phase 6 Smoke Test**: A verification process to ensure RAW to WIKI consistency.
- **RAW to WIKI**: The process of compiling raw content into a clean internal technical wiki note.

## Practical Use
- This test is used to validate the compilation process, ensuring that no information is lost or altered during the transformation from RAW to WIKI.
- It helps maintain the integrity of the knowledge base by confirming that the compiled content matches the original RAW content.

## Implementation Notes
- The test involves comparing the RAW content with the compiled WIKI content to ensure they are identical.
- The test can be run manually or as part of an automated pipeline.
- Example command to run the test:
  ```sh
  python scripts/phase_6_smoke_test.py --raw_path=/home/nerd/aiagentnerd-wiki/RAW/architecture/raw-test-3-2.md --wiki_path=architecture/raw-test-3-2.md
  ```

## Related
- [[raw-test-2]]
- [[raw-test-3]]
- [[raw-test]]
- [[test-raw-bypass]]
- [[hermes-knowledge-system-full-architecture]]

## Source
- RAW: [[RAW/architecture/raw-test-3-2]]
