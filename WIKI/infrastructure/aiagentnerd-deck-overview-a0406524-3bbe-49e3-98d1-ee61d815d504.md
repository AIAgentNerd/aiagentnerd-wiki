---
title: Openwebui Aiagentnerd Deck Overview A0406524 3bbe 49e3 98d1 Ee61d815d504
source_raw: RAW/openwebui/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504.md
compiled_wiki_path: WIKI/infrastructure/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504.md
compiled_at: 2026-04-30T19:49:41.432Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, deck, overview, a0406524, 3bbe, 49e3]
---

# Openwebui Aiagentnerd Deck Overview A0406524 3bbe 49e3 98d1 Ee61d815d504

## Summary
Deck is the operational dashboard of the AiAgentNerd system, a single-page web application accessible at `deck.aiagentnerd.com`. It provides real-time monitoring and management of the multi-agent crew, serving as the primary control interface and visualization layer for Hermes task execution.

## Key Concepts
- **Five-Panel Layout**: User Panel, Agent Office View, Task Panel, Activity Feed (Ship Log), System Monitoring.
- **Agent Office View**: Central interaction area showing each agent’s current task, status, and model.
- **Task Panel**: Lists active/queued tasks with admin controls (stop/retry).
- **Activity Feed**: Chronological log of system events, agent actions, and errors.
- **System Monitoring**: Displays CPU, memory, health, and runtime alerts.
- **Structured Data Model**: Consumes `users[]`, `agents[]`, `tasks[]`, `activity[]`, `system_status`.
- **Real-Time Updates**: Via polling or WebSocket for live task states and agent activity.

## Practical Use
- Operators use Deck to monitor the entire agent system in real time.
- Click an agent to view its current task; click a user to filter tasks; click a task to open details.
- Admins can stop or retry tasks directly from the Task Panel.
- The Activity Feed provides a chronological audit trail of system events and errors.
- System Monitoring panel gives at-a-glance health and resource usage.

## Implementation Notes
- **URL**: `deck.aiagentnerd.com`
- **Data Consumption**: Structured JSON-like data for users, agents, tasks, activity, and system status.
- **Real-Time Mechanism**: Polling or WebSocket (exact implementation not specified in source).
- **Interaction Model**: Click-based navigation; admin controls for task lifecycle management.
- **Role**: Primary control interface and visualization layer for Hermes task execution.

## Related
- [[acr-overview-da74bd9b-66f7-4705-a7f5-11c50645f812]]
- [[deck]]
- [[deck]]
- [[acr-dashboard-ui-b5cd7aa5-335b-4342-8461-29717600d1fa]]
- [[agent-control-room-acr-fb05e0f0-c846-45b2-9728-dd7bd55af8ca]]

## Source
- RAW: [[RAW/openwebui/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504]]
