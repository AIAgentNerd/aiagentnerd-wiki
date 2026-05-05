---
title: Openwebui Aiagentnerd Deck Overview A0406524 3bbe 49e3 98d1 Ee61d815d504
source_raw: RAW/openwebui/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504.md
compiled_wiki_path: WIKI/architecture/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504.md
compiled_at: 2026-05-05T06:50:26.101Z
type: system-note
tags: [aiagentnerd, compiled, architecture, deck, overview, a0406524, 3bbe, 49e3]
---

# Openwebui Aiagentnerd Deck Overview A0406524 3bbe 49e3 98d1 Ee61d815d504

## Summary
Deck is the operational dashboard of the AiAgentNerd system, a single-page web app accessible at `deck.aiagentnerd.com`. It provides real-time monitoring and management of the entire multi-agent ecosystem, allowing operators to oversee and control various aspects of the system.

## Key Concepts
- **Deck**: The primary operational dashboard for AiAgentNerd.
- **User Panel**: Lists users, shows active task counts, and allows filtering.
- **Agent Office View**: Visual representation of all agents, showing current tasks, status, and models in use.
- **Task Panel**: Displays active and queued tasks with task ID, type, user, and status, and includes admin controls to stop or retry tasks.
- **Activity Feed (Ship Log)**: Chronological log of system events, agent actions, and error messages.
- **System Monitoring**: Provides CPU, memory, health, and runtime alerts.

## Practical Use
- **Monitoring**: Use Deck to observe the overall state of the system, including user activity, agent tasks, and system health.
- **Task Management**: Admins can stop or retry tasks directly from the Task Panel.
- **User Management**: Filter tasks by user and view active task counts.
- **Real-Time Updates**: Deck updates in real-time via polling or WebSocket, ensuring operators have the latest information.
- **System Health**: Monitor CPU, memory, and runtime alerts to identify and address potential issues.

## Implementation Notes
- **Data Consumption**: Deck consumes structured data for users, agents, tasks, activity, and system status.
- **Interaction**: Clicking on an agent reveals its current task, clicking on a user filters tasks, and clicking on a task opens detailed information.
- **Real-Time Updates**: Real-time updates are achieved through polling or WebSocket connections.
- **Role**: Deck serves as the primary control interface and visualization layer for Hermes task execution, providing operators with a clear entry point into the system.

## Related
- [[aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504]]
- [[acr-overview-da74bd9b-66f7-4705-a7f5-11c50645f812]]
- [[acr-overview-da74bd9b-66f7-4705-a7f5-11c50645f812]]
- [[cleanup-knowledge-about-deck-deeec384-5ce3-477e-884a-aff13904a4ad]]
- [[deck]]

## Source
- RAW: [[RAW/openwebui/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504]]
