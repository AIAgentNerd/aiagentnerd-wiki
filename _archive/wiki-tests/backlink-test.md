---
title: Backlink Test
source_raw: RAW/backlink-test.md
compiled_wiki_path: WIKI/infrastructure/backlink-test.md
compiled_at: 2026-04-24T14:37:44.820Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, backlink, cloudflare, networking, ssh, hermes]
---

# Backlink Test

## Summary
Test fixture for the RAW-to-WIKI compilation pipeline. Validates backlink resolution, bidirectional source linking, tag handling, and safe anchor generation for headings containing hash characters.

## Key Concepts
- RAW-to-WIKI backlink resolution
- WIKI-to-RAW source traceability
- Tag preservation and frontmatter merging
- Hash-safe anchor generation
- Infrastructure references: Cloudflare, SSH, networking, Hermes, PM2

## Details
This note exercises the wiki compiler's transformation logic to ensure internal links survive the RAW-to-WIKI migration. It verifies that:
- Backlinks are correctly parsed and rewritten in compiled output
- Source links maintain a pointer back to the originating RAW file
- Tags are normalized and merged into frontmatter without collision
- Heading anchors

## Source
- RAW: [[RAW/backlink-test]]

## Related
- [[cloudflare-network]]
- [[hermes-setup]]
- [[Networking Ports and IPs]]
- [[ssh-ports]]
- [[test-nginx]]
