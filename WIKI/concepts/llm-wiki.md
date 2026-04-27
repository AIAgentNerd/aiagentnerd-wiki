# LLM Wiki #concept #core

## Key Insight
Don’t retrieve knowledge — compile and maintain it.

---

## What it is

A system where an LLM incrementally builds and maintains a structured, interlinked wiki from raw sources.

Instead of re-deriving answers each time (RAG), knowledge is compiled once and continuously improved.

---

## Mental Model

Raw → Wiki → Output

- Raw = source material (articles, videos)
- Wiki = structured knowledge (LLM maintained)
- Output = posts, answers, ideas

---

## Core Layers

### Raw
Immutable source material  
→ stored in `raw/`

### Wiki
Structured markdown knowledge  
→ stored in `wiki/`

### Schema
Rules for how the system works  
→ future: `AGENTS.md`

---

## Core Operations

### Ingest
- Add source
- LLM reads + extracts
- Updates multiple wiki pages

### Query
- Ask questions
- LLM answers using wiki
- Good answers get saved back

### Lint
- Detect contradictions
- Improve structure
- Suggest missing knowledge

---

## Why it matters

- knowledge compounds over time  
- eliminates repeated work  
- enables agent-based systems  
- foundation for AiAgentNerd  

---

## Connections

[[git-obsidian-setup]]
[[x-post-app]]
[[topic-brains]]

## Sources
[[Karpathy-Style LLM Wiki]]
