---
title: Karpathy Style LLM Wiki
source_raw: web/Karpathy-Style LLM Wiki.md
compiled_at: 2026-04-17T16:23:13.085Z
type: concept
tags: [aiagentnerd, wiki, compiled]
---

# Karpathy Style LLM Wiki

# AIAgentNerd-Wiki Setup Guide  

## 🧰 Installation  
1. **Install Obsidian**  
   - Download from [obsidian.md](https://obsidian.md/)  
   - Install on your laptop (NOT server)  

2. **Install Web Clipper**  
   - Chrome Store: Search "Obsidian Web Clipper"  
   - Add to browser  

---

## 📁 Vault Setup  
1. **Create Vault**  
   - Open Obsidian → "Create new vault"  
   - Name: `AIAgentNerd-Wiki`  
   - Location: Local folder (e.g., `Documents/AIAgentNerd-Wiki`)  

2. **Folder Structure**  
   Create these folders in Obsidian:  
   ```  
   00-glossary  
   01-foundations  
   02-infrastructure  
   03-agents  
   04-apps  
   05-workflows  
   06-debugging  
   07-topics  
   raw/  
   templates/  
   ```  

3. **Key Files**  
   - `index.md` (navigation hub)  
   - `log.md` (timeline of actions)  
   - `x-post-app.md` (first note)  

---

## 🔐 Git Integration  
1. **Initialize Git**  
   - Open terminal in vault folder  
   - Run:  
     ```bash  
     git init  
     git add .  
     git commit -m "Initial AIAgentNerd wiki setup"  
     ```  

2. **Gitignore**  
   - Create `.gitignore` with:  
     ```  
     .obsidian/  
     ```  

---

## 🌐 Web Clipper Configuration  
1. **Connect to Vault**  
   - In Web Clipper settings:  
     - Vault: `AIAgentNerd-Wiki`  
     - Folder: `raw/web`  

2. **Test Clipping**  
   - Save an article → Verify in `raw/web` folder  

---

## 🔄 Sync with Server  
1. **Free Sync via rsync**  
   - On laptop:  
     ```bash  
     rsync -av ~/AIAgentNerd-Wiki/ nerd@nerd-server:~/aiagentnerd-wiki/  
     ```  
   - Create alias:  
     ```bash  
     alias syncwiki="rsync -av ~/AIAgentNerd-Wiki/ nerd@nerd-server:~/aiagentnerd-wiki/"  
     ```  

2. **Sync Habit**  
   - Run `syncwiki` after each session  

---

## 🧠 Mental Model Example  
Add to `x-post-app.md`:  
```  
## 🧠 Mental Model  
User clicks button → request goes to backend → backend calls LLM → response comes back → UI displays posts  
```  

---

## 📌 Tags (Optional)  
Add at top of notes:  
```  
#x-post-app #llm #app
