---
title: Concepts Deck
source_raw: RAW/concepts/deck.md
compiled_wiki_path: WIKI/concepts/deck.md
compiled_at: 2026-04-29T13:53:16.388Z
type: concept
tags: [aiagentnerd, compiled, concepts, deck]
---

# Concepts Deck

## Summary
Deck is the primary control interface for the AiAgentNerd multi-agent system.

It provides a unified operational view to visualize agents, monitor tasks, manage users, and observe real-time system activity.

The design follows a ship metaphor:
- AiAgentNerd = the ship
- Deck = the control surface
- agents = the crew
- tasks = missions
- activity feed = the ship log
- system monitoring = ship status

## Key Concepts
- **Deck**: Central control interface for the AiAgentNerd system
- **Centralized oversight**: Single interface for agents, tasks, users, and system activity
- **Agent visualization**: Real-time view of all agents and their status
- **Task monitoring**: Active and queued task tracking
- **User management**: Control of system users and permissions
- **System activity**: Chronological event stream (ship log)

## Practical Use
- Operators use Deck to monitor agent status, task progress, and system health in real time.
- It serves as the touchpoint for manual intervention when automated workflows need adjustment.
- All recent system activity is visible, reducing the need to inspect separate logs or databases.

## Implementation Notes
- Inherits the design of the former ACR; likely maintains the same panel layout: User panel, Agent office view, Task panel, Activity feed, and System monitoring panel.
- The exact UI implementation may be a web-based internal tool with real-time updates (WebSocket or polling).
- Refer to [[acr]] for detailed panel descriptions and previous design notes.

## Related
- [[acr]]
- [[aiagentnerd-master-notes]]
- [[auto-test]]
- [[empty-test]]
- [[karpathy-llm-wiki-test]]

## Source
- RAW: [[RAW/concepts/deck]]
