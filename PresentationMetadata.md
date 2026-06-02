# Presentation Metadata

This file documents the audience profile and presentation preferences for [Presentation.html](./Presentation.html). It is intended to guide content decisions, tone, depth calibration, and future updates to the deck.

---

## Presenter

**Dugald Morrow**  
Principal Developer Advocate, Atlassian

---

## Audience Profile

### Who they are

The primary audience is **professional and aspiring software developers**, with a particular interest in building apps on the Atlassian platform using Forge. The audience is expected to attend events such as developer conferences, Atlassian community meetups, and developer advocacy sessions.

### Technical experience

The audience has **varied technical experience** — from developers who are relatively new to Forge and AI tooling through to experienced engineers who are already using AI coding agents in their daily workflow. The presentation should serve both ends of this spectrum:

- For **less experienced attendees**: clear definitions, practical examples, and a low-friction on-ramp (e.g. the Three Levels of Adoption path)
- For **more experienced attendees**: technical depth, honest caveats, concrete code examples, and nuanced discussion of topics such as MCP invocation discretion and skill enforcement

### What they know coming in

- Most will have some familiarity with Atlassian products (Jira, Confluence, Forge)
- Most will have used an AI coding tool (GitHub Copilot or similar autocomplete)
- Fewer will have experience with AI coding *agents* (Rovo Dev, Claude Code, Cursor agent mode, etc.)
- Fewer still will have configured MCP servers or agent skills

### What they want to leave with

- A clear mental model of what AI agents are and why they're different from autocomplete
- Practical knowledge of the tools available today (agents, MCP servers, skills, App Studio)
- At least one thing they can do in the next 10 minutes (add the Forge MCP Server to their current AI tool)
- Confidence that AI-assisted Forge development is ready for production use — not just a demo

---

## Presentation Preferences

### Tone

- **Professional and confident** — this is a public presentation to a technical audience
- **Honest and balanced** — acknowledge limitations (e.g. discretionary MCP invocation, hallucination risks) rather than presenting an uncritically positive view
- **Practical, not inspirational** — the audience values actionable takeaways over vision statements; every slide should earn its place by telling the audience something useful

### Technical depth

- **Technical where necessary** — do not shy away from code examples, config blocks, or CLI commands where they add value
- **Accessible framing first** — introduce concepts with a plain-language summary before going deep; use analogies (USB-C for MCP, npm for `npx skills`) to anchor new ideas
- **No dumbing down** — the audience is intelligent and time-constrained; assume competence and respect their time

### Slide content

- **Action titles** — every slide title should be a complete sentence that states the conclusion, not a generic topic label
- **One idea per slide** — if a slide needs two titles, it needs to be two slides
- **Concrete examples** — use real tool names, real commands, real config blocks; avoid generic placeholders
- **Tables for comparisons** — use tables to compare agents, tools, techniques; keep columns to 4–5 maximum
- **Code blocks for anything runnable** — commands, JSON config, SKILL.md snippets, AGENTS.md examples

### Speaker notes

- Speaker notes should be **detailed enough for someone to present the deck without prior context**
- Include: key talking points, background not on the slide, anticipated questions, transition cues
- Do **not** simply repeat what is written on the slide
- Notes may include honest caveats, real-world anecdotes, and technical depth that would be too much for the slide itself

### Length and pacing

- The deck is designed for a **session of approximately 45–60 minutes** including Q&A
- Q&A should take place **before** the final closing slide, so the session ends on the key message rather than on a random audience question
- Slides are expected to be viewed at approximately **1–2 minutes per slide** for content-heavy slides; shorter for section breaks and overview slides

### Visual style

- The deck is authored in HTML (`Presentation.html`) and rendered with Reveal.js using the conventions defined in [PresentationFormat.md](./PresentationFormat.md)
- ASCII art diagrams and code blocks are used where visual structure aids comprehension
- Illustrations are described in `<details>` blocks for slide designers to implement as proper graphics

---

## Content Priorities

When making decisions about what to add, cut, or modify, prioritise in this order:

1. **Forge-specific content** — this is a Forge-focused presentation; generic AI content should serve as framing only
2. **Actionable takeaways** — every section should leave the audience with something they can do
3. **Technical accuracy** — facts, version numbers, dates, and pricing must be current and verifiable
4. **Narrative coherence** — the presentation should tell a single coherent story from hook to close
5. **Completeness** — coverage of the landscape is important but secondary to depth on the core topics

---

## Key Messages

The three things every audience member should leave knowing:

1. **MCP Servers are the connection** — they give any AI agent access to Forge knowledge and Atlassian data
2. **Agent Skills are the knowledge** — they encode your team's Forge workflows so the agent applies them consistently
3. **Forge is the platform** — its constrained, declarative architecture makes it the ideal target for AI-assisted development

---

## Known Audience Concerns to Address

Based on typical developer audiences for this topic:

- *"Does AI actually work for real Forge development, or just demos?"* — Address with production evidence, real pricing, and the autonomous agent workflow example
- *"Which tool should I use?"* — Address with the four-category classification and the Three Levels adoption path
- *"What about hallucinations and reliability?"* — Address directly with the hallucinations slide and the MCP invocation discretion slides
- *"Is this going to be expensive?"* — Address with Forge's free tier, token cost context, and LLMflation trend
- *"Do I need to replace my current tools?"* — Address with the IDE extensions category and the "any tool + MCP" message

---

## References

- [Presentation.html](./Presentation.html) — the full slide deck
- [PresentationFormat.md](./PresentationFormat.md) — formatting conventions for the deck
- [AGENTS.md](./AGENTS.md) — agent personality, scope, and boundaries for this project
