**Karpathy LLM Wiki**

aiagentnerd, Karpathy LLM Wiki, chrome laptop, opera mobile

**[Prompts – Commands](#PromptsCommands)**

[Summary](#Summary)

Potential Names

[Dev Wiki alongside apps](#DevWikialongsideApps)

[Prompt by Alex Finn](#PromptAlexFinn)

**[Prompt adjusted for our Hermes](#PromptadjHermes)**

[TUTORIAL for setting up Obsidian Wiki](#TUTORIALWikiSetup)

[Connect Wiki to Hermes / server](#ConnectWikiServer)

[Why we set up everything manually, rather than just telling Hermes ?](#WhyManually)

How to use Docs with Obisidian

**Prompts – Commands**

**[Top](#top)**

Wiki on laptop – open powershell:

cd "C:\Users\Win11\OneDrive\Documents\AIAgentNerd-Wiki"

github: [https://github.com/AIAgentNerd/aiagentnerd-wiki](https://github.com/AIAgentNerd/aiagentnerd-wiki)

git remote set-url origin https://github.com/AiAgentNerd/aiagentnerd-wiki.git

git config user.name "AiAgentNerd"

git config user.email "aiagentnerd@gmail.com"

git remote set-url origin https://github.com/AiAgentNerd/aiagentnerd-wiki.git

git push -u origin main

Sync laptop with server via github:

## Then sync it

On laptop:

git add .  
git commit -m "Add raw vs wiki definition"  
git push

On server:

cd ~/aiagentnerd-wiki  
git pull

Then restart Hermes:

pm2 restart hermes

  **Vault name:** AIAgentNerd-Wiki

  **Root folder on laptop:** AIAgentNerd-Wiki

  **Root folder on server:** ~/aiagentnerd-wiki

Compile and generate output

# 🧠 Rule to remember  
  
- ```bash → starts code block  
- ``` → ends code block👉 Anything inside = code👉 Anything outside = real note content

**Summary:**

[Top](#top)

**Karpathy-Style LLM Wiki — Summary**

**🎯** **Goal**

Build a **structured, chapter-based knowledge system** that captures everything you’re learning while building TaskNerd.

Instead of scattered chats, you create a:

Personal + Product Knowledge Wiki

That can later become:

- your internal playbook
- your system documentation
- potentially a public learning resource

---

**🧭** **What this wiki should contain**

Your wiki should be organized into **clear chapters**, for example:

01 - SSH & VS Code  
02 - Tailscale  
03 - Hermes Basics  
04 - OpenRouter & Models  
05 - X Post App  
06 - Multi-Agent Routing  
07 - Cloudflare & Domain  
08 - PM2 & Processes  
09 - Debugging Cheatsheet  
10 - System Architecture

---

**🧠** **Structure of each chapter (VERY important)**

Each chapter should follow the same format:

**1. What it is**

Simple explanation in plain language.

**2. Why it matters**

Why this concept is important in your system.

**3. How we set it up**

Step-by-step commands and actions.

**4. Common errors**

Real problems you encountered.

**5. How we fixed them**

Actual solutions (this is gold).

**6. Final setup (your standard)**

What you decided to use going forward.

---

**💡** **Add a glossary (highly recommended)**

Create a file like:

00-glossary.md

Include simple definitions for:

- SSH
- localhost
- port
- API
- route
- PM2
- process
- proxy
- subdomain
- cron job
- model
- prompt
- agent

👉 This reduces confusion massively over time.

---

**🛠****️ How to build it (best approach)**

**✅** **Start simple (recommended)**

Use:

Markdown files (.md)

- create a folder:

~/tasknerd-wiki

- edit in VS Code
- no extra setup needed

👉 fastest and lowest friction

---

**🚀** **Upgrade later (optional)**

Once you have content, turn it into a docs site using:

- Docusaurus
- Nextra
- MkDocs

This gives you:

- navigation sidebar
- search
- clean UI

But only after content exists.

---

**🧠** **What makes it “Karpathy-style”**

Not just commands — but understanding.

Each chapter should include:

- concepts (what things mean)
- mental models (how pieces fit together)
- simple explanations
- practical steps
- real debugging stories

👉 It should teach, not just document.

---

**🔥** **Why this is powerful for you**

Right now:

- knowledge is scattered across chats
- steps are easy to forget
- concepts get mixed

This wiki turns that into:

Clear → Structured → Reusable → Scalable knowledge

---

**🚀** **Future potential**

This wiki can later become:

- internal TaskNerd documentation
- onboarding material for users
- content for X posts
- a public “learn AI agents” resource
- input for your agents (Atlas / Drift)

---

**🧭** **Best next step**

In your new chat, start with:

“Help me design my TaskNerd LLM wiki structure”

Then we can:

- define exact chapter list
- create first 2–3 files together
- standardize formatting
- begin filling content

---

If you build this alongside your syst

**Potential Names**

[Top](#top)

**1. “Brain / Intelligence” Focus (strongest fit)**

These align directly with your core concept:

**🔹** **Clean & brandable**

- **TopicBrain.ai**
- **BrainTopics.com**
- **MyTopicBrain.com**
- **BrainForge.ai** _(nice tie-in with Forge agent)_
- **BrainNest.ai**
- **BrainStack.ai**
- **BrainLayer.ai**

**🔹** **More premium / product-feel**

- **SecondBrainAI.com**
- **PersonalBrain.ai**
- **BrainVault.ai**
- **BrainBase.ai**
- **BrainFlow.ai**

👉 These clearly communicate: _this is your intelligence system_

---

**🧩** **2. “Knowledge / Research System” Angle**

More professional, slightly less “AI hype”

**🔹** **Strong options**

- **KnowledgeHub.ai**
- **ResearchNerd.ai** _(fits your brand system)_
- **InsightBase.ai**
- **InsightHub.ai**
- **SignalBase.ai** ⭐ (very strong)
- **SignalHub.ai**
- **DeepTopics.ai**

👉 “Signal” is especially good (signal vs noise concept)

---

**🚀** **3. “Future / Sci-Fi” Feel (very TaskNerd-compatible)**

Feels like a system, not a tool.

**🔹** **Strong + memorable**

- **NeuroBase.ai**
- **NeuroVault.ai**
- **CortexHub.ai**
- **SynapseAI.com**
- **SynapseBase.ai**
- **MindMesh.ai**
- **MindGrid.ai** ⭐

👉 These feel like infrastructure for intelligence

---

**🧠** **4. “Topic-Centric” (closest to your original idea)**

**🔹** **Clean + descriptive**

- **TopicVault.ai**
- **TopicBase.ai**
- **TopicHub.ai**
- **TopicStack.ai**
- **TopicFlow.ai**
- **TopicNest.ai**

👉 Very clear, but slightly less “wow” factor

---

**🔥** **5. “Own Your Intelligence” Positioning (very powerful)**

These lean into your philosophy:

- **OwnYourBrain.ai**
- **OwnYourData.ai**
- **OpenBrain.ai**
- **FreeYourData.ai**
- **PortableBrain.ai**
- **BrainExport.ai**

👉 Great for differentiation, slightly more niche

---

**🧬** **6. Hybrid (my favorite category for YOU)**

These balance:

- brandability
- meaning
- future expansion

**⭐** **Top picks for your vision**

- **SignalBase.ai** ← VERY strong (signal vs noise, scalable)
- **MindGrid.ai** ← feels like a system
- **BrainVault.ai** ← strong + clear value
- **TopicVault.ai** ← simple + powerful
- **NeuroBase.ai** ← futuristic but grounded
- **InsightStack.ai** ← product-like
- **CortexHub.ai** ← premium feel

---

**🧠** **My honest recommendation**

For your direction (agents + research + X automation):

**🥇** **Best overall:**

👉 **SignalBase.ai**

Why:

- “signal vs noise” = perfect for content + research
- works for individuals AND teams
- not limiting (can expand beyond topics)
- feels like infrastructure, not a gimmick

---

**🥈** **Best futuristic:**

👉 **MindGrid.ai**

Feels like:

interconnected intelligence system

---

**🥉** **Best simple + clear:**

👉 **TopicVault.ai**

Easy to understand immediately.

**Dev Wiki alongside apps**

[Top](#top)

Question: how should we proceed from here? Focus only on advancing the x post app, or start the wiki, or do it alongside each other ?

Great question — this is exactly where a lot of people either accelerate fast… or get stuck juggling too much.

Short answer first:

👉 **Do both — but asymmetrically**

- **80% focus:** keep advancing the X post app
- **20% effort:** build the Obsidian wiki _as you go_

Not 50/50. Not separate phases.  
👉 The wiki should **follow the build**, not replace it.

---

**🧭** **Why this is the best approach**

**❌** **If you ONLY build the app**

- you move fast
- but forget half of what you did
- things get messy
- hard to reuse later

**❌** **If you ONLY build the wiki**

- feels productive
- but no real system evolves
- you stall

**✅** **If you do BOTH (correctly)**

- build momentum **and** clarity
- everything compounds
- your system becomes teachable + reusable

---

**🧠** **How to use Obsidian (this is key)**

Think of Obsidian as:

Your second brain for TaskNerd

Not documentation.  
Not notes.

👉 **Structured thinking system**

---

**🧱** **Your setup (simple + powerful)**

**Step 1 — Create vault**

On your laptop:

TaskNerd-Wiki

---

**Step 2 — Folder structure**

Inside Obsidian:

00 - Glossary  
01 - Foundations  
02 - Infrastructure  
03 - Agents  
04 - Apps  
05 - Workflows  
06 - Debugging  
07 - Ideas

---

**Step 3 — First notes to create**

Start with:

01 - Foundations/  
  frontend-vs-backend.md  
  localhost-vs-server.md  
  
02 - Infrastructure/  
  ssh-vscode.md  
  tailscale.md  
  pm2.md  
  
04 - Apps/  
  x-post-app.md  
  
03 - Agents/  
  atlas.md  
  nova.md  
  drift.md

---

**🧠** **How to write notes (VERY important)**

Each note should follow this:

**Example: x-post-app.md**

**What it is**

Simple X post generator using LLM.

**Architecture**

Frontend (HTML) → Backend (Express) → OpenRouter → Qwen

**Setup**

Commands + steps

**Key files**

- /xnerd-lite/index.html
- /aiagentnerd/server.js

**Problems we hit**

- wrong folder served
- localhost confusion
- wrong endpoint /ask

**Fixes**

- use /api/chat
- serve from correct directory
- use 0.0.0.0

**Current version**

- multi-agent routing
- Nova writes posts
- 3-post generation

---

**🔗** **Obsidian superpower (don’t skip this)**

Use links like:

[[frontend-vs-backend]]  
[[nova]]  
[[openrouter]]  
[[pm2]]

This creates a **network of knowledge**, not isolated notes.

---

**🌐** **Obsidian Web Clipper (how to use it)**

Use it for:

- docs you read
- GitHub repos
- tutorials
- ideas

But:

👉 ALWAYS rewrite in your own words inside your notes

Otherwise it becomes junk storage.

---

**🚀** **How this connects to your X app**

Every step you take in the app becomes a note:

**Example**

Today you built:

- LLM integration
- multi-agent routing
- Nova writer
- 3-post generation

👉 That becomes:

04 - Apps/x-post-app.md

---

**⚖️** **Exact working rhythm (this is the magic)**

**When building**

Do NOT stop every 2 minutes to write notes.

Instead:

**Build → then summarize**

Example flow:

1.     Implement feature (like today)

2.     Confirm it works

3.     Spend 10–15 minutes writing one clean note

---

**🧭** **What YOU should do next**

**Step 1 — do NOT stop building**

Continue with:

👉 X post app improvements

Next logical step:

- select 1 of 3 posts
- approve it
- save it

---

**Step 2 — create FIRST Obsidian note**

Just one:

x-post-app.md

Include:

- what you built today
- problems you hit
- fixes

---

**Step 3 — ignore perfection**

Your wiki will be messy at first.

That’s fine.

👉 It becomes powerful over time.

---

**🧠** **Strategic advice (important)**

You are currently doing:

Learning + Building + Designing a system

That’s advanced.

So:

👉 The app is your **engine**👉 The wiki is your **memory**

You need both — but the engine must lead.

---

**🎯** **Final recommendation**

👉 Continue building the X agent tomorrow👉 Create 1–2 wiki notes after each session👉 Use Obsidian as your long-term brain

---

**🚀** **Next move**

If you want, next step in the app:

👉 **“approve + save selected post”**

That’s the first real step toward automation.

Just say:

👉 “next step: approve system”

and we’ll build it cleanly.

**Prompt by Alex Finn**

[Top](#top)

Prompt: I want to build an Obsidian memory system into OpenClaw. Here's how it will work: There are 4 layers, from smallest/always-present to largest/on-demand: LAYER 1: BUILT-IN MEMORY (~2,200 chars) ----------------------------------------

- Injected into every single prompt automatically
- Tiny — just compact facts and pointers
- Things like "Alex's name", "SSH into DGX with ssh spark", "vault is at X path"
- Think of it as sticky notes on my monitor — always visible

LAYER 2: AGENTS.md + SOUL.md -----------------------------

- Also injected every single prompt automatically
- My operating instructions, personality, and hard rules
- Includes the mandatory logging rules we just tightened
- This is my "how to behave" layer

LAYER 3: OBSIDIAN VAULT (the big one) --------------------------------------

- Location: iCloud Obsidian vault, shared with OpenClaw
- NOT auto-injected — I read it on session start and during work
- Three folders:

Agent-Shared/ — both agents read/write user-profile.md — who you are, preferences, corrections project-state.md — all projects and their status decisions-log.md — shared decision history Agent-Hermes/ — my private workspace working-context.md — what I'm actively doing right now mistakes.md — things I've gotten wrong daily/ — daily logs (one file per day) Agent-OpenClaw/ — OpenClaw's space (I don't touch it)

- I READ on: session start, after compaction, when I need details
- I WRITE on: task start, every 3-5 tool calls, task completion, corrections

LAYER 4: SESSION SEARCH ------------------------

- Searchable archive of every past conversation
- I don't write to it — it's automatic
- I query it when you reference past work or I need cross-session context
- Last resort recall — "what did we do about X last week?"

THE FLOW ======== New session starts | v Read vault (user-profile, project-state, working-context, today's log) | v Work on tasks — checkpoint to vault every 3-5 tool calls | v Task done — append to daily log, update working-context | v Compaction hits? — todo list survives, re-read vault after | v Session ends — flush everything to daily log

**Prompt adjusted for our Hermes**

[Top](#top)

**Prompt: Hermes Memory System for TaskNerd**

I want to build an Obsidian-based memory and knowledge system into Hermes for TaskNerd / AiAgentNerd.  
  
The goal is not just note storage. The goal is a practical multi-layer memory architecture so Hermes can:  
  
- remember who I am and how I work  
- follow my operating rules and agent conventions  
- use my Obsidian wiki as structured project knowledge  
- recall prior session context when needed  
- preserve continuity across long-running work  
  
There are 4 memory layers, from smallest and always-present to largest and on-demand.  
  
==================================================  
LAYER 1 — CORE MEMORY (tiny, always injected)  
==================================================  
  
This is a compact memory block injected into every prompt automatically.  
  
Purpose:  
- persistent core facts  
- identity anchors  
- critical paths and conventions  
- must-fit-in-context essentials only  
  
Examples:  
- User/project: AiAgentNerd / TaskNerd  
- Main server: ssh nerd@nerd-server  
- Main domain: aiagentnerd.com  
- Standard architecture: Hermes-first  
- Cloudflare Tunnel is the standard exposure method  
- Obsidian vault/repo path  
- Locked agent naming conventions  
- critical current project pointers  
  
Rules:  
- keep extremely compact  
- facts only  
- no long explanations  
- update only when something truly changes  
- think of this as the “sticky notes” layer  
  
==================================================  
LAYER 2 — OPERATING RULES (always injected)  
==================================================  
  
This is the behavior and operating system layer for Hermes.  
  
Purpose:  
- define how Hermes should behave  
- define how each agent role should behave  
- enforce style, discipline, and workflow rules  
- prevent drift, sloppiness, and hallucinated project facts  
  
This layer includes:  
- AGENTS.md style role definitions  
- system rules  
- tone and workflow rules  
- memory handling rules  
- logging/update rules  
- project-specific conventions  
  
Examples:  
- ExecNerd Atlas = strategy, structure, coordination  
- ResearchNerd Drift = exploration, synthesis, research  
- CodeNerd Forge = implementation and code  
- DesignNerd Nova = creative generation and X post writing  
- Hermes must prefer project-specific wiki knowledge over generic assumptions  
- Hermes must say when wiki knowledge is missing instead of inventing facts  
- Hermes should distinguish:  
  - project truth from wiki  
  - general reasoning from LLM knowledge  
  - fresh information from web search  
- Hermes should checkpoint key progress during long tasks  
- Hermes should write durable learnings back into the wiki when instructed  
  
This is the “how to behave” layer.  
  
==================================================  
LAYER 3 — OBSIDIAN WIKI (structured durable knowledge)  
==================================================  
  
This is the large, structured knowledge layer stored in Obsidian and synced to the server.  
  
Purpose:  
- serve as the long-term project brain  
- hold curated, reusable knowledge  
- store decisions, architecture, workflows, and structured project notes  
  
This layer is NOT fully injected every time.  
Instead, Hermes should read from it selectively.  
  
Source structure:  
- raw/ = messy, untouched source material  
- wiki/ = cleaned, structured, reusable knowledge  
  
Primary folders inside wiki/:  
- concepts/  
- infrastructure/  
- apps/  
- agents/  
- workflows/  
  
Key files:  
- index.md = knowledge map  
- log.md = ongoing historical/project log  
  
Rules:  
- Hermes should prefer wiki/ over raw/  
- raw/ is source material, not primary reasoning context  
- wiki/ is the curated knowledge layer  
- Hermes should retrieve only relevant notes when possible  
- if retrieval is not yet available, Hermes may use a bounded wiki context block  
- when useful, Hermes may write back new structured notes to the wiki  
  
Typical use cases:  
- project architecture questions  
- system design continuity  
- workflow recall  
- definitions of internal terms  
- status/context for active builds  
  
==================================================  
LAYER 4 — SESSION / HISTORY RECALL  
==================================================  
  
This is the broad archive and cross-session recall layer.  
  
Purpose:  
- recover what happened in prior sessions  
- find previous decisions, experiments, and context  
- act as fallback memory when the wiki does not contain something yet  
  
This layer is not manually written each time.  
It is searched on demand.  
  
Use it when:  
- I reference past work  
- I say “what did we do last week”  
- I refer to a prior failed attempt  
- Hermes needs cross-session continuity not yet written into wiki  
  
This is the last-resort recall layer, not the primary working memory.  
  
==================================================  
DECISION POLICY  
==================================================  
  
Hermes should decide memory sources like this:  
  
1. If the task depends on fixed identity, infrastructure, agent names, or critical project facts:  
   use Layer 1  
  
2. If the task depends on behavior, rules, role definitions, conventions, or operating style:  
   use Layer 2  
  
3. If the task is about TaskNerd / AiAgentNerd project knowledge, architecture, workflows, decisions, or internal terminology:  
   use Layer 3  
  
4. If the task references prior discussions or older work not clearly present in the wiki:  
   use Layer 4  
  
5. If the task requires broader world knowledge not in memory:  
   use the base LLM reasoning  
  
6. If the task requires fresh or current information:  
   use web search  
  
Hermes must combine these layers intelligently rather than treating one source as universal.  
  
==================================================  
WORKING PRINCIPLES  
==================================================  
  
Hermes should follow these principles:  
  
- Use wiki knowledge as source of truth for project-specific facts  
- Use LLM reasoning for general concepts, synthesis, explanation, and recommendations  
- Use web search for live or changing information  
- Never replace project truth with generic assumptions  
- If a project-specific answer is missing from the wiki, say so clearly  
- When useful, propose writing the new knowledge into the wiki  
- Keep durable knowledge structured and reusable  
- Do not dump large irrelevant note blocks into prompts unnecessarily  
  
==================================================  
FLOW  
==================================================  
  
New session starts  
→ load Layer 1→ load Layer 2→ inspect relevant Layer 3 notes if task is project-specific→ use Layer 4 only when prior-session recall is needed  
  
During work→ use LLM reasoning as normal→ consult wiki when project knowledge is needed→ consult web when freshness is needed→ checkpoint important durable learnings  
  
Task completion→ summarize durable learnings→ optionally write/update wiki notes→ update relevant logs if needed  
  
Long-running or interrupted work→ preserve active context in durable form→ resume by reloading relevant wiki notes and current-state notes  
  
The result should be a Hermes system that behaves like an intelligent operator with:  
- small always-on memory  
- stable operating rules  
- structured project knowledge  
- searchable historical recall

---

**Why this version is better for you**

It improves the original in a few big ways.

**1. It is Hermes-native, not OpenClaw-native**

It assumes:

- Hermes is the main system
- your own wiki is the durable brain
- your own TaskNerd structure matters

**2. It separates project truth from LLM reasoning**

This is huge.

Without this, the agent either:

- becomes too generic
- or becomes too wiki-bound

You want:

- wiki for your system facts
- LLM for broader thinking

**3. It introduces a real decision policy**

This is the most important improvement.

Not just “4 layers exist,” but:

- **when to use each one**
- **how they interact**

**4. It fits your actual folder design**

It respects:

- raw/
- wiki/
- index.md
- log.md

instead of a random imported structure.

---

**How to implement this later**

Not today. But when the time comes, this is the exact path I’d use.

**Phase 1 — Layer 1: Core Memory**

Create one tiny file, for example:

wiki/agents/core-memory.md

This should contain only compact essentials, such as:

- server access
- main domains
- locked naming conventions
- architecture choices
- key paths

Then in your server.js, always inject a **small extracted version** of that file into Atlas.

This should stay short.

Think:

- 10–20 lines
- not a full note dump

---

**Phase 2 — Layer 2: Operating Rules**

Create one or two files like:

wiki/agents/agents.md  
wiki/agents/hermes-rules.md

These hold:

- agent roles
- behavior rules
- system conventions
- tone
- decision-making rules
- “prefer wiki over assumptions”
- “English unless asked otherwise”
- “separate project facts from recommendations”

These also get injected automatically, every time, but in a bounded form.

So later your prompt stack becomes:

- core memory
- operating rules
- optional retrieved wiki notes
- user task

---

**Phase 3 — Layer 3: Retrieved Wiki Knowledge**

This is the big one.

At first, you can do a rough version:

- load a chunk of wiki/

Later, the real version should be:

- detect what the question is about
- retrieve only the most relevant notes
- inject those into the prompt

Example:

User asks:  
“how is our x post app structured?”

Hermes should retrieve:

- wiki/apps/x-post-app.md
- maybe wiki/workflows/content-ingestion.md
- maybe wiki/infrastructure/hermes-setup.md

Not the whole vault.

This is the real upgrade path.

---

**Phase 4 — Layer 4: Session Recall**

This stays separate.

This can come from:

- Hermes history
- prior session summaries
- your platform’s memory/search layer

Use it only when needed.

Example:

- “what did we decide last Tuesday about model routing?”

That’s not necessarily wiki material.  
That’s history retrieval.

---

**Exact implementation architecture later**

When we implement this, I would structure your app like this:

**A. Memory builder**

A function that assembles prompt context:

buildMemoryContext({  
  agent,  
  message,  
  useWeb,  
  useHistory,  
  useWiki  
})

This function pulls from:

- Layer 1 core memory
- Layer 2 rules
- Layer 3 retrieved wiki notes
- Layer 4 session recall

and builds the final context.

---

**B. Router**

A lightweight classifier that decides:

- is this project-specific?
- is this general reasoning?
- is this current/live info?
- does it reference prior work?

Then it chooses:

- wiki-first
- llm-first
- web-first
- history recall

---

**C. Writeback layer**

When useful, Hermes can write:

- new structured note
- updated project state
- new decision log entry
- new workflow clarification

But not everything should be auto-written.  
Only durable knowledge.

That’s important.

---

**What I would name the files**

For your system, I’d recommend something like this:

wiki/agents/core-memory.md  
wiki/agents/operating-rules.md  
wiki/agents/agent-roles.md  
wiki/workflows/memory-system.md  
wiki/concepts/raw-vs-wiki.md  
wiki/infrastructure/wiki-sync.md  
wiki/apps/x-post-app.md  
log.md  
index.md

And optionally later:

wiki/state/current-focus.md  
wiki/state/project-state.md  
wiki/state/decisions-log.md

That gives Hermes a much cleaner memory structure.

---

**The most important design rule**

This is the single sentence I would lock in:

Use the wiki as the source of truth for project-specific facts, terminology, and decisions; use the LLM for broader reasoning and synthesis; use web search for live information; use session recall for past conversational context not yet captured in the wiki.

That is the heart of the whole system.

---

**My honest recommendation**

When we implement this for real, do it in this order:

1.        Layer 1 core memory

2.        Layer 2 operating rules

3.        selective wiki retrieval

4.        session recall

5.        writeback to wiki

That order keeps things manageable and avoids chaos.

---

**Bottom line**

Yes — Alex Finn’s structure is excellent.

But for you, the correct version is not:

- “Obsidian memory for OpenClaw”

It is:

- **Hermes memory architecture for TaskNerd, backed by your Obsidian wiki**

And that can become a real, durable brain for your whole system.

Tomorrow or whenever you want, we can turn this into:

- a final locked prompt
- the actual Obsidian file structure
- the exact server.js implementation plan
- and later the real code step-by-step

**TUTORIAL for setting up Obsidian Wiki**

[Top](#top)

aiagentnerd, Karpathy-style LLM wiki, chrome laptop

**AI Agent Nerd — Obsidian Wiki Setup (FULL GUIDE)**

This is your **official setup guide** for building a Karpathy-style LLM Wiki.

---

**🧠** **0. What you are building (IMPORTANT)**

You are NOT building notes.

You are building:

👉 A **knowledge system for Hermes + TaskNerd**

---

**🧱** **Core architecture**

raw/   → source material  
wiki/  → structured knowledge  
index  → map  
log    → history

---

**🖥****️ 1. Install Obsidian (Laptop)**

Install Obsidian on your laptop.

**Steps:**

1.     Download from obsidian.md

2.     Install

3.     Open Obsidian

4.     Click **“Create new vault”**

---

**Vault name (IMPORTANT)**

👉 Use:

AIAgentNerd-Wiki

---

**📂** **2. Create your folder structure**

Inside Obsidian:

---

**Create these folders:**

raw/  
wiki/

---

**Inside raw/**

raw/web/

---

**Inside wiki/**

concepts/  
infrastructure/  
apps/  
agents/  
workflows/

---

**📄** **3. Create key files**

These live in the **root (top level)**:

---

**1. index.md**

👉 Your **navigation system**

---

**2. log.md**

👉 Your **activity/history**

---

**3. First note (already done)**

wiki/infrastructure/git-obsidian-setup.md

---

**🧠** **4. Note structure (STANDARD TEMPLATE)**

Every note should look like this:

# Title #tags  
  
## Key Insight  
One powerful sentence.  
  
---  
  
## What it is  
  
Simple explanation.  
  
---  
  
## Mental Model  
  
How it works conceptually.  
  
---  
  
## Setup / Steps  
  
Commands or process.  
  
---  
  
## Why it matters  
  
Why you care.  
  
---  
  
## Connections  
  
[[other-note]]

---

**🧠** **5. Tags vs Headings (IMPORTANT)**

**Headings:**

## Section

👉 structure

---

**Tags:**

#infrastructure #wiki

👉 categorization

---

👉 They are NOT the same

---

**🔗** **6. Linking system (CORE OF EVERYTHING)**

**Internal links:**

[[llm-wiki]]  
[[x-post-app]]

---

**Bidirectional linking**

**In RAW:**

## Processed into  
[[llm-wiki]]

---

**In WIKI:**

## Sources  
[[raw/web/article-name]]

---

👉 This creates:

raw ⇄ wiki

---

**🌐** **7. Web Clipper setup**

Use the Obsidian Web Clipper extension.

---

**Settings:**

- Default location → raw/web/
- Save full article

---

**IMPORTANT RULE**

❗ Never treat clipped content as final

---

**🧠** **Workflow:**

1.     Clip article → raw/web

2.     Process (with me)

3.     Create structured note in wiki/

4.     Link both ways

---

**⚠️** **8. Raw vs Wiki (CRITICAL)**

**raw/**

- messy
- untouched
- source of truth

---

**wiki/**

- clean
- structured
- reusable

---

👉 NEVER mix them

---

**🧠** **9. Index (NEW STRUCTURE)**

Your index.md should be:

# AI Agent Nerd Wiki  
  
## Concepts  
- [[llm-wiki]]  
- [[topic-brains]]  
  
## Infrastructure  
- [[git-obsidian-setup]]  
  
## Apps  
- [[x-post-app]]  
  
## Workflows  
- [[content-ingestion]]  
  
## Current Focus  
- X Post App  
- LLM Wiki system

---

👉 This is a **knowledge map**, not folder list

---

**🧠** **10. Log system**

In log.md:

## 2026-04-10  
  
- Created LLM Wiki note  
- Set up linking system  
- Built first Topic Brain

---

👉 This becomes important later for Hermes

---

**🔁** **11. Git setup (local backup)**

In PowerShell (NOT SSH):

cd "C:\Users\Win11\OneDrive\Documents\AIAgentNerd-Wiki"  
  
git init  
git add .  
git commit -m "Initial wiki setup"

---

**Notes:**

- CRLF warnings = normal
- DO NOT run git in home directory

---

**🧠** **12. How Obsidian saves files**

👉 Auto-save

No save button needed.

---

**🧠** **13. Templates (IMPORTANT CONCEPT)**

Templates = reusable note structures

---

**Example:**

Instead of writing structure every time:

👉 you paste your standard format

Later you can automate this.

---

**⚠️** **14. “Don’t save clips as raw” (what it means)**

It means:

❗ Don’t leave knowledge in raw form

---

**WRONG:**

- clip → done

---

**CORRECT:**

- clip → process → wiki note

---

**🧠** **15. Topic Brain (WHAT YOU BUILT)**

You now have:

llm-wiki  
topic-brains  
content-ingestion

---

👉 This is your first **knowledge system**

---

**🔥** **16. Your workflow going forward**

**Daily flow:**

1.     Build (X app / system)

2.     Clip useful content

3.     Process into wiki (10–15 min)

4.     Link everything

---

👉 That’s it

---

**🧠** **17. What comes next (IMPORTANT)**

You now have:

✅ structured wiki✅ linking system✅ topic brain✅ ingestion workflow

---

**NEXT PHASE:**

👉 **Connect this to Hermes**

That means:

- Hermes reads your wiki
- Hermes uses it to think
- Hermes updates it

---

**🎯** **Final mental model**

You are building:

You → curate  
Wiki → stores knowledge  
Hermes → uses + expands knowledge

---

**🚀** **When you're ready**

Open a new chat and say:

👉 **“connect Hermes to Obsidian wiki (step-by-step)”**

---

We’ll then:

- sync vault to server
- define what Hermes reads
- build your first real memory loop

---

You’ve just built something most people never get to:

👉 a **real knowledge system foundation**

Take a break — this was a big step 🔥

**Connect wiki to Server / Hermes**

[Top](#top)

# 🖥️ 19. Where your Wiki lives (CRITICAL DECISION)

Right now your vault is on:

👉 your **laptop (Windows)**

But Hermes runs on:

👉 your **server (nerd-server)**

---

## ❗ Problem

Hermes cannot access your wiki unless:

👉 the vault exists on the server

---

## ✅ Solution (simple + correct)

We will:

👉 **sync your Obsidian vault to your server**

---

# 🔁 20. Step 1 — Sync Wiki to Server

We’ll use Git (you already initialized it 👍)

---

## 💻 On your laptop (PowerShell)

Inside your vault:

cd "C:\Users\Win11\OneDrive\Documents\AIAgentNerd-Wiki"

Then:

git remote add origin https://github.com/AiAgentNerd/aiaagentnerd-wiki.git  
git push -u origin main

👉 (If repo doesn’t exist → create it on GitHub first)

---

## 🖥️ On your server (SSH)

ssh nerd@nerd-server

Then:

cd ~  
git clone https://github.com/YOUR_USERNAME/aiaagentnerd-wiki.git

You now have:

~/aiaagentnerd-wiki

---

## 🎯 Result

Now:

- Laptop → editing wiki
- GitHub → sync layer
- Server → Hermes access

---

# 🔁 21. Step 2 — Keep Wiki in Sync

Every time you update:

### On laptop:

git add .  
git commit -m "update wiki"  
git push

### On server:

cd ~/aiaagentnerd-wiki  
git pull

👉 Later we automate this (don’t worry yet)

---

# 🧠 22. What Hermes should read (VERY IMPORTANT)

Hermes should NOT read everything.

---

## ❌ DO NOT feed:

- raw/
- messy notes
- long articles

---

## ✅ ONLY feed:

👉 `wiki/` folder

Specifically:

- concepts/
- infrastructure/
- apps/
- workflows/
- agents/

---

## 🎯 Why

Because:

👉 You already cleaned and structured it

This is **high-quality context**

---

# ⚙️ 23. Step 3 — Give Hermes access

Now we connect Hermes to:

~/aiaagentnerd-wiki/wiki

---

## In your Hermes system (server.js)

We will add:

👉 a **wiki reader function**

Example (simple version):

const fs = require("fs");  
const path = require("path");  
  
function loadWiki() {  
  const wikiPath = "/home/nerd/aiaagentnerd-wiki/wiki";  
  const files = fs.readdirSync(wikiPath, { recursive: true });  
  
  let content = "";  
  
  files.forEach(file => {  
    if (file.endsWith(".md")) {  
      const fullPath = path.join(wikiPath, file);  
      content += fs.readFileSync(fullPath, "utf-8") + "\n\n";  
    }  
  });  
  
  return content;  
}

---

## Then inject into Hermes prompt

Inside your Atlas agent:

const wikiContext = loadWiki();  
  
const prompt = `  
You are ExecNerd Atlas.  
  
Use the following knowledge base:  
  
${wikiContext}  
  
User input:  
${userInput}  
`;

---

## 🎯 Result

Atlas now:

👉 **thinks using your wiki**

---

# 🧠 24. First “WOW moment” you will get

After this:

Ask Atlas:

👉 “How does our X post system work?”

Instead of generic answer, it will say:

👉 based on YOUR system (Hermes + worker + dashboard)

That’s when it clicks 🔥

---

# 🔄 25. Step 4 — Writing BACK to the Wiki (later)

Right now:

Hermes can **read**

Next step (later):

👉 Hermes can **write new notes**

Examples:

- Drift → research → save to `wiki/concepts/`
- Forge → create system doc → save to `wiki/infrastructure/`
- Atlas → update index.md

---

# ⚠️ 26. Keep it SIMPLE (IMPORTANT)

Right now, DO NOT:

- build embeddings
- build vector DB
- over-engineer search

👉 Just load markdown files

That’s enough for V1

---

# 🧠 27. How this fits YOUR system (TaskNerd)

This is where it gets exciting:

Your agents become:

- **ExecNerd Atlas** → reads wiki → makes decisions
- **ResearchNerd Drift** → expands wiki
- **CodeNerd Forge** → builds based on wiki
- **MemoryNerd Recall** → manages updates

👉 This = your **real multi-agent brain**

---

# 🚀 28. What we do NEXT (in next chat)

When you’re ready, say:

👉 **“step-by-step connect Hermes to wiki (hands-on)”**

And I will:

- walk you line-by-line in server.js
- plug it into your EXISTING system
- test it live with you

**Why we set up everything manually, rather than just telling Hermes ?**

[Top](#top)

aiagentnerd, Karpathy style LLM Wiki

gm gm . first question of the day. people on youtube always say that one of the big advantages of openclaw / hermes is that you just tell them what to do, and they will do everything by themsevles, e.g. setting up an obsidian wiki (v 0.9 of Hermes has a Karpathy llm wiki skill). I feel like I do things wrong because I seem to be setting up everything manually with your great help, rather than just telling hermes. Please discuss my concerns.

GM GM ☀️ — this is a really important question, and I’m glad you asked it now.

Short answer:

👉 You are **not doing it wrong**👉 You are actually doing it **the right (and rare) way**

Let’s unpack this honestly.

---

**🧠** **What YouTube _says_ vs reality**

**🎥** **What you see**

“Just tell the agent and it will do everything”

Examples:

- “build me a system”
- “set up a wiki”
- “create automation”

---

**⚠️** **What’s actually happening**

Behind the scenes:

- lots of retries
- hidden manual fixes
- incomplete setups
- shallow systems

👉 They show the **best 10 seconds**, not the messy 2 hours

---

**🧠** **The core misunderstanding**

Agents like Hermes / OpenClaw are:

❗ **Execution engines — not system designers**

---

**What they’re GOOD at**

- writing files
- calling APIs
- generating content
- automating repetitive steps

---

**What they’re BAD at (today)**

- designing long-term architecture
- making durable decisions
- understanding YOUR goals deeply
- building systems that last

---

**🧠** **What YOU are doing (this is key)**

You are not just “setting up tools”

You are:

👉 designing a **knowledge system + product architecture**

---

**That includes:**

- raw vs wiki separation
- Topic Brains
- linking strategy
- index design
- future Hermes integration
- product thinking (TaskNerd)

---

👉 Hermes cannot reliably do this yet

---

**🔥** **The truth (no fluff)**

If you had told Hermes:

“set up an Obsidian wiki”

You would likely get:

- a folder
- some files
- generic structure

---

But NOT:

- Karpathy-style system
- Topic Brain architecture
- bidirectional linking
- product-ready structure

---

👉 What you built is **10x better**

---

**🧠** **Why your approach is actually superior**

**You are building:**

**1. Understanding**

You now know:

- why raw exists
- why wiki exists
- how knowledge flows

---

**2. Control**

You can:

- change architecture anytime
- debug issues
- evolve the system

---

**3. Foundation for automation**

Now (important):

👉 You can later LET Hermes automate it correctly

---

**🧠** **The correct sequence (THIS is the secret)**

**❌** **Wrong order (YouTube way)**

Agent → builds system → user doesn’t understand → system breaks

---

**✅** **Correct order (what YOU did)**

Understand → design → structure → THEN automate

---

👉 This is how real systems are built

---

**🔥** **Where Hermes actually fits**

Hermes shines here:

---

**🟢** **After system is defined**

Then you can say:

- “process this raw file into wiki”
- “update topic brain”
- “generate X posts from this topic”
- “log today’s activity”

---

👉 Now Hermes becomes powerful

---

**🔴** **Before system exists**

It guesses.

And guesses = fragile systems.

---

**🧠** **Mental model (very important)**

Think of Hermes as:

👉 a **junior engineer with infinite speed**

---

Would you tell a junior engineer:

“Design my entire architecture from scratch”

👉 Probably not

---

But you WOULD say:

- “Here’s the structure — implement it”
- “Process this data”
- “Update this system”

---

**🔥** **Your current position (very strong)**

You now have:

- structured wiki
- Topic Brain
- ingestion system
- clear architecture

---

👉 This is EXACTLY when agents become useful

---

**🚀** **What happens next (this is exciting)**

In the next phase, you will:

👉 Start saying things like:

- “Hermes, ingest this article into the wiki”
- “Hermes, update llm-wiki.md with new insights”
- “Hermes, generate 3 X posts from topic brain”

---

👉 And it will actually work

---

**🎯** **Final answer to your concern**

“Am I doing it wrong because I’m not letting Hermes do everything?”

👉 No.

You are doing what **builders do** instead of what **demo watchers do**.

---

**🧠** **One sentence to remember**

👉 First you build the system👉 Then the agent runs the system

**How to use Docs with Obisidian**

[Top](#top)

question.. How can i feed personal documents, e.g. word files, into my obsidian wiki ?

Great question — this is exactly how your system becomes **personal + powerful** 🔥

Short answer:

👉 You don’t “upload Word files into Obsidian” directly👉 You **convert** **→** **process** **→** **integrate into your wiki**

Let me show you the clean, scalable way.

---

**🧠** **The correct mental model**

Your system has 2 layers:

Word files → raw → wiki → knowledge

---

👉 Word files are just another **source (like web clips)**

---

**🚀** **OPTION 1 — SIMPLE (recommended now)**

**Step 1 — Open your Word file**

In Microsoft Word

---

**Step 2 — Copy the content**

- Ctrl + A
- Ctrl + C

---

**Step 3 — Create raw note in Obsidian**

Inside:

raw/docs/

Create:

my-document.md

---

**Step 4 — Paste**

👉 Now you have:

- raw version stored
- inside your system

---

**Step 5 — Process (important)**

Then:

👉 send it to me👉 I convert it into structured wiki notes

---

**🧠** **This is EXACTLY like web clipper**

- Web → raw/web
- Word → raw/docs

---

**⚙️** **OPTION 2 — CLEANER (slightly better)**

Instead of copy/paste:

---

**Export Word** **→** **Markdown**

In Word:

- File → Save As
- Choose:

- .txt OR .html

Then paste into Obsidian

---

👉 Keeps formatting cleaner

---

**🔥** **OPTION 3 — FUTURE (automated)**

Later you can:

- upload .docx
- Hermes reads file
- converts to markdown
- auto-ingests into wiki

---

👉 fully automated pipeline

---

**🧠** **Where should Word docs live?**

Create:

raw/docs/

---

Final structure:

raw/  
  web/  
  docs/

---

**⚠️** **IMPORTANT RULE**

❗ Never treat Word files as final knowledge

---

**WRONG:**

- store doc → done

---

**CORRECT:**

- store doc → process → wiki note

---

**🧠** **Example workflow (real)**

You have:

👉 “TaskNerd business plan.docx”

---

**Step 1**

Paste into:

raw/docs/tasknerd-business-plan.md

---

**Step 2**

We process into:

wiki/concepts/business-model.md  
wiki/apps/x-post-app.md  
wiki/workflows/monetization.md

---

👉 ONE document → MULTIPLE notes

(This is VERY Karpathy-style)

---

**🔥** **Why this is powerful**

Now your personal knowledge becomes:

- searchable
- structured
- reusable
- usable by Hermes

---

**🧠** **Mental model**

Raw = storage  
Wiki = intelligence

---

**🚀** **What I recommend for YOU right now**

Do this:

1.        Create folder:

raw/docs/

2.        Take ONE Word file

3.        Paste into Obsidian

4.        Send it here

---

👉 I’ll convert it into:

- clean wiki notes
- properly structured
- linked into your system

---

**🎯** **Final takeaway**

Your Word files are not separate from your system.

👉 They are **fuel for your Topic Brains**

---

When you’re ready:

👉 upload one document and say  
**“process this into wiki”**

**_Update Document files_**

[top](#top)

and when i update the word file? do i have to re-upload and we create a new raw/md file, or can the existing files be updated?

Great question — this is where your system becomes either **clean and scalable**… or messy over time.

Short answer:

👉 **Do NOT create a new raw file every time**👉 **Update the existing raw file (with version awareness)**

---

**🧠** **The right way to handle updates**

Think of your Word file like:

👉 a **living source**, not a one-time input

---

**🧱** **Recommended system (simple + powerful)**

**✅** **1. ONE raw file per document**

Example:

raw/docs/tasknerd-business-plan.md

---

**✅** **2. When you update the Word file**

👉 Replace or update the content in that SAME file

---

**🔥** **Add version tracking (VERY important)**

At the top of the raw file:

# TaskNerd Business Plan  
  
## Version  
v2 — updated pricing model  
  
## Last Updated  
2026-04-16

---

👉 Now you always know:

- what changed
- when it changed

---

**🧠** **3. What happens to the wiki?**

**❗** **You do NOT rebuild everything**

Instead:

👉 You **update affected notes only**

---

**Example**

You change pricing in Word file

---

**You update:**

wiki/concepts/business-model.md

---

**You do NOT touch:**

- unrelated notes
- stable knowledge

---

**🔁** **Workflow (clean version)**

**When document changes:**

1.        Update Word file

2.        Update raw markdown file

3.        Tell me:

👉 “update wiki based on this change”

---

👉 I will:

- detect changes
- update only relevant notes
- keep structure clean

---

**⚠️** **What NOT to do**

**❌** **Don’t do this:**

tasknerd-plan-v1.md  
tasknerd-plan-v2.md  
tasknerd-plan-final-final.md 😅

---

👉 This becomes chaos

---

**🧠** **Optional (advanced later)**

If you want full tracking:

👉 use Git (you already started)

Then you get:

- full version history
- diffs (what changed)
- rollback

---

**🧠** **Alternative (if changes are HUGE)**

Only if document is completely different:

👉 THEN create:

tasknerd-business-plan-v2.md

---

👉 But this is rare

---

**🔥** **Best practice for YOU**

Keep it simple:

- 1 file per document
- update it
- track version at top
- update wiki selectively

---

**🧠** **Mental model**

Raw evolves  
Wiki stabilizes

---

**🚀** **What this enables later**

When Hermes is connected:

👉 it can:

- detect updates
- update wiki automatically
- log changes in log.md

---

**🎯** **Final answer**

Update existing raw file  
Don’t create duplicates  
Update wiki selectively

---

If you want next:

👉 I can show you how to turn updates into a **semi-automated pipeline**

Just say:

👉 “automate document updates”