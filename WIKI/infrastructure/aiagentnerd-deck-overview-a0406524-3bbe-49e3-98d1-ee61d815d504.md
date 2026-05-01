---
title: Openwebui Aiagentnerd Deck Overview A0406524 3bbe 49e3 98d1 Ee61d815d504
source_raw: RAW/openwebui/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504.md
compiled_wiki_path: WIKI/infrastructure/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504.md
compiled_at: 2026-05-01T19:48:03.052Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, deck, overview, a0406524, 3bbe, 49e3]
---

# Openwebui Aiagentnerd Deck Overview A0406524 3bbe 49e3 98d1 Ee61d815d504

## Summary
AiAgentNerd Deck is the operational dashboard for the multi-agent system, accessible as a single-page web app at `deck.aiagentnerd.com`. It provides real-time monitoring and management of agents, tasks, and system health, acting as the primary control interface for Hermes task execution.

## Key Concepts
- **Single-Page Dashboard**: Web app running at `deck.aiagentnerd.com`.
- **Five Panels**:
  1. **User Panel**: Lists users, active task counts, and supports filtering by user.
  2. **Agent Office View**: Visual representation of all agents, showing current task, status, and assigned model. Primary interaction area.
  3. **Task Panel**: Active and queued tasks with ID, type, user, status; includes admin controls to stop/retry tasks.
  4. **Activity Feed (Ship Log)**: Chronological log of system events, agent actions, and errors.
  5. **System Monitoring**: CPU, memory, health, and runtime alerts.
- **Structured Data Consumption**: Deck consumes JSON-like data containing `users`, `agents`, `tasks`, `activity`, and `system_status`.
- **Interaction Model**: Click agent to view current task; click user to filter tasks; click task for details; admins can stop/retry tasks directly.
- **Real-Time Updates**: Updates are delivered via polling or WebSocket, enabling live stream of agent states and activity.

## Practical Use
- Operators use Deck to monitor agent states and task pipelines in real time.
- Admins can intervene on stuck or failing tasks using the stop/retry controls.
- The activity feed provides an audit trail for debugging and oversight.
- Deck reduces the need to SSH into the server for routine status checks.

## Implementation Notes
- **URL**: `deck.aiagentnerd.com`
- **Data format**: Structured objects (users, agents, tasks, activity, system_status).
- **Update mechanism**: Polling or WebSocket (exact implementation depends on backend setup).
- **Agent credentials**: The interface does not directly expose model keys; agent routing is handled internally (see [[model-routing-reliability]]).
- No database or API details provided in this overview.

## Related
- [[acr-overview-da74bd9b-66f7-4705-a7f5-11c50645f812]]
- [[deck]]
- [[deck]]
- [[acr-dashboard-ui-b5cd7aa5-335b-4342-8461-29717600d1fa]]
- [[agent-control-room-acr-fb05e0f0-c846-45b2-9728-dd7bd55af8ca]]

## Source
- RAW: [[RAW/openwebui/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504]]
