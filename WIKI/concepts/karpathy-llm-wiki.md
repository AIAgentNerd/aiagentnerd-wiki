# Compiled Note

**Source RAW file:** `web/Karpathy-Style LLM Wiki.md`

---

Great! You're now at the critical stage where your clipped content becomes **structured knowledge** that feeds into your AI system. Let’s walk through the exact steps to process your first clipped note into a **Topic Brain entry** (this is where your system starts compounding).

---

### 🧠 Step 1: Open the Clipped Note
1. In Obsidian, navigate to:  
   `raw/web` → Open the clipped note (e.g., `2026-04-15-openai-update.md`).

---

### 📝 Step 2: Transform Raw Content into Structured Knowledge
**Goal:** Turn the raw article into a **Topic Brain entry** that’s ready for your AI agents to use.

#### 🔹 1. Add a Summary
At the top of the note, write:  
```markdown
## Summary  
This article discusses OpenAI’s latest updates to their API, including new model capabilities and pricing changes.  
```

#### 🔹 2. Extract Key Points
List the most important details:  
```markdown
## Key Points  
- New model: `gpt-4o` with improved reasoning and multimodal support.  
- Pricing: 20% discount for developers using the OpenAI API.  
- API rate limits increased for enterprise users.  
```

#### 🔹 3. Add Relevance to Your System
Explain why this matters for your X post app or AI agents:  
```markdown
## Why It Matters  
- Enables more advanced X post generation with multimodal content.  
- Reduces costs for high-volume users.  
- Opens opportunities for new agent workflows (e.g., image-to-post generation).  
```

#### 🔹 4. Add Ideas for Future Use
Suggest how this could be used in your system:  
```markdown
## Ideas  
- Use `gpt-4o` for generating image captions for X posts.  
- Create a "cost-effective" agent for high-volume content creation.  
```

---

### 🔗 Step 3: Link to Related Notes
Use Obsidian’s **links** to connect this note to other parts of your wiki:  
```markdown
[[00-glossary/ai-agent]]  
[[03-agents/openai-api]]  
[[04-apps/x-post-app]]  
```

This creates a **knowledge graph** that your agents can traverse.

---

### 🏷️ Step 4: Add Tags (Optional but Powerful)
At the top of the note, add tags for grouping:  
```markdown
#openai #api #x-post-app  
```

This helps you filter notes later (e.g., click `#openai` to see all OpenAI-related notes).

---

### 🧹 Step 5: Clean Up the Raw Clip
1. Delete the raw article content (you’ve already extracted the key points).  
2. Keep only the structured sections:  
   - Summary  
   - Key Points  
   - Why It Matters  
   - Ideas  

---

### 🔄 Step 6: Sync to Server
Run your rsync command to
