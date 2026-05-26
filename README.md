# Forge App Development with AI

Research and presentation materials for the talk **"Forge App Development with AI: Agents, MCP Servers, and Skills"** by [Dugald Morrow](https://www.linkedin.com/in/dugaldmorrow/), Principal Developer Advocate at Atlassian.

---

## What is this repository?

This repository contains:

- **[Presentation.md](./Presentation.md)** — the full slide deck, covering AI coding agents, MCP servers, agent skills, and how to use them to build Forge apps
- **[PresentationMetadata.md](./PresentationMetadata.md)** — audience profile, tone, pacing, and content priorities for the deck
- **[PresentationFormat.md](./PresentationFormat.md)** — formatting conventions used in the presentation
- **[AGENTS.md](./AGENTS.md)** — agent context file that configures AI agents working in this repository
- **[.agents/skills/](./.agents/skills/)** — reusable agent skills for commit conventions, changelog management, and presentation best practices
- **[changelog/](./changelog/)** — a full version history of changes to the research and presentation

---

## Ask questions with an AI agent

This repository is designed to be used interactively with an AI coding agent. If you clone it and open it in an AI-agent-enabled tool — such as [Rovo Dev](https://www.atlassian.com/software/rovo), [Claude Code](https://claude.ai/code), or [Cursor](https://www.cursor.com) — the agent will have full context about the presentation and can answer questions like:

- *"Which AI agent should I use for Forge development?"*
- *"What is an MCP server and how do I configure one?"*
- *"What are the three levels of AI adoption described in the presentation?"*
- *"How do agent skills differ from MCP servers?"*

The [`AGENTS.md`](./AGENTS.md) file at the root of this repository acts as a standing brief for the agent, giving it the scope, personality, and key references it needs to answer questions accurately.

### Quickstart

```bash
git clone https://github.com/atlassian/forge-dev-with-ai-research.git
cd forge-dev-with-ai-research
# Open in your AI agent of choice (Rovo Dev, Claude Code, Cursor, etc.)
```

---

## Presentation overview

The presentation covers:

1. **The Agentic Shift** — why AI agents are fundamentally different from autocomplete tools
2. **The AI dev tool landscape** — four categories: AI coding agents, AI-native IDEs, IDE extensions, and hosted AI-native IDEs
3. **MCP Servers** — what they are, why they matter, and how to configure the Forge MCP Server
4. **Agent Skills** — reusable instruction sets that encode your team's workflows
5. **Forge as an AI target** — why Forge's constrained, declarative architecture makes it ideal for AI-assisted development
6. **A complete AI-driven workflow** — from prompt to deployed Forge app

### Key messages

- **MCP Servers are the connection** — they give any AI agent access to live Forge knowledge and Atlassian data
- **Agent Skills are the knowledge** — they encode your team's Forge workflows so the agent applies them consistently
- **Forge is the platform** — its constrained, declarative architecture makes it the ideal target for AI-assisted development

---

## Contributing

Contributions are welcome. Please sign a Contributor License Agreement (CLA) before submitting a pull request:

- **Corporate CLA**: [https://opensource.atlassian.com/corporate](https://opensource.atlassian.com/corporate)
- **Individual CLA**: [https://opensource.atlassian.com/individual](https://opensource.atlassian.com/individual)

---

## License

Copyright @ 2026 Atlassian Pty Ltd

Licensed under the [Apache License, Version 2.0](./LICENSE.txt).
