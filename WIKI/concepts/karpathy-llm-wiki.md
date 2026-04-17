# Compiled Note

**Source RAW file:** `web/Karpathy-Style LLM Wiki.md`

---

# Karpathy-Style LLM Wiki

## Summary

The Karpathy-Style LLM Wiki is a structured, chapter-based knowledge system designed to capture and organize everything learned while building TaskNerd. Instead of scattered information, it creates a personal and product knowledge wiki that can evolve into internal documentation, system documentation, and potentially a public learning resource.

## Key Concepts

- **Structured Knowledge System**: Organized into clear chapters following a consistent format
- **Karpathy-Style**: Not just commands, but understanding with concepts, mental models, and real debugging stories
- **Compounding Asset**: Knowledge that grows over time and becomes increasingly valuable
- **Personal + Product Knowledge**: Combines individual learning with product development insights

## Important Details

### Chapter Structure (Critical Format)

Each chapter must follow this exact template:
1. **What it is**: Simple explanation in plain language
2. **Why it matters**: Why this concept is important in your system
3. **How we set it up**: Step-by-step commands and actions
4. **Common errors**: Real problems encountered
5. **How we fixed them**: Actual solutions (this is gold)
6. **Final setup (standard)**: What you decided to use going forward

### Additional Elements

- **Mental Model Layer**: Added to every important chapter explaining how concepts fit into the system
- **Connections Section**: How each chapter connects to other chapters, creating a knowledge graph
- **Glossary**: Simple definitions for technical terms to reduce confusion over time

### Implementation Approach

1. **Start Simple**: Use markdown files in a folder, edit in VS Code
2. **Upgrade Later**: Convert to docs site using Docusaurus, Nextra, or MkDocs after content exists
3. **Consistency**: Uniform formatting across all chapters

## Relevance to AIAgentNerd / Tasknerd

The Karpathy-Style LLM Wiki serves as the foundational knowledge system for TaskNerd, transforming scattered information into structured, reusable, and scalable knowledge. It becomes the "brain" of the system, feeding into agents like Atlas (knowledge) and Drift (research), and providing the foundation for future automation and documentation.

The wiki approach enables TaskNerd to evolve from a simple tool into a comprehensive intelligence system that compounds user knowledge over time, making it increasingly valuable as users build their personal research memory systems.
