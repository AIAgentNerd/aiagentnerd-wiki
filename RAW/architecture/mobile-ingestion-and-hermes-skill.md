# Mobile Ingestion Workflow + Hermes “Save to Knowledge” Skill

## Topics
- mobile-ingestion
- youtube
- workflow
- raw
- hermes
- automation
- product-design

---

## Context

Defines the practical workflow for capturing knowledge on mobile (e.g. YouTube, research) and integrating it into the AiAgentNerd system.

Also introduces the concept of a Hermes skill that automates RAW creation, ingestion, and compilation into the WIKI.

---

## Key Concepts

- Mobile is for **capture + structuring**, not execution
- Server is the **source of truth**
- WIKI is **compiled output**
- Users should NOT see “RAW / WIKI / compile”
- Product should feel like:
  
  > “Save this to my knowledge” / “Remember this”

---

## Mobile Ingestion Workflow (Recommended)

### Core Flow


📱 Mobile:
YouTube / Content
↓
ChatGPT → structured RAW
↓
Store temporarily (Notes / messaging)

💻 Laptop / Server:
copy RAW
↓
save to RAW folder
↓
compile
↓
Git → Obsidian sync


---

## Mobile Capture Options

### Option 1 — ChatGPT (Primary)

- paste YouTube link or content
- use YouTube → RAW prompt
- get structured RAW immediately

---

### Option 2 — Notes App (Recommended storage)

- single note: `RAW INBOX`
- append multiple RAW entries
- batch process later

---

### Option 3 — Messaging (Telegram / WhatsApp)

- send RAW to self
- access on laptop
- copy → ingest

---

### Option 4 — Obsidian Mobile (Limited use)

- only use as:
  

RAW/inbox/


- avoid direct integration with system RAW folders

---

## Mobile → Laptop Transfer

### Preferred methods

- Telegram / WhatsApp self-chat
- Notes app (iCloud / Google sync)
- Email draft (fallback)

---

## ChatGPT as Temporary Storage

### Pattern

- one chat per RAW
- rename:


RAW: <filename>


### Pros

- already structured
- no extra tools

### Cons

- chat list clutter
- not scalable long-term

---

## Decision

- Do NOT use ChatGPT as primary storage
- Use Notes app as **RAW inbox**

---

## YouTube → RAW Strategy

### Without transcript

- use structured prompt
- extract:
  - key concepts
  - workflows
  - tools

---

### With transcript (preferred)

- transcript = source of truth
- produces near-perfect RAW
- avoids hallucination

---

## Commands (Primary)

```bash
# create RAW file
cat > ~/aiagentnerd-wiki/RAW/<category>/<filename>.md

# compile
curl -X POST http://localhost:3100/api/system-wiki/scan-and-compile \
  -H "Content-Type: application/json" \
  -d '{}'

# git sync
cd ~/aiagentnerd-wiki
git add .
git commit -m "add file"
git push
Commands (Alternatives)
Editor method
nano ~/aiagentnerd-wiki/RAW/<category>/<filename>.md
Decision
Selected: terminal cat > method
Why:
fastest
consistent
no UI dependency
Obsidian Sync Strategy
Do NOT use Obsidian Sync for system

Reason:

bypasses Git
creates conflicts
not aware of compile process
Use Git-based sync
Server → GitHub → Laptop Obsidian
Product Direction (IMPORTANT)

Users should NOT see:

RAW
WIKI
compiler
User-facing model
User creates / researches
↓
Clicks “Save”
↓
System stores + structures
↓
Future responses improve
System Reality
content
↓
RAW
↓
compile
↓
WIKI
↓
retrieval
Hermes Skill Idea — “Save to Knowledge”
Goal

User pastes content into Hermes:

Save this to my knowledge
Desired behavior

Hermes should:

Convert input → structured RAW
Generate filename + category
Save to:
~/aiagentnerd-wiki/RAW/<category>/<filename>.md
Trigger compile
Push to Git
Return confirmation
Required Endpoint
POST /api/wiki/ingest-raw
Payload
{
  "category": "web",
  "filename": "youtube-agent-routing.md",
  "content": "# markdown..."
}
Backend Flow
validate
↓
sanitize filename
↓
write RAW file
↓
compile
↓
git push
↓
return result
Commands (Conceptual)
Ingest RAW (future)
curl -X POST http://localhost:3100/api/wiki/ingest-raw \
  -H "Content-Type: application/json" \
  -d '{...}'
Decision
Build ingestion endpoint next
Then add Hermes skill
Custom Wiki Platform Idea
Internal version
paste RAW
compile
browse WIKI
User version (future)
workspace per user
save knowledge
retrieval improves outputs
Product Insight

Users don’t want a wiki.

They want:

“A system that remembers and improves.”

Mobile Template (Capture Layer)
RAW: <filename>

Source:
<link>

Key:
- ...

Steps:
- ...

Commands:
- ...

Decision:
- ...
Rules
Mobile = capture only
Server = source of truth
WIKI = output only
Never edit WIKI directly
Always go through RAW
Related
[[knowledge-ingestion-workflow]]
[[knowledge-system-wiki]]
[[core-hermes-architecture]]
Raw Notes
ChatGPT can be temporary storage but not scalable
Notes app is best mobile inbox
Transcript-based ingestion is highest quality
Automation via Hermes skill is next major upgrade