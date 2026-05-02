# 🖥️ AiAgentNerd Deck Overview

source: openwebui
openwebui_chat_id: a0406524-3bbe-49e3-98d1-ee61d815d504
created_at: 1777541551
updated_at: 1777541655
exported_at: 2026-05-03T02:45:01.903174

---

## USER

tell me about deck by aiagentnerd

## ASSISTANT

Deck is the operational dashboard of the AiAgentNerd system — a single‑page web app at `deck.aiagentnerd.com`. It lets you monitor and manage the entire multi‑agent crew in real time.

**Layout** – Deck consists of five panels:

1. **User Panel** – lists users, shows active task counts, and allows filtering.
2. **Agent Office View** – visual representation of all agents; you see each agent’s current task, status, and the model it’s using. This is the primary interaction area.
3. **Task Panel** – shows active and queued tasks (task ID, type, user, status) with admin controls to stop/retry.
4. **Activity Feed (Ship Log)** – chronological log of system events, agent actions, and error messages.
5. **System Monitoring** – CPU, memory, health, and runtime alerts.

**Data & Interaction** – Deck consumes structured data (users, agents, tasks, activity, and system status). Clicking an agent reveals its current task, clicking a user filters tasks, and clicking a task opens details. Admins can stop or retry jobs directly from the interface.

**Real‑Time Behaviour** – Updates come via polling or WebSocket, so task states and agent activity stream in live.

**Role** – Deck is the primary control interface and visualization layer for Hermes task execution, giving operators a clear entry point into the system.

---
## Compiled Wiki
- WIKI: [[WIKI/infrastructure/aiagentnerd-deck-overview-a0406524-3bbe-49e3-98d1-ee61d815d504]]
- Last compiled: 2026-05-02T19:49:17.896Z
