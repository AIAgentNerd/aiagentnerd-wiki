---
title: Hermes Native Memory System Architecture
type: wiki
category: architecture
source_raw: RAW/architecture/hermes-native-memory-architecture-md.md
compiled_at: "2026-05-11 20:00:03"
---

# Hermes Native Memory System Architecture

## Summary

This WIKI note was compiled from a RAW source by the Hermes-native memory profile.

## Key Knowledge

# Hermes-Native Memory System — Full Architecture & Feature Documentation

Overview
This document describes the completed migration of the AiAgentNerd knowledge and memory system from the legacy server.js orchestration layer into a fully Hermes-native architecture built around:
•	Hermes Workspace 
•	Hermes profiles 
•	MCP tools 
•	filesystem-based RAW/WIKI knowledge 
•	deterministic metadata regeneration 
•	Git-based synchronization 
•	Workspace-native memory ingestion 
The migration removed dependency on:
•	OpenWebUI 
•	legacy export cron jobs 
•	OpenRouter-based wiki compile daemons 
•	PM2 server.js orchestration 
•	hidden compile loops and model routing 
The new architecture is modular, deterministic, and fully owned by the Hermes Memory profile.
________________________________________
High-Level Architecture
Current Runtime Stack
Workspace
↓
Hermes Runtime
↓
Memory Profile
↓
MCP Tools / Skills
↓
RAW Knowledge Store
↓
Hermes-native Compile
↓
Metadata Regeneration
↓
Git Sync
↓
GitHub Repo
↓
Obsidian Pull/Sync
________________________________________
Core Philosophy
Source of Truth
The Hermes server is now the source of truth.
Primary storage location:
/home/nerd/aiagentnerd-wiki
GitHub and Obsidian are synchronization/mirror layers, not the primary runtime memory.
________________________________________
RAW / WIKI Knowledge Architecture
RAW Layer
Purpose:
•	source material 
•	drafts 
•	transcripts 
•	workspace snapshots 
•	imported notes 
•	unstructured knowledge 
Location:
RAW/<category>/
Examples:
RAW/concepts/deck.md
RAW/workspace/workspace-session-....
RAW/architecture/...
RAW is editable and may contain:
•	frontmatter 
•	merge markers 
•	source references 
•	workspace snapshots 
•	large chunked imports 
________________________________________
WIKI Layer
Purpose:
•	compiled knowledge 
•	canonicalized reference notes 
•	readable structured knowledge 
Location:
WIKI/<category>/
Examples:
WIKI/concepts/deck.md
WIKI/architecture/...
WIKI files are generated from RAW.
________________________________________
Hermes-Native Compile System
compile_wiki.sh
Location:
~/.hermes/profiles/memory/bin/compile_wiki.sh
Responsibilities:
•	RAW → WIKI compilation 
•	metadata injection 
•	source tracking 
•	deterministic generation 
•	category placement 
The compile system:
•	does NOT use server.js 
•	does NOT use OpenRouter 
•	does NOT use OpenWebUI 
•	does NOT require PM2 daemon orchestration 
________________________________________
Compile Output Features
Generated WIKI files include:
•	title 
•	category 
•	source_raw reference 
•	compiled timestamp 
•	summary section 
•	tags 
Example metadata:
________________________________________
Hermes-Native Metadata Regeneration
wiki_metadata.py
Location:
~/.hermes/profiles/memory/lib/wiki_metadata.py
Responsibilities:
•	regenerate indexes 
•	regenerate manifests 
•	regenerate category indexes 
•	update wiki metadata 
•	maintain generated sections safely 
________________________________________
Generated Metadata
Root Index
index.md
Category Indexes
Examples:
WIKI/concepts/index.md
WIKI/architecture/index.md
WIKI/services/index.md
Manifest Tracking
Location:
system/manifests/compiled-files.json
Tracks:
•	rawPath 
•	wikiPath 
•	category 
•	title 
•	compiled_at 
•	updated_at 
________________________________________
Generated Section Safety
Generated index regions are wrapped in markers:
<!-- BEGIN HERMES GENERATED INDEX -->
<!-- END HERMES GENERATED INDEX -->
This allows preservation of manual content outside generated regions.
________________________________________
Git Synchronization System
sync_wiki_git.sh
Location:
~/.hermes/profiles/memory/bin/sync_wiki_git.sh
Responsibilities:
•	git pull 
•	git add 
•	git commit 
•	git push 
Stages:
•	RAW 
•	WIKI 
•	system 
•	index.md 
•	topic-brains.md 
•	log.md 
No server.js dependency.
________________________________________
Workspace-Native Session Snapshots
export_workspace_session_snapshot
MCP Tool:
mcp_search_knowledge_export_workspace_session_snapshot
Purpose:
•	save Workspace conversations as source material 
•	replace old OpenWebUI export system 
Output location:
RAW/workspace/
Example filename:
workspace-session-2026-05-11-1900-hermes-native-migration-test.md
________________________________........... (truncated)

## Source

- RAW: [[RAW/architecture/hermes-native-memory-architecture-md.md]]

## Tags

#aiagentnerd #hermes #memory #wiki
