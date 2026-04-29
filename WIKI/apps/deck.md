---
title: Concepts Deck
source_raw: RAW/concepts/deck.md
compiled_wiki_path: WIKI/apps/deck.md
compiled_at: 2026-04-29T14:44:00.211Z
type: system-note
tags: [aiagentnerd, compiled, apps, deck]
---

# Concepts Deck

## Summary
Deck is the central control interface for the AiAgentNerd system, designed to unify agent visualization, task monitoring, user management, and activity observation. It follows a ship metaphor where Deck represents the bridge from which operations are coordinated.

## Key Concepts
- **Deck**: The primary operational dashboard for the multi‑agent system
- **Agent visualization**: View all agents and their statuses
- **Task monitoring**: Track active, queued, and completed tasks
- **User management**: Administer system users and permissions
- **Activity observation**: Chronological feed of system events and agent actions
- **Ship metaphor**: `AiAgentNerd` = ship, `Deck` = control surface, `agents` = crew, `tasks` = missions, `activity` = ship log

## Practical Use
- Operators use Deck to get a single‑pane‑of‑glass view of the entire agent system
- It consolidates monitoring, reducing the need to inspect multiple logs or databases
- Likely provides manual intervention capabilities such as starting, stopping, or reconfiguring agent operations

## Implementation Notes
- No technical architecture is detailed in the source note
- Presumes a web‑based internal dashboard with panels for agents, tasks, users, and an activity feed
- Requires integration with the backend agent orchestration and task execution layers
- Probably depends on real‑time updates (WebSockets or polling) to reflect live state

## Related
- [[deck]]
- [[x-post-app]]

## Source
- RAW: [[RAW/concepts/deck]]
