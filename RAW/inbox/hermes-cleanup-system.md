---
category: inbox
filename: hermes-cleanup-system.md
type: raw
---

# Hermes Cleanup System

## Topics
- Merge Logic
- Archive Management
- Canonical Files
- Chunking
- Pending State Files
- Auto Cleanup

## Context
This document outlines the key concepts and important details of the Hermes Cleanup System, which is responsible for maintaining the integrity and efficiency of the AiAgentNerd knowledge base. It addresses issues related to merge logic, archive management, and auto cleanup processes.

## Key Concepts
- **Merge Logic**: Rules for combining and reconciling multiple sources of data without overwriting canonical files.
- **Archive Management**: Systematic storage and retrieval of historical data instead of deletion.
- **Canonical Files**: Authoritative versions of files that should not be overwritten.
- **Chunking**: Splitting large inputs into manageable chunks to avoid processing failures.
- **Pending State Files**: Temporary files used during the cleanup process, stored in `system/tmp`.
- **Auto Cleanup**: Automated processes for identifying and handling low-value or duplicate content.

## Important Details
- **Merge Logic**: Merge operations should not overwrite canonical files. Instead, they should be merged in a way that preserves the integrity of the canonical version.
- **Archive Management**: Instead of deleting content, it should be archived. This ensures that historical data is retained and can be retrieved if needed.
- **Preview Before Confirm**: Users should have the option to preview changes before confirming them, especially for critical operations.
- **Pending State Files**: These files are stored in the `system/tmp` directory and are used to manage the state of the cleanup process.
- **Chunking**: Large inputs are split into chunks to prevent processing failures. This is particularly useful for handling long inputs that might cause the wiki compile to fail.
- **Auto Cleanup**: The auto cleanup process should be designed to distinguish between low-value content and duplicates. It should be tested to ensure it makes accurate decisions.

## Commands
```sh
# Example command to run the Knowledge Cleanup Agent
python scripts/knowledge_cleanup_agent.py --action=cleanup --source=raw_data --destination=clean_data
```

## Decisions
- **Safety First**: The "delete cleanup group" feature has been disabled to prevent accidental data loss. Instead, content is archived.
- **Chunking for Long Inputs**: Chunking has been implemented to handle long inputs and prevent wiki compile failures.

## Open Questions
- **Handling Duplicate Topics**: What happens if the same topic exists in multiple RAW files?
- **Auto Cleanup Criteria**: How does the auto cleanup process decide what content is low value versus a duplicate?
----------------------------------------

Reply: confirm save
</chat_history>

---
## Compiled Wiki
- WIKI: [[WIKI/services/hermes-cleanup-system]]
- Last compiled: 2026-05-05T02:48:12.429Z
