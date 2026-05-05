---
title: Openwebui Aiagentnerd Deck Overview A0406524 3bbe 49e3 98d1 Ee61d815d504
source_raw: RAW/openwebui/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504.md
compiled_wiki_path: WIKI/infrastructure/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504.md
compiled_at: 2026-05-03T19:47:14.698Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, deck, overview, a0406524, 3bbe, 49e3]
status: archived
archived_at: 2026-05-05T06:50:26.106Z
reclassified_to: architecture/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504.md
---

# Openwebui Aiagentnerd Deck Overview A0406524 3bbe 49e3 98d1 Ee61d815d504

## Summary
Deck is the operational single-page dashboard for the AiAgentNerd multi-agent system, hosted at `deck.aiagentnerd.com`. It provides real-time visualization and administrative control over agents, tasks, users, and system health. It serves as the primary human interface for monitoring Hermes task execution and managing crew operations.

## Key Concepts
- **Single-Page Dashboard**: A unified web interface that displays the full system state without page reloads.
- **Five-Panel Layout**: User Panel, Agent Office View, Task Panel, Activity Feed (Ship Log), and System Monitoring Panel.
- **Agent Office View**: Visual representation of the agent crew showing each agent’s current task, status, and active model.
- **Real-Time Transport**: Live updates delivered via polling or WebSocket.
- **Hermes Visualization Layer**: Deck renders backend task execution into an operator-friendly control surface.

## Practical Use
- Access the dashboard at `deck.aiagentnerd.com`.
- Use the **User Panel** to list users, view active task counts, and filter tasks by user.
- Use the **Agent Office View** to inspect agent status, current assignments, and which model each agent is using.
- Use the **Task Panel** to review active and queued tasks by ID, type, user, and status; admins can stop or retry jobs directly from the interface.
- Monitor CPU, memory, health metrics, and runtime alerts in the **System Monitoring Panel**.
- Review the **Activity Feed** for chronological system events, agent actions, and error messages.

## Implementation Notes
- Deck consumes a structured data model consisting of `users`, `agents`, `tasks`, `activity`, and `system_status`.
- Real-time behavior is implemented through polling or WebSocket connections.
- Admin controls in the Task Panel trigger stop/retry actions against backend jobs.
- The dashboard is the primary operator entry point and the main visualization layer for Hermes.

## Related
- [[acr-overview-da74bd9b-66f7-4705-a7f5-11c50645f812]]
- [[deck]]
- [[deck]]
- [[acr-dashboard-ui-b5cd7aa5-335b-4342-8461-29717600d1fa]]
- [[agent-control-room-acr-fb05e0f0-c846-45b2-9728-dd7bd55af8ca]]

## Source
- RAW: [[RAW/openwebui/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504]]
