---
title: Concepts Deck
source_raw: RAW/concepts/deck.md
compiled_wiki_path: WIKI/services/deck.md
compiled_at: 2026-04-29T14:54:14.562Z
type: system-note
tags: [aiagentnerd, compiled, services, deck, queue, hermes]
---

# Concepts Deck

## Summary
Deck is the primary control interface for the AiAgentNerd multi-agent system. It unifies agent visualization, task monitoring, user management, and real-time system activity logs into a single operational surface. As the visualization layer of Hermes task execution, it serves as the operator’s entry point into the system.

## Key Concepts
- **Ship metaphor**: AiAgentNerd = the ship, Deck = the control interface, agents = crew, tasks = missions, activity feed = the ship log, system monitoring = ship status.
- **Agent visualization**: Real-time display of all agents and their current status.
- **Task monitoring**: Tracking of active and queued tasks.
- **User management**: Control over users and permissions.
- **System activity observation**: Chronological event stream of all system actions.

## Practical Use
Deck is used as the day‑to‑day operational interface for the AiAgentNerd system. Operators interact with it to:
- View which agents are online, what they are currently doing, and their health.
- See active and queued tasks, including their owners and statuses.
- Manage system users and permissions.
- Inspect the chronological activity log to understand what happened when and to diagnose issues.

## Implementation Notes
Deck is tightly integrated with the Hermes orchestration layer; it acts as the visualization surface for Hermes task execution. The RAW note does not specify the technology stack, endpoints, or deployment details beyond its role.

## Related
- [[hermes-setup]]
- [[deck]]
- [[deck]]
- [[backlink-test]]
- [[hermes-setup]]

## Source
- RAW: [[RAW/concepts/deck]]
