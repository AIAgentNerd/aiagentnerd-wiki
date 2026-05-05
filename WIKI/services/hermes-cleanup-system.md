---
title: Inbox Hermes Cleanup System
source_raw: RAW/inbox/hermes-cleanup-system.md
compiled_wiki_path: WIKI/services/hermes-cleanup-system.md
compiled_at: 2026-05-05T02:48:12.429Z
type: system-note
tags: [aiagentnerd, compiled, services, hermes, cleanup, debugging]
---

# Inbox Hermes Cleanup System

## Summary
The Hermes Cleanup System is responsible for maintaining the integrity and efficiency of the AiAgentNerd knowledge base. It addresses issues related to merge logic, archive management, and automated cleanup processes.

## Key Concepts
- **Merge Logic**: Rules for combining and reconciling multiple sources of data without overwriting canonical files.
- **Archive Management**: Systematic storage and retrieval of historical data instead of deletion.
- **Canonical Files**: Authoritative versions of files that should not be overwritten.
- **Chunking**: Splitting large inputs into manageable chunks to avoid processing failures.
- **Pending State Files**: Temporary files used during the cleanup process, stored in `system/tmp`.
- **Auto Cleanup**: Automated processes for identifying and handling low-value or duplicate content.

## Practical Use
- **Merge Logic**: Merge operations should not overwrite canonical files. Instead, they should be merged in a way that preserves the integrity of the canonical version.
- **Archive Management**: Instead of deleting content, it should be archived. This ensures that historical data is retained and can be retrieved if needed.
- **Preview Before Confirm**: Users should have the option to preview changes before confirming them, especially for critical operations.
- **Pending State Files**: These files are stored in the `system/tmp` directory and are used to manage the state of the cleanup process.
- **Chunking**: Large inputs are split into chunks to prevent processing failures. This is particularly useful for handling long inputs that might cause the wiki compile to fail.
- **Auto Cleanup**: The auto cleanup process should be designed to distinguish between low-value content and duplicates. It should be tested to ensure it makes accurate decisions.

## Implementation Notes
- **Commands**:
  ```sh
  # Example command to run the Knowledge Cleanup Agent
  python scripts/knowledge_cleanup_agent.py --action=cleanup --source=raw_data --destination=clean_data
  ```
- **Decisions**:
  - **Safety First**: The "delete cleanup group" feature has been disabled to prevent accidental data loss. Instead, content is archived.
  - **Chunking for Long Inputs**: Chunking has been implemented to handle long inputs and prevent wiki compile failures.

## Related
- [[cleanup-knowledge-about-hermes-setup-ef1de140-a2ad-459a-8174-ae17d74be2f4]]
- [[hermes-service-restart-and-troubleshooting-merged-2]]
- [[hermes-knowledge-system-full-architecture]]
- [[deck]]
- [[hermes-knowledge-ingestion-system]]

## Source
- RAW: [[RAW/inbox/hermes-cleanup-system]]
