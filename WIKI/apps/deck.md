---
title: Concepts Deck
source_raw: RAW/concepts/deck.md
compiled_wiki_path: WIKI/apps/deck.md
compiled_at: 2026-04-29T13:55:00.746Z
type: system-note
tags: [aiagentnerd, compiled, apps, deck]
---

# Concepts Deck

# App: Deck

## Summary
Deck is the operational interface of AiAgentNerd used to monitor, manage, and interact with the multi-agent system in real time.

It is implemented as a web-based internal dashboard accessible via:
deck.aiagentnerd.com

---

## Core Layout

Deck is a single-page dashboard composed of five main panels:

1. **User Panel**
   - Displays system users
   - Shows active task counts per user
   - Allows filtering by user

2. **Agent Office View**
   - Visual representation of all agents (crew)
   - Shows current task, status, and model
   - Primary interaction area

3. **Task Panel**
   - Lists active and queued tasks
   - Displays task ID, type, user, status
   - Allows admin control (stop/retry)

4. **Activity Feed (Ship Log)**
   - Chronological log of system events
   - Agent actions, task updates, errors

5. **System Monitoring Panel**
   - CPU, memory, and system health
   - Alerts and runtime status

---

## Data Model (Simplified)

Deck consumes structured data:

- users[]
- agents[]
- tasks[]
- activity[]
- system_status

---

## Interaction Model

- Click agent → view current task
- Click user → filter tasks
- Click task → open task details
- Admin controls → stop / retry tasks

---

## Real-Time Behavior

Deck updates via:

- polling or WebSocket
- live task updates
- agent state changes
- activity stream updates

---

## Role in System

Deck acts as:

- the primary control interface for AiAgentNerd
- the visualization layer of Hermes task execution
- the operator’s entry point into the system

## Related
- [[concepts/deck]]

## Source
- RAW: [[RAW/concepts/deck]]
