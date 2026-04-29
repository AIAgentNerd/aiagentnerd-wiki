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
Deck is the primary control interface for the AiAgentNerd multi-agent system, previously known as the Agent Control Room (ACR). It centralizes agent visualization, task monitoring, user management, and system activity observation, providing a single operational dashboard for the system operator.

## Key Concepts
- **Deck**: The rebranded control interface of AiAgentNerd, replacing the earlier ACR name.
- **Centralized oversight**: Single interface for seeing agents, tasks, users, and system logs.
- **Four core functions**:
  - Visualize agents
  - Monitor tasks
  - Manage users
  - Observe system activity
- **Metaphor**: AiAgentNerd as a ship; Deck is the control surface where the operator commands the crew (agents) and tracks missions (tasks) via the ship log (activity feed).

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
