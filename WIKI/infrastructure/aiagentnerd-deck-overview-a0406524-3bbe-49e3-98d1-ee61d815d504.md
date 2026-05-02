---
title: Openwebui Aiagentnerd Deck Overview A0406524 3bbe 49e3 98d1 Ee61d815d504
source_raw: RAW/openwebui/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504.md
compiled_wiki_path: WIKI/infrastructure/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504.md
compiled_at: 2026-05-02T19:49:17.896Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, deck, overview, a0406524, 3bbe, 49e3]
---

# Openwebui Aiagentnerd Deck Overview A0406524 3bbe 49e3 98d1 Ee61d815d504

## Summary
Deck is the operational dashboard of the AiAgentNerd system, a single-page web application at `deck.aiagentnerd.com`. It provides real-time monitoring and management of the entire multi-agent crew, serving as the primary control interface and visualization layer for Hermes task execution.

## Key Concepts
- **Five-panel layout**: User Panel, Agent Office View, Task Panel, Activity Feed (Ship Log), System Monitoring.
- **Agent Office View**: Visual representation of all agents showing current task, status, and model; primary interaction area.
- **Task Panel**: Lists active and queued tasks with admin controls (stop/retry).
- **Activity Feed**: Chronological log of system events, agent actions, and errors.
- **System Monitoring**: CPU, memory, health, and runtime alerts.
- **Data model**: Consumes structured data for users, agents, tasks, activity, and system status.
- **Interaction**: Click agent to view task, click user to filter tasks, click task for details; admins can stop/retry tasks.
- **Real-time updates**: Via polling or WebSocket, streaming task states and agent activity live.

## Practical Use
- Operators use Deck to monitor the health and activity of the AiAgentNerd multi-agent system.
- Accessible at `deck.aiagentnerd.com`.
- Provides a visual overview of all agents and their current workloads.
- Enables direct task management (stop/retry) from the interface.
- Acts as the entry point for system operators to interact with Hermes task execution.

## Implementation Notes
- Single-page web application.
- Real-time updates implemented via polling or WebSocket.
- Consumes structured data endpoints (users, agents, tasks, activity, system_status).
- URL: `deck.aiagentnerd.com`.

## Related
- [[acr-overview-da74bd9b-66f7-4705-a7f5-11c50645f812]]
- [[deck]]
- [[deck]]
- [[acr-dashboard-ui-b5cd7aa5-335b-4342-8461-29717600d1fa]]
- [[agent-control-room-acr-fb05e0f0-c846-45b2-9728-dd7bd55af8ca]]

## Source
- RAW: [[RAW/openwebui/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504]]
