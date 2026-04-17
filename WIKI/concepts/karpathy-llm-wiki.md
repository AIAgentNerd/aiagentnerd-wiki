# Compiled Note

**Source RAW file:** `web/Karpathy-Style LLM Wiki.md`

---

# Karpathy‑Style LLM Wiki for AI Agent Nerd  

**Path:** `concepts/karpathy-llm-wiki.md`  

---  

## Summary  
A Karpathy‑style LLM wiki is a **structured, markdown‑based knowledge base** that serves as the long‑term memory for your AI agents (Atlas, Drift, Forge). It is built as a simple Git repository of `.md` files, edited in Obsidian, and synced to your server where Hermes can read it. The wiki follows a strict chapter template, includes mental‑model sections, cross‑chapter links, and a glossary. It starts as a personal “second brain” and can later become a public tutorial resource or a per‑user “topic brain” system.

---

## Core Principles  

| Principle | Description |
|-----------|-------------|
| **Not documentation** | The wiki is a *thinking system* that mirrors how agents reason. |
| **Flat, chapter‑based** | Each concept lives in its own markdown file (`01‑ssh‑vscode.md`, …). |
| **Karpathy template** | Every chapter uses the exact six‑section format plus optional mental‑model and connection sections. |
| **Git versioned** | The whole vault is a Git repo → full history, easy rollback, collaborative edits. |
| **Sync via rsync** | Free, command‑line sync from laptop (Obsidian) to `~/aiagentnerd-wiki` on the server. |
| **Obsidian UI** | Human‑friendly editing, backlinks, tags, and Web Clipper for rapid ingestion. |
| **Future‑ready** | Can be exported to static site generators (Nextra, Docusaurus) or fed to agents as memory. |

---

## Folder & File Layout  

```
AIAgentNerd-Wiki/                ← Obsidian vault (local)
│
├── .git/                        ← Git repo (local)
├── .gitignore
├── index.md                     ← Home page with navigation links
├── log.md                       ← Chronological record of changes
├── AGENTS.md                    ← Instructions for agents (schema)
│
├── 00-glossary/                 ← Glossary files (or single 00-glossary.md)
│   └── glossary.md
│
├── 01-foundations/
│   └── 01-ssh-vscode.md
│
├── 02-infrastructure/
│   └── 02-tailscale.md
│
├── 03-agents/
│   └── 03-hermes-basics.md
│
├── 04-apps/
│   └── 04-x-post-app.md
│
├── 05-workflows/
│   └── 05-multi-agent-routing.md
│
├── 06-debugging/
│   └── 06-debugging-cheatsheet.md
│
├── 07-topics/
│   └── (future topic‑brain files)
│
└── raw/
    ├── web/                     ← Web‑clipper raw articles
    └── docs/                    ← PDFs, Word exports, etc.
```

*Keep the top‑level flat for now; subfolders only for `raw/` and optional `templates/`.*

---

## Chapter Template (mandatory)

```markdown
# [Chapter Title]

## 1. What it is
*Plain‑language description.*

## 2. Why it matters
*Why this concept is needed in your system.*

## 3. How we set it up
*Step‑by‑step commands.*

## 4. Common errors
*Real mistakes you hit.*

## 5. How we fixed them
*Actual fixes (gold).*

## 6. Final setup (standard)
*Your chosen configuration.*

## 🧠 Mental Model
*Explain how the piece fits into the overall architecture.*

## 🔗 How this connects to other chapters
*Bullet list of cross‑references (e.g., SSH → PM2 → Cloudflare).*
```

**Do not deviate** – consistency is what makes the wiki “Karpathy‑style”.

---

## Glossary (highly recommended)

Create `00-glossary/glossary.md` (or `00-glossary.md`) with one‑line definitions, e.g.:

```markdown
# Glossary

## SSH
Secure remote shell access.

## Port
Numeric endpoint on a server (e.g., 3100 for Hermes).

## API
Programmatic interface for services to communicate.

## Process
Running program instance.

## Proxy
Forwarder (e.g., Nginx) that routes requests.

## Agent
AI worker with a specific role.

## Route
Path a request follows (frontend → backend → agent).
```

---

## Workflow Overview  

1. **Capture** – Use **Obsidian Web Clipper** → saves raw article to `raw/web`.  
2. **Process** – Open the raw note, add *Summary*, *Key Points*, *Why it matters*, *Ideas*.  
3. **Structure** – Move/convert the processed note into the appropriate chapter file using the template.  
4. **Commit** – `git add . && git commit -m "Update <topic>"`.  
5. **Sync** – `rsync -av ~/AIAgentNerd-Wiki/ nerd@nerd-server:~/aiagentnerd-wiki/` (or alias `syncwiki`).  
6. **Agent consumption** – Hermes reads markdown files from `~/aiagentnerd-wiki` as its memory source.  

*Repeat for every new piece of knowledge.*

---

## Git Setup (local)

```bash
cd path/to/AIAgentNerd-Wiki
git init
echo ".obsidian/" > .gitignore
git add .
git commit -m "Initial AIAgentNerd wiki setup"
```

*Commit after each meaningful edit.*

---

## Free Sync to Server (rsync)

```bash
# One‑time server folder creation
ssh nerd@nerd-server "mkdir -p ~/aiagentnerd-wiki"

# Sync command (run after each session)
rsync -av ~/AIAgentNerd-Wiki/ nerd@nerd-server:~/aiagentnerd-wiki/
```

Add an alias for convenience:

```bash
alias syncwiki='rsync -av ~/AIAgentNerd-Wiki/ nerd@nerd-server:~/aiagentnerd-wiki/'
```

---

## Tags vs. Links (Obsidian)

* **Links (`[[Note]]`)** – direct, strong connections; use for cross‑chapter references.  
* **Tags (`#tag`)** – loose grouping; optional early on (1‑3 tags per note).  

Prefer links for the Karpathy system; add tags only when you need a quick filter.

---

## Extending to Per‑User “Topic Brains”

| Layer | Description |
|-------|-------------|
| **User** | Account, preferences, private memory. |
| **Topic Hub** | Folder (e.g., `topics/ai‑agents/`) containing its own markdown knowledge base, raw inputs, and `log.md`. |
| **Outputs** | X‑post drafts, summaries, alerts generated from the hub. |

Implementation steps (future):

1. Create a `topics/` folder inside the repo.  
2. Each user gets a sub‑folder (`topics/<user‑id>/<topic>/`).  
3. Sync/clone per‑user repos or expose via API for import/export.  

Export formats: Markdown (human‑readable) and JSON (structured) – keep the data portable.

---

## Relevance to **AI Agent Nerd / TaskNerd**  

* The wiki **becomes the brain** for Atlas (knowledge), Drift (research ingestion), and Forge (execution).  
* All system documentation, debugging stories, and architectural decisions are stored once, versioned, and instantly available to agents.  
* Future X‑post generation can pull directly from the wiki’s “topic brains,” ensuring consistency and reducing duplicated effort.  
* The same structure can be exposed as a public tutorial resource under the AI Agent Nerd brand.

---

## Quick Checklist (first‑time setup)

- [ ] Install Obsidian (desktop) → create vault **AIAgentNerd-Wiki**.  
- [ ] Create folder hierarchy (00‑glossary … 07‑topics, raw, templates).  
- [ ] Add `index.md`, `log.md`, and first chapter (`04-x-post-app.md`) using the template.  
- [ ] Initialize Git, add `.gitignore`.  
- [ ] Commit initial state.  
- [ ] Install **Obsidian Web Clipper** → set default save location to `raw/web`.  
- [ ] Create server folder `~/aiagentnerd-wiki`.  
- [ ] Set up rsync alias `syncwiki`.  
- [ ] Run `syncwiki` → verify files appear on server.  
- [ ] Configure Hermes to read markdown files from `~/aiagentnerd-wiki`.  

Once these steps are done, you have a **fully functional Karpathy‑style LLM wiki** ready to power AI Agent Nerd.
