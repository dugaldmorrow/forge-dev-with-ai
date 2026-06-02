# Illustration Specifications

Visual design specs for diagrams to be created for the presentation. Each illustration is referenced to the slide it belongs to.

---

## Illustration 1

**Slide:** "AI agents pursue goals across many steps — they plan, execute, and iterate" (Slide 4)

**Title:** The Agent Reasoning Loop

A circular flow diagram with five steps arranged in a loop:

1. **Goal** (top) — "Build a Jira issue panel showing related Confluence pages"
2. **Plan** (right) — agent decides next action: "Read PROJ-123 via Atlassian MCP"
3. **Execute** (bottom-right) — agent calls tools: reads files, writes code, runs tests
4. **Observe** (bottom-left) — agent reads results: test output, file contents, API responses
5. **Iterate** (left) — agent refines: adjusts plan based on what it observed

An arrow from step 5 back to step 2 closes the loop. A dashed arrow exits the loop from step 3 labeled **"Goal achieved — hand back to developer"**.

A small human figure sits outside the loop with a two-way arrow labeled **"Human-in-the-loop"** — they can inject guidance at any point but don't need to be present for every step.

Style: clean diagrammatic, Atlassian blue primary colour, minimal text on diagram elements.

---

## Illustration 2

**Slide:** "MCP is the universal adapter for AI agents — one standard, any tool" (Slide 13)

**Title:** MCP — One Standard, Any Tool

A two-panel "before and after" comparison:

**Before MCP (left panel — messy, red tones):**
A tangled web of lines connecting 4 AI apps (Claude, Cursor, Rovo Dev, ChatGPT) to 5 tools (Jira, GitHub, Forge, Slack, Postgres). Every app has its own custom line to every tool — 20 crossing lines total, visually chaotic. Label: "N×M custom integrations".

**After MCP (right panel — clean, blue/green tones):**
The same 4 AI apps on the left, each connecting to a single central vertical bar labeled "MCP". The same 5 tools on the right, each connecting to the same bar. Clean parallel lines, no crossing. Label: "N+M standard connections".

Below the two panels, a row of three icons labeled **Tools**, **Resources**, **Prompts** — the three MCP primitives — each with a one-line description.

Style: split-panel layout, high contrast between the messy left and clean right, Atlassian brand colours.

---

## Illustration 3

**Slide:** "Agent skills are reusable instruction sets — they teach AI your team's specific way of working" (Slide 18)

**Title:** Progressive Disclosure — Skills Load Only When Needed

A horizontal three-stage flow:

**Stage 1 — Discover (left):**
A session startup icon. Below it, a small table showing 4 skill names and one-line descriptions being loaded — labelled "~100 tokens per skill". Visual emphasis: small, lightweight.

**Stage 2 — Activate (centre):**
A task prompt bubble: "Build a Forge app for Jira". An arrow points to one skill card (Forge App Builder) highlighted and expanding outward — the other skill cards stay small and greyed out. Label: "Full SKILL.md loaded — only when relevant".

**Stage 3 — Execute (right):**
The agent following step-by-step instructions from the expanded skill, with a `references/` folder opening beside it. Label: "Instructions + referenced files loaded on demand".

A token counter graphic runs across the bottom showing cost at each stage: tiny at Discover, moderate at Activate, zero extra cost for unused skills.

Style: left-to-right flow with expanding/contracting card metaphor, Atlassian blue for the active skill, grey for inactive ones.

---

## Illustration 4

**Slide:** "Agent context files give every session a standing brief" (Slide 26)

**Title:** The AGENTS.md Hierarchy — Layers of Context

A nested layer diagram, like a stack of translucent sheets viewed from the side:

**Layer 1 (bottom, widest — grey/global):** `~/.rovodev/AGENTS.md` — labelled "Your personal defaults: preferred language, timezone, coding style. Applies to every project."

**Layer 2 (middle — blue/team):** `./AGENTS.md` — labelled "Team standards: architecture, build commands, coding conventions. Committed to git — shared with all teammates."

**Layer 3 (narrower — teal/subdirectory):** `./src/AGENTS.md` — labelled "Specialist rules: only applied when working in this directory."

**Layer 4 (top, smallest — orange/local):** `AGENTS.local.md` — labelled "Personal overrides: gitignored, your machine only."

An arrow on the right side points downward labeled "Higher specificity wins". A lock icon on Layer 4 indicates gitignored.

Style: layered/stacked card metaphor, each layer a different colour, clean labels, Atlassian palette.

---

## Illustration 5

**Slide:** "Agent + MCP Servers + Skills + Forge CLI = a complete AI-driven Forge development workflow" (Slide 37)

**Title:** The AI Forge Developer Stack — How It All Fits Together

A layered architecture diagram with four horizontal bands stacked vertically, each a different colour:

**Band 1 — Developer (top, lightest):**
A developer icon on the left with a speech bubble: "Build a Jira issue panel that shows related Confluence pages. See PROJ-123."
On the right: a "Review & approve" icon. Label: "You set the goal and review the result."

**Band 2 — AI Agent (blue):**
Three agent logos side by side: Rovo Dev · Claude Code · Cursor. Label: "Plans, writes code, runs tools, iterates."

**Band 3 — Extensions (teal), split into two columns:**
Left column — **MCP Servers:**
- 🔶 Forge MCP → "Forge knowledge"
- 🔷 Atlassian MCP → "Jira · Confluence · Bitbucket"

Right column — **Agent Skills:**
- 📋 Forge App Builder
- 📋 Forge App Review
- 📋 Commit · Changelog

**Band 4 — Platform (darkest, bottom):**
The Forge logo with three items: `forge tunnel` · `forge deploy` · `forge install`
Label: "Atlassian-managed serverless infrastructure — no servers to configure."

Vertical arrows connect the bands downward: Developer → Agent → Extensions → Platform. A return arrow on the right side goes back up from Platform to Developer labeled "Deployed app".

Style: stacked band layout, Atlassian brand palette (blue → teal → slate), clean iconography.
