# Codex + Hermes + Obsidian Wiki — Complete Setup & Workflow Guide
#workflow #codex #hermes #memory #aiagentnerd

## Sections

- [[#Part 1 Codex Setup & Usage (VS Code + Server)]]
- [[#Part 2 Codex + Hermes + Obsidian Wiki]]

---

# 🧠 Part 1: Codex Setup & Usage (VS Code + Server)

## Overview

Codex is an **AI coding agent inside your terminal**.

It does NOT replace ChatGPT. Instead:

- ChatGPT → planning, architecture, explanations
    
- Codex → execution, file edits, implementation
    

---

## 1. Connect VS Code to Your Server

1. Open **VS Code**
    
2. Click bottom-left green icon
    
3. Select **Connect to Host**
    
4. Choose:
    

```
nerd@nerd-server
```

5. Open folder:
    

```
/home/nerd/aiagentnerd
```

---

## 2. Open Terminal (on server)

In VS Code:

```
Terminal → New Terminal
```

You should see:

```
nerd@nerd-server:~/aiagentnerd$
```

---

## 3. Install Codex

```bash
npm i -g @openai/codex
```

---

## 4. Start Codex

```bash
cd ~/aiagentnerd
codex
```

Important:

👉 ALWAYS start Codex inside your project folder

---

## 5. Exit Codex

```bash
exit
```

---

## 6. How Codex Works

Codex:

- reads your codebase
    
- explains structure
    
- proposes plans
    
- asks permission to run commands
    
- edits files
    

👉 You talk to it in **normal language**

---

## 7. Prompting Codex (VERY IMPORTANT)

### ❌ Weak prompts

- “how do I fix this?”
    
- “what is this?”
    

### ✅ Strong prompts

```
[Goal]

Constraints:
- ...
- ...

First explain the plan.
Then implement.
Afterwards show how to test.
```

---

### Example (real)

```
Implement compile logging for the Obsidian wiki flow.

Constraints:
- modify only server.js
- append to ~/aiagentnerd-wiki/log.md
- keep API unchanged

First explain the plan.
Then implement.
Then show how to test with curl.
```

---

## 8. Safe Approval Rules

### ✅ Usually safe

- read files
    
- list directories
    
- syntax checks (node -c)
    

### ⚠️ Review carefully

- file edits
    
- unsandboxed execution
    
- restarting services
    

---

## 9. Your Proven Workflow

### Step 1 — Start Codex

```bash
cd ~/aiagentnerd
codex
```

---

### Step 2 — Inspect

```
Explain this codebase and the wiki compile flow. Do not change anything.
```

---

### Step 3 — Plan

```
Propose a minimal logging feature.
Do not implement yet.
```

---

### Step 4 — Implement

```
Proceed with implementation.
Modify only server.js.
Append logs to log.md.
```

---

### Step 5 — Test

```bash
curl -X POST http://127.0.0.1:3100/api/wiki/compile-raw \
  -H "Content-Type: application/json" \
  -d '{ ... }'
```

---

### Step 6 — Restart if needed

```bash
pm2 restart hermes
```

---

### Step 7 — Verify

```bash
tail -n 15 ~/aiagentnerd-wiki/log.md
```

---

## 10. Key Codex Rules

- always inspect first
    
- always ask for a plan
    
- keep changes minimal
    
- test everything
    
- restart backend if needed
    

---

# 🧠 Part 2: Codex + Hermes + Obsidian Wiki (Shared Memory System)

---

## 1. Core Idea

You are building:

> **AI system with shared external memory**

---

## 2. System Architecture

```
You (Obsidian UI)
        ↓
Obsidian Wiki (Memory)
        ↑        ↑
     Hermes    Codex
```

---

## 3. Components

### 🧠 Obsidian Wiki

Location:

```
~/aiagentnerd-wiki
```

Purpose:

- knowledge
    
- logs
    
- structured memory
    

---

### ⚙️ Hermes (Backend)

- runs on port 3100
    
- handles API
    
- compiles wiki
    
- reads memory
    

---

### 🤖 Codex

- edits backend code
    
- implements features
    
- writes logs
    

---

## 4. Wiki Structure

```
RAW/      → unprocessed content
WIKI/     → structured knowledge
log.md    → system memory
```

---

## 5. Compile Flow

```
RAW → LLM → WIKI → Git Push → Log
```

---

## 6. Logging System (IMPORTANT)

### Success

```
## <timestamp>
- action: compile_raw
- source: <rawPath>
- target: <wikiPath>
- result: success
```

---

### Failure

```
## <timestamp>
- action: compile_raw
- source: <rawPath>
- target: <wikiPath>
- result: failure
- error: <message>
```

---

## 7. Why This Matters

Your system can now:

- remember actions
    
- track failures
    
- debug history
    
- support multi-agent workflows
    

---

## 8. How Codex Links to Hermes

Codex modifies:

```
~/aiagentnerd/server.js
```

That file controls:

- wiki compile
    
- API routes
    
- logging
    

So:

👉 Codex → edits code  
👉 Hermes → executes logic  
👉 Wiki → stores memory

---

## 9. AGENTS.md (Recommended)

Create:

```
~/aiagentnerd/AGENTS.md
```

Example:

```
Shared memory:
~/aiagentnerd-wiki

Rules:
- append logs to log.md
- do not overwrite logs
- keep markdown readable

Backend:
- PM2 process: hermes
```

---

## 10. Real Workflow (Now Active)

### You

- add RAW content in Obsidian
    

### Hermes

- compiles via API
    

### Codex

- improves system logic
    

### Wiki

- stores result + logs
    

---

## 11. What This Unlocks

### 🔹 Debugging

“What failed yesterday?”

### 🔹 Automation

retry failed actions

### 🔹 Dashboards

mission control UI

### 🔹 Multi-agent systems

shared memory coordination

---

## 12. Key Principle

You are NOT building:

❌ AI with memory

You ARE building:

✅ System with shared file-based memory

---

## 13. Locked-in Commands

### Start Codex

```bash
cd ~/aiagentnerd
codex
```

### Exit Codex

```bash
exit
```

### Restart backend

```bash
pm2 restart hermes
```

### Test compile

```bash
curl -X POST http://127.0.0.1:3100/api/wiki/compile-raw ...
```

### Check logs

```bash
tail -n 20 ~/aiagentnerd-wiki/log.md
```

---

# 🚀 Final Summary

You now have:

- Codex → execution layer
    
- Hermes → orchestration layer
    
- Obsidian → memory layer
    
- log.md → system history
    

Core loop:

```
Plan → Execute → Log → Learn
```

---

This is your foundation for AiAgentNerd 🚀
