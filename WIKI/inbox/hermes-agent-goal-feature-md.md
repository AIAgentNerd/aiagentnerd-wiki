---
title: Hermes Agent /goal Feature — Persistent Objective System, Workflow, and Best Practices
type: wiki
category: inbox
source_raw: RAW/inbox/hermes-agent-goal-feature.md
compiled_at: "2026-05-11 22:50:25"
---

# Hermes Agent /goal Feature — Persistent Objective System, Workflow, and Best Practices

## Summary

This WIKI note was compiled from a RAW source by the Hermes-native memory profile.

## Key Knowledge


# Hermes Agent /goal Feature — Persistent Objective System, Workflow, and Best Practices


# Hermes Agent /goal Feature — Persistent Objective Workflow

## Core concept of /goal

The `/goal` feature gives Hermes Agent a persistent standing objective that survives across turns.

After every turn:
- Hermes evaluates whether the goal has been satisfied
- A judge system checks progress
- If incomplete, Hermes automatically continues the same session
- The agent keeps working toward the original objective

This creates:
- persistent focus
- long-running autonomous execution
- reduced distraction from intermediate debugging errors

Without `/goal`:
- agents may fall into debugging rabbit holes
- context drifts
- original objectives get forgotten

With `/goal`:
- the objective is reinforced every turn
- the agent keeps steering back toward the target


# Recommended /goal workflow

## Step 1 — Create a dedicated project folder

Very important concept:
Every project should live inside its own isolated workspace directory.

Example:
```bash
mkdir fighting-game
cd fighting-game
hermes
```
Benefits:

keeps files organized
isolates project memory/context
avoids cross-project confusion
gives Hermes clear file references

Without this:

files become scattered
future sessions become ambiguous
Hermes does not know which files belong to which project

Comparison made:
This is similar to proper IDE project setup before coding.

VPS / workspace observations

The creator mentions:

Hermes workspace directories may vary by installation
his workspace directory was called claude
possibly due to migration from OpenClaw

Key idea:
Project isolation matters more than directory naming.

Step 2 — Plan BEFORE building

Critical workflow recommendation:

Do NOT immediately run:

/goal build my app

Instead:

brainstorm with Hermes
define requirements
let Hermes ask questions
create architecture
create agents.md
only THEN execute /goal
agents.md importance

The creator strongly emphasizes agents.md.

Purpose:

synchronize project understanding
establish architecture
define stack/specs
persistent project memory artifact

Example sections:

overview
tech stack
game specifications
architecture

Observation:
Experienced Hermes workflows may automatically generate agents.md.

However:
new users may need to explicitly instruct Hermes to create it.

Example project used in the video

Project:
Simple browser-based fighting game.

Requirements:

two characters
attacks
health bars
keyboard controls
HTML5 canvas
JavaScript
simple but playable

Initial attempt:

Hermes immediately started building
insufficient planning
weak gameplay result
enemy AI missing

This demonstrated:
Why planning first matters.

Improved workflow

The creator corrected the workflow:

Prompt:

This game is not up to my expectation.
Look up official documentation.
Plan first.
Do not build yet.

Alternative:
Use:

/plan

Hermes then:

researched multiple sources
derived architecture decisions
created a structured plan

Only AFTER planning:

/goal build the fighting game according to the plan
Turn budget system

When /goal starts:
Hermes displays:

Goal set — 20 turn budget

Meaning:

Hermes may autonomously continue up to 20 internal turns
only counts continuation turns
not ordinary chat turns

Continuation turns occur when:

errors happen
loops happen
debugging is needed
retries occur
agent gets stuck
Configuring max turns

Config location:
hermesconfig.yaml

Section:

goals:
  max_turns: 20

Recommendations:

raise carefully
use increments of 5–10
examples:
25
30

Use larger budgets when:

project complexity is high
context is incomplete
insufficient visual references exist
agent must perform significant research
Example result from /goal

The second iteration successfully created:

combat mechanics
blocking
hitboxes
collision layers
combo system
special moves
AI opponent
difficulty modes
PvP
AI easy
AI hard

Important observation:
Graphics quality was low,
but functionality was achieved.

Key insight:
/goal is excellent for:

functional iteration
systems implementation
autonomous debugging
architecture completion

Less ideal for:

polished visuals
creative refinement
subjective design iteration
Iterative workflow philosophy

Recommended workflow after V1/V2 completion:

Return to the project directory and add:

reference images
documentation
style guides
gameplay references
visual inspiration

Especially useful with multimodal models.

Specific model mention:

Kimi 2.6 described as strong for frontend work

Workflow:

add references
re-plan
run /goal again
iterate toward higher quality versions
Possible future /goal improvements

The creator mentions a hallucinated command:

/goal sub

This does NOT currently exist.

However,
the concept proposed:

hierarchical sub-goals
parent/child task trees
decomposition of large projects

Example hypothetical breakdown:

core engine
combat system
special attacks
AI
UI

Each with independent turn budgets.

Interesting insight:
The hallucination may have been influenced by:

kanban parent-child task dependency memories
retrieval overlap between projects
Relationship with Kanban workflows

The creator notes:
/goal and kanban workflows currently have limited native synergy.

However:
/goal works very well during debugging inside larger kanban systems.

Example use:

/goal fix this error first

Then:

/goal fix error two

Especially useful when:

the agent loops
repeatedly asks clarifying questions
stops making progress
When NOT to use /goal

The creator explicitly recommends avoiding /goal for:

Simple single-turn tasks

Examples:

quick questions
tiny edits
one-shot commands
Brainstorming

Planning should happen BEFORE /goal.

Manual approval workflows

Avoid when:

you want human approval between iterations
you want tight supervision

Reason:

/goal assumes autonomous continuation
Production deployment

Avoid autonomous deployment loops directly to production.

Major takeaways
Proper Hermes workflow
Create isolated project folder
Enter workspace
Brainstorm with Hermes
Plan first
Create agents.md
Add documentation/references
Run /goal
Iterate in versions
Key conceptual insight

/goal is not:

a magic prompt enhancer

It is:

a persistence mechanism
an autonomous continuation system
a focus-preservation layer for long-running agent work

The true power comes from:

preparation
architecture
planning
context organization
environment setup
Relevance to AiAgentNerd / Hermes-native workflows

Strong parallels to AiAgentNerd architecture:

workspace isolation
project-specific memory
planning before execution
persistent task execution
iterative refinement
debugging loops
future parent-child task decomposition
autonomous continuation
mission-control style orchestration

Potential future integrations:

/goal + Deck task systems
/goal + Kanban orchestration
/goal + wiki-driven project memory
parent-child autonomous task trees
Goal persistence tied to compiled knowledge

Suggested future experimentation ideas
Goal decomposition

Possible future architecture:

parent goals
sub-goals
task graphs
dependency chains
Goal-aware memory retrieval

Improve:

retrieval precision
project isolation
long-running continuity
Workspace-native project templates

Potential reusable structure:

project/
├── agents.md
├── references/
├── specs/
├── assets/
├── notes/
├── tasks/
└── builds/
Overall conclusion

The video demonstrates that:

/goal is fundamentally a persistent autonomous execution framework
preparation matters more than prompting
planning is critical
isolated project environments are essential
agents.md acts as persistent project grounding
iterative refinement produces the best results
/goal is especially powerful for debugging and long-running implementation tasks

The creator also hints at the future evolution of Hermes toward:

hierarchical goals
autonomous project decomposition
stronger workflow orchestration
deeper persistent memory integration

## Source

- RAW: [[RAW/inbox/hermes-agent-goal-feature.md]]

## Tags

#aiagentnerd #hermes #memory #wiki
