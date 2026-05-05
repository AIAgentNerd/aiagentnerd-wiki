---
category: architecture
filename: aiagentnerd-backend-hardening-summary.md
type: raw
---
# AiAgentNerd Backend Hardening Summary
## Topics
- backend hardening
- Save to Knowledge
- RAW to WIKI pipeline
- intent routing
- pending state safety
- chunking
- cleanup safety
- Git safety
- RAW/WIKI consistency
- logging privacy
## Context
This note summarizes the debugging and hardening phase for the AiAgentNerd / Hermes backend knowledge system.
The goal of this phase was to move the system from a fragile prototype into a deterministic, safe, production-grade backend that can reliably ingest messy or structured input, preview changes, save RAW files, compile WIKI files, push to Git, and keep the knowledge system consistent over time.
## Key Concepts
- The core product behavior is: paste anything, preview it, confirm it, save it safely, and make it usable knowledge.
- RAW is the source of truth.
- WIKI is the compiled, usable knowledge layer.
- All Save-to-Knowledge writes now follow preview before confirm.
- Intent routing is deterministic and command-driven.
- Cleanup actions are safe, preview-first, and archive-first.
- RAW/WIKI consistency is now actively verified instead of blindly trusting the manifest.
- Git operations now stage only touched files.
- Logs are safer and avoid storing full pasted content.
## Major Improvements
### Save-to-Knowledge Resilience
The Save-to-Knowledge flow was stabilized so that user input no longer fails easily.
Behavior now:
- valid RAW is preserved exactly
- near-RAW is normalized locally
- messy input is cleaned through Clean Up Source
- failed cleanup produces a safe RAW capture fallback
- all save writes require preview and confirm
This changed the system behavior from fragile cleanup-dependent ingestion to resilient ingestion.
### File-Exists Resolution
The system no longer fails with a simple file_exists error.
When a file already exists, Hermes now offers safe choices:
- merge with existing
- overwrite with preview
- save as new version
The default safe behavior is to avoid overwriting and use preview-first resolution.
### Fuzzy Pending Commands
Pending commands no longer require exact wording.
Examples now understood during pending save state:
- save as new version
- save as a new version
- save new version
- merge existing
- merge with existing knowledge
- overwrite file
- replace file
- confirm
- yes save
- cancel
- never mind
Fuzzy matching only runs when a pending state exists, preventing accidental command execution.
### Pending State Safety
The system now prevents multiple active pending actions from overwriting each other.
Pending state checks cover:
- ingestion preview
- merge preview
- cleanup preview
- auto cleanup preview
- mark superseded preview
If a pending action already exists, Hermes asks the user to confirm or cancel it first.
### Intent Routing Hardening
Intent detection was changed to rely on the first command line where practical.
This prevents pasted content from accidentally triggering commands like save, merge, cleanup, or split.
Result:
- commands are deterministic
- pasted source content is treated as content
- accidental execution risk is reduced
### Chunking Hardening
Large input handling was hardened with a central OpenRouter guard.
Implemented behavior:
- oversized prompts are detected before model calls
- supported tasks use chunking
- unsupported generic chat is rejected with a clear message
- long lines and blocks are hard-split safely
- chunking logs show size, threshold, and task type
Supported chunking task types include:
- wiki_compile
- merge_knowledge
- cleanup_processing
- save_to_knowledge_cleanup
### Cleanup Safety
The Knowledge Cleanup Agent was hardened.
Final cleanup behavior:
- delete is disabled
- archive is preferred
- canonical files are protected
- auto cleanup only archives safe high-confidence targets
- low and medium confidence groups are skipped
- all write actions require preview and confirmation
### Archive Filtering
Archived files are now excluded from:
- merge candidates
- cleanup scans
- auto cleanup selection
This prevents archived knowledge from being repeatedly reprocessed.
### Git Safety
Git operations were hardened.
Changes:
- removed git add .
- only explicit touched files are staged
- unrelated staged files cause push refusal
- git commit uses argument-based execution instead of shell-string interpolation
- path traversal guards protect file operations
### RAW/WIKI Consistency
The compile pipeline now verifies consistency instead of blindly trusting the manifest.
Behavior:
- WIKI existence is verified after compile
- missing WIKI files force recompile
- classifier target changes force recompile
- stale old WIKI copies are archived
- manifest entries are updated only after verified compile
- false compile failures can be recovered when WIKI metadata proves success
### Compile Failure Recovery
The system now handles cases where compile appears to fail but WIKI output actually exists.
If the WIKI file exists and metadata matches, Hermes treats the compile as recovered success and logs the mismatch.
### Logging Privacy
Logs were hardened to reduce sensitive content exposure.
Current logging behavior:
- logs first command line instead of full pasted content
- logs message length and selected handler
- avoids full user body/source content
- route-level errors use safe metadata, message, and code
## Important System Rules
- RAW is the source of truth.
- WIKI is derived from RAW.
- Save-to-Knowledge always uses preview then confirm.
- No destructive cleanup action runs automatically.
- Delete is disabled.
- Archive is preferred over delete.
- Canonical files must not be archived by auto cleanup.
- Git pushes only include known touched files.
- Pasted source content should not trigger commands unless the first line is a command.
- Logs should not contain full pasted user content.
## Tested Flows
The following flows were tested and confirmed:
- messy input saves successfully
- structured RAW saves successfully
- duplicate filename resolution works
- save as new version works
- compile result includes wikiPath
- false compile_failed response was fixed
- RAW file is created
- WIKI file is created
- Git push succeeds
- preview-first behavior works
- fuzzy pending commands work
## Current Backend Status
The AiAgentNerd / Hermes backend knowledge system is now considered production-grade for internal use.
Current state:
- ingestion is reliable
- preview and confirm flow is enforced
- compile is verified
- Git sync is safer
- cleanup is safer
- logs are safer
- large input handling is more stable
- user-facing failures are clearer and actionable
## Final Takeaway
The backend is no longer a fragile prototype.
It is now a deterministic, safe, self-healing knowledge engine that supports the core product behavior:
Paste anything → preview → confirm → save safely → compile into usable knowledge.

---
## Compiled Wiki
- WIKI: [[WIKI/architecture/aiagentnerd-backend-hardening-summary]]
- Last compiled: 2026-05-05T06:56:28.221Z
