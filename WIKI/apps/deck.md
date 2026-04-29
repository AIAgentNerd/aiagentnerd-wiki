---
title: Concepts Deck
source_raw: RAW/concepts/deck.md
compiled_wiki_path: WIKI/apps/deck.md
compiled_at: 2026-04-29T13:55:00.746Z
type: system-note
tags: [aiagentnerd, compiled, apps, deck]
---

# Concepts Deck

## Summary
Deck is the control interface for the AiAgentNerd system, previously known as the Agent Control Room (ACR). It provides a unified dashboard to visualize agents, monitor tasks, manage users, and observe real-time system activity. The design follows a ship metaphor: AiAgentNerd is the ship, Deck is the bridge, agents are the crew, tasks are missions, and activity is the ship log.

## Key Concepts
- **Deck**: Central control surface for the multi-agent system.
- **Agent visualization**: View all agents and their current status.
- **Task monitoring**: Track active and queued tasks.
- **User management**: Administer system users and permissions.
- **Activity observation**: Chronological feed of system events and agent actions.
- **Ship metaphor**: `AiAgentNerd = ship`, `Deck = control surface`, `agents = crew`, `tasks = missions`, `activity = ship log`.

## Practical Use
- Operators use Deck to gain a single-pane-of-glass view of agent health, task backlogs, and system-wide activity.
- It consolidates operational oversight, reducing the need to inspect multiple logs or databases.
- Likely provides manual intervention capabilities for starting, stopping, or reconfiguring agent operations.

## Implementation Notes
- Formerly named ACR (Agent Control Room); renamed to Deck to align with the ship metaphor.
- Presumed to be a web-based internal dashboard with panels for agents, tasks, users, and an activity feed.
- Requires integration with the backend agent orchestration and task execution systems.
- Likely depends on real-time updates (WebSocket or polling) to reflect agent state and task progress.

## Related
- [[deck]]
- [[acr]]
- [[x-post-app]]

## Source
- RAW: [[RAW/concepts/deck]]
