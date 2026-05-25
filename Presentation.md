
# Forge App Development with AI

A presentation about AI-assisted software development, with a focus on building Forge apps using AI agents, MCP servers, and agent skills.

---

## Slides

### Forge App Development with AI: Agents, MCP Servers, and Skills

**Dugald Morrow**  
Principal Developer Advocate, Atlassian

*A practical guide to building Forge apps with AI agents, MCP servers, and agent skills — from idea to deployed.*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- The title slide is on screen while the audience settles — no speaking needed
- Allow the visual to set the tone; move to the next slide once the room is ready
- This session is practical: the audience will leave with something they can apply today

</details>

---

### What we'll cover today

1. **The Agentic Shift** — why agents are different from autocomplete
2. **The Landscape** — four categories of AI dev tools and the major players
3. **The Standards** — MCP Servers and Agent Skills
4. **Forge as an AI Build Target** — why Forge is uniquely suited
5. **Getting Started** — three levels of adoption you can start today

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- Keep this brief — 30 seconds maximum; the agenda is a map, not the journey
- Transition: "Let's start with the shift that makes all of this relevant — what exactly is an AI software development agent, and why is it different from the autocomplete tools most of us use today?"

</details>

---

### The AI revolution is here — and software development is its most definitive use case

> *"In 2026, AI wrote more code than all human developers combined for the first time in history."*

**How long did your last Forge app take to build from idea to deployed?**

What if that was 20 minutes?

This session covers the tools, standards, and patterns that make it possible today.

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- Open with the statistic — let it land before moving on
- Pose the question to the room: ask for a show of hands — who has built a Forge app? Who has used an AI agent to do it?
- The goal of this session is practical: leave with something you can apply today, not just inspiration
- Transition: "Let's start with the foundation — what exactly is an AI software development agent?"

</details>

---

### AI agents pursue goals across many steps — they plan, execute, and iterate

An AI software development agent is an autonomous system powered by a large language model (LLM) that can plan, reason, use tools, and execute multi-step coding tasks with minimal human intervention. Unlike a chatbot that answers one question at a time, an agent pursues a *goal* — reading your codebase, writing code, running tests, fixing failures, and iterating — until the job is done.

**Key characteristics:**
- 🎯 **Goal-directed** — works toward a defined objective across many steps
- 🔧 **Tool use** — reads/writes files, runs terminal commands, calls APIs, browses the web
- 🔁 **Reasoning loops** — plans, executes, observes results, and adjusts
- 🧠 **Context-aware** — understands your codebase, project structure, and prior work
- 🤝 **Human-in-the-loop** — works *with* you, not just *for* you

<details>
<summary>Illustration</summary>

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

</details>

> *In August 2025, New York Magazine described software development as the most definitive use case of AI agents.*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

An AI software development agent is fundamentally different from a code completion tool or a chatbot. The key insight is autonomy combined with tool use — the agent doesn't just suggest code, it actually executes a plan across multiple steps.

Think of it like the difference between asking a colleague "how would you fix this bug?" versus handing a colleague your laptop and saying "fix this bug and open a PR when you're done." The agent takes the second role.

The reasoning loop is critical: the agent observes the current state of the codebase, plans what to do, executes actions (writes code, runs tests), observes the results, and repeats until the goal is achieved. This is fundamentally different from autocomplete.

Software development is a particularly strong fit for AI agents because:
- Goals are clearly defined (tests pass, code compiles, acceptance criteria met)
- Feedback loops are fast (run the tests, see if it worked)
- The environment is structured (files, APIs, CLIs)
- Mistakes are recoverable (git, version control)

</details>

---

### Autocomplete tools predict the next token — agents pursue goals across many steps

| | Autocomplete (e.g. GitHub Copilot) | AI Agent (e.g. Rovo Dev) |
|---|---|---|
| **Mental model** | High-speed typewriter | Digital teammate |
| **How it works** | Predicts the next token based on context | Pursues a goal across a multi-step reasoning loop |
| **Input** | Your current cursor position | A task or objective |
| **Output** | A code suggestion | A completed feature, fix, or deployment |
| **Iteration** | You iterate | The agent iterates |
| **Tool use** | ❌ None | ✅ Files, terminal, APIs, web |

> The shift from autocomplete to agents is not incremental — it is a fundamentally different relationship with AI.

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- Most developers in the room have used GitHub Copilot or a similar autocomplete tool — this slide gives them permission to update their mental model
- Autocomplete is not obsolete — it's a different tool for a different job; agents are for multi-step, goal-directed work; autocomplete is for in-the-moment code suggestions
- The key mental shift: autocomplete augments the developer's typing; agents augment the developer's *thinking and execution*
- Transition: "Before we go further into agents, let's quickly cover inference — the underlying mechanism that makes all of this possible."

</details>

---

### Inference is AI in "execution" mode — what happens every time an LLM runs

**Inference** is the execution phase of an AI model — when a trained model receives an input (a prompt) and generates an output (a response). Every time an LLM generates code, answers a question, or takes an action, it is performing inference.

> 💡 **The cost story:** *By 2030, running inference on a 1-trillion-parameter model will cost over 90% less than in 2025.* Agentic AI is getting dramatically cheaper every year.

**Why it matters for developers:**

| Concept | What it means |
|---|---|
| **Token-based billing** | You pay per token — every word in and out has a cost |
| **Agentic amplification** | Agents use 5–30× more tokens per task than a chatbot |
| **Context window** | The "working memory" of a session — longer context = more tokens |
| **LLMflation** | Inference costs drop ~10× per year — rapidly becoming cheaper |

#### Speaker notes

<details>
<summary>Speaker notes</summary>

Inference is the "using" phase of an AI model — as opposed to training, which is the "learning" phase. When you type a prompt and get a response, that's inference.

Why this matters: inference costs money. Every token (roughly ¾ of a word) that flows in or out of the model is billed. This becomes very significant in agentic workflows because:

1. The agent reads your entire codebase (many input tokens)
2. The agent has long multi-step conversations (context grows with each step)
3. Each step re-feeds the full history into the model
4. Agentic models use 5–30× more tokens than a standard chatbot per task

The good news: "LLMflation" — the a16z term for the rapid decline in inference costs — is real. What cost $10 per million tokens in 2023 costs a fraction of that today. The trend is accelerating.

For Forge developers: when using AI agents to build Forge apps, you will consume tokens. Understanding this helps you choose the right model (cheaper models for simple tasks, frontier models for complex reasoning) and use skills to avoid re-explaining context every session.

</details>

---

### AI development tools fall into four categories — each offering a different level of autonomy

Not all AI development tools are the same. For this presentation, we classify them into four categories based on depth of integration and degree of autonomy:

```
┌─────────────────────────────────────────────────────────────────┐
│                   AI DEV TOOL CATEGORIES                        │
├──────────────────────┬──────────────────────────────────────────┤
│  AI SOFTWARE         │  Autonomous agents that work in your     │
│  DEVELOPMENT AGENTS  │  terminal or in the background.          │
│                      │  Rovo Dev, Claude Code, Codex CLI,       │
│                      │  Google Antigravity 2.0, Devin, Cline   │
├──────────────────────┼──────────────────────────────────────────┤
│  AI-NATIVE IDEs      │  Full IDEs rebuilt around AI — not just  │
│                      │  a plugin bolted on.                     │
│                      │  Cursor, Windsurf, Replit                │
├──────────────────────┼──────────────────────────────────────────┤
│  IDE EXTENSIONS &    │  AI capabilities added to your existing  │
│  EDITOR COMPANIONS   │  IDE. Lowest friction to adopt.          │
│                      │  GitHub Copilot, JetBrains AI, Tabnine  │
├──────────────────────┼──────────────────────────────────────────┤
│  HOSTED AI-NATIVE    │  Cloud-based, often no-code platforms.   │
│  IDEs                │  Atlassian App Studio, Lovable,          │
│                      │  Bolt.new, v0.dev                        │
└──────────────────────┴──────────────────────────────────────────┘
```

**The key question when choosing:** *How much autonomy do you want the AI to have?*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

This classification helps developers choose the right tool for the right job. The spectrum moves from "AI assists me" (extensions) through to "AI works for me" (agents).

**AI Software Development Agents** are the most autonomous. You give them a goal and they work — potentially for hours — without needing you to intervene. They live in your terminal or run as background workers.

**AI-Native IDEs** are full development environments where AI is baked into every interaction. Cursor is the best example — it's a fork of VS Code rebuilt entirely around AI. Every feature (autocomplete, chat, multi-file editing, agents) is first-class, not an afterthought.

**IDE Extensions** are the most conservative option — you keep your existing IDE (VS Code, IntelliJ) and add AI as a plugin. Less integrated, but lower switching cost. Good starting point for teams nervous about changing workflows.

**Hosted AI-Native IDEs** are cloud platforms where the entire stack (IDE, hosting, database, AI) is managed for you. Great for getting started fast, especially for non-developers. Atlassian App Studio falls here — describe what you want and it builds a Forge app.

There's no single right answer — it depends on the task, your team, and your comfort level. Many developers use multiple categories for different purposes.

</details>

---

### Six major AI coding agents are available today — each with a different LLM and autonomy model

The most autonomous category — agents that independently plan, write, test, and ship code.

| Agent | Creator | Distinctive Feature |
|---|---|---|
| **Rovo Dev** | Atlassian | Atlassian Teamwork Graph — Jira, Confluence, Bitbucket, Compass context |
| **Claude Code** | Anthropic | Agent View + /goal; supervisor Claude verifies results |
| **Codex CLI** | OpenAI | ~4M weekly users; open source; Goal mode for multi-day tasks |
| **Google Antigravity 2.0** | Google | Multi-model routing; launched May 19 2026 at Google I/O |
| **Devin** | Cognition AI | First "autonomous AI software engineer"; Interactive Planning; from $20/mo |
| **Cline** | Community (MIT) | 5M+ installs; bring your own API key; fully open source |

> *Claude Code and Devin 2.0 lead SWE-bench Verified benchmarks at ~71–73% task completion (up from ~14% at Devin's 2024 launch).*

---

### LLM configurability varies widely — choose the agent that fits your model preferences

| Agent | LLMs | Configurable? |
|---|---|---|
| **Rovo Dev** | GPT, Claude, Gemini + open-source | Limited (switch with /model) |
| **Claude Code** | Claude only (Opus/Sonnet/Haiku) | Yes (/model command) |
| **Codex CLI** | GPT-5.x series; local via Ollama | Yes (/model command) |
| **Google Antigravity 2.0** | Gemini (default), Claude, GPT-OSS | Yes |
| **Devin** | Proprietary SWE-1 / SWE-1.5 | ❌ No |
| **Cline** | 200+ models (Claude, GPT, Gemini, Ollama…) | Yes — fully |

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- Cline is the most flexible — bring your own API key for any model; ideal for teams with specific model requirements or cost constraints
- Claude Code is locked to Anthropic models — a significant constraint if your organisation requires model diversity or has Anthropic API limits
- Devin has no configurability — you use Cognition's proprietary SWE model; tradeoff is it's optimised specifically for software engineering tasks
- Rovo Dev model switching is limited to /model command; enterprise customers can configure defaults via admin settings
- For Forge development: model choice matters less than MCP + skills configuration — a well-configured smaller model often outperforms a frontier model without Forge context

Let's look at each major agent:

**Rovo Dev (Atlassian)** — Atlassian's own coding agent. Distinctive because of the Teamwork Graph — it understands your Jira issues, Confluence docs, Bitbucket PRs, and Compass components, connecting context across your whole project. Available included with Standard, Premium, or Enterprise Cloud plans of Jira, Confluence, or JSM.

**Claude Code (Anthropic)** — Lives in your terminal. The May 2026 "Code with Claude" event introduced Agent View (manage a fleet of agents from one interface) and the /goal command (give an objective, the agent pursues it with a second supervisor Claude verifying the result). Works with Opus 4.6, Sonnet 4.6, Haiku 4.5 models. Enterprise: Amazon Bedrock or Google Vertex AI.

**Codex CLI (OpenAI)** — Open source (Rust), runs locally. NOT the original Codex API from 2021. Launched April 2025, now ~4M weekly active users (confirmed April 2026). Available as CLI, web (chatgpt.com/codex), IDE extensions, and Codex app. Goal mode for multi-hour/multi-day objectives. Powered by GPT-5.5.

**Google Antigravity 2.0** — Brand new, launched May 19 2026 at Google I/O. Desktop app + CLI (`agy`) + SDK + Gemini API managed agents tier. Powered by Gemini 3.5 Flash. Multi-agent parallel orchestration and scheduled background tasks. AI Ultra plan ($100/mo) for 5× higher limits.

**Devin (Cognition AI)** — The "first autonomous AI software engineer." Devin 2.0 (April 2025) slashed price from $500 to $20/month (Core plan). Interactive Planning: analyses your codebase, proposes a plan, lets you iterate together. Parallel Devins. SWE-bench: 71%. Real-world complex task completion: ~14-15% (independent testing).

**Cline** — MIT licensed, 5M+ installs, 58,000+ GitHub stars. Runs inside VS Code. Bring your own API keys (Claude, OpenAI, Gemini, or local via Ollama). The open-source choice for transparency and control. Lightweight extension — keep your existing VS Code setup.

</details>

---

### Rovo Dev is the only agent with full Atlassian context — Jira, Confluence, Bitbucket, and Forge

Rovo Dev is Atlassian's context-aware AI coding agent, built for the full software development lifecycle and deeply integrated with the Atlassian ecosystem.

**What makes Rovo Dev different:**

- 🧠 **Teamwork Graph** — knows your Jira issues, Confluence docs, Bitbucket PRs, Compass components
- 🔄 **Full lifecycle** — plan, generate, review, and ship code without leaving the terminal
- 🔌 **MCP-powered** — extensible via MCP servers (Forge, Jira, GitHub, and more)
- 📋 **Skills-enabled** — teach it your team's workflows via reusable skill files
- 🔶 **Forge-aware** — with the Forge MCP Server, understands Forge modules, manifests, and APIs

**Availability:** Included with Standard, Premium, or Enterprise Cloud plans of Jira, Confluence, JSM, or Teamwork Collection — no additional licence required. Each plan includes **2,000 Rovo Dev credits per user/month**; usage beyond that incurs charges of $0.01 per credit. Admins can set per-user limits and enable or disable overage charges.

```
Rovo Dev CLI ──► Forge MCP Server    (Forge knowledge)
             ──► Atlassian MCP Server (Jira, Confluence, Bitbucket)
             ──► Teamwork Graph       (project context)
             ──► Agent Skills         (team workflows)
```

#### Speaker notes

<details>
<summary>Speaker notes</summary>

Rovo Dev is the most relevant agent for this audience — it's purpose-built for Atlassian customers and has special Forge awareness.

The Teamwork Graph is the key differentiator. When you ask Rovo Dev to implement a feature, it doesn't just look at the code — it looks at the Jira issue describing the feature, the Confluence page with the design spec, the previous PRs that touched related code, and the Compass component ownership. That's context no other agent has access to.

MCP integration means Rovo Dev is extensible. Connect the Forge MCP Server and it gains deep knowledge of Forge modules, manifest syntax, API scopes, and common patterns. This dramatically reduces hallucination when building Forge apps.

Real-world evidence: a developer ran a challenge where they didn't write any code themselves — letting the Rovo Dev agent do all the work. When adding Jira API calls, the agent automatically updated the manifest with the required scopes — something developers routinely forget manually and that causes apps to fail in production.

Forge CLI now offers AI-powered assistance through Rovo CLI and Gemini CLI integration — the agent analyses errors from forge commands or tunnels and suggests actionable fixes automatically.

The agent helps developers understand new codebases, implement features with web-integrated research via MCP servers, and assist in complex code migrations — all without leaving the terminal.

</details>

---

### AI-native IDEs rebuild the entire editor around AI

Full development environments rebuilt from the ground up around AI — not plugins added to existing tools.

| IDE | Creator | LLMs | Configurable? | Pricing (Pro) |
|---|---|---|---|---|
| **Cursor** | Anysphere | Claude, GPT, Gemini, Grok + proprietary Composer | Yes — per-conversation | $20/mo |
| **Windsurf** | Codeium / Cognition | Proprietary SWE-1.5/1.6, Claude, GPT + BYOK | Yes — dropdown in Cascade | $15/mo |
| **Replit** | Replit Inc. | Managed (not user-selectable) | ❌ No | $17/mo |

**Cursor vs Windsurf (May 2026):**

```
Both: ~$20/mo Pro | 200K token context | multi-file agentic editing
Cursor:   multi-model freedom · VS Code familiarity · largest community
Windsurf: proprietary SWE-1.5 (13× faster) · 40+ IDE plugins · FedRAMP/HIPAA/ITAR
```

#### Speaker notes

<details>
<summary>Speaker notes</summary>

AI-Native IDEs differ from extensions because AI is baked into the core architecture, not bolted on. This allows deeper integration — the IDE can modify the entire editing experience around AI workflows.

**Cursor** is the market leader by a wide margin. Reached $2B ARR in February 2026 (doubling from $1B in three months — reportedly the fastest-growing SaaS product in history). $29.3B valuation after Series D. 2M+ users, 1M+ paying customers, 50% Fortune 500 adoption. Cursor v3 (April 2026) added Background Agents and Cloud Agents — the developer orchestrates agents rather than writing code. Model support: Claude Opus/Sonnet 4.7, GPT-5.5, Gemini 2.5 Pro, Grok 4, plus Cursor's own Sonic (Tab) and Composer-1 (multi-file) models.

**Windsurf** (acquired by Cognition AI for ~$250M in late 2025). Cascade agent tracks all your actions — edits, clipboard, terminal commands — to infer intent and stay aligned with your current task. Proprietary SWE-1.5 model is 13× faster than Claude Sonnet 4.5 while approaching similar quality. 40+ IDE plugins — a key advantage for teams that won't leave JetBrains. FedRAMP, HIPAA, ITAR compliance for regulated industries. March 2026 pricing change from credits to quotas triggered user backlash.

**Replit** is cloud-only — no installation, runs entirely in the browser. Replit Agent 3 builds complete web apps from natural language with effort-based pricing. Full stack: editor, hosting, database, AI agent in one browser window. Best for education, rapid prototyping, and zero-setup requirements. Hidden cost risk: effort-based billing can result in $100–300/month bills when expecting $25/month.

For Forge development: Cursor and Windsurf both work excellently with the Forge MCP Server — configure it in settings and the agent gains Forge-specific knowledge immediately.

</details>

---

### IDE extensions add AI to your existing editor — the lowest-friction path to AI-assisted development

AI capabilities added to your existing IDE — the lowest-friction path to AI-assisted development.

| Extension | Creator | LLMs | Configurable? | Pricing |
|---|---|---|---|---|
| **GitHub Copilot** | Microsoft / GitHub | GPT-5.5, GPT-5.4, Claude Sonnet 4.6, Claude Haiku 4.5 | Yes — user or admin selectable | Free / $10 / $39 / mo |
| **JetBrains AI Assistant** | JetBrains | Claude (Anthropic), Gemini, GPT via BYOK; proprietary Mellum for completions | Yes — BYOK supported | $10 / $20 / $30 / mo |
| **Tabnine** | Tabnine | Privacy-first; multiple models; self-hosted / air-gapped available | Yes — enterprise model config | $12–$39/mo |

**GitHub Copilot in 2026:**
- Autonomous PR creation agent
- Agentic code review
- GitHub Spark (natural language app building)
- Multi-model: Claude Opus/Sonnet, GPT-4o, Gemini
- Note: moving toward token-based billing in mid-2026

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- Extensions are the lowest-friction entry point — keep your existing editor and workflow, add AI on top
- **GitHub Copilot** — most widely adopted AI coding assistant globally; works in VS Code, JetBrains, Neovim, Visual Studio; evolved far beyond autocomplete into agent mode, autonomous PR creation, and GitHub Spark; 5-tier pricing: Free → Pro ($10) → Pro+ ($39) → Business ($19/user) → Enterprise ($39/user); transitioning to token-based billing mid-2026 — heavy agentic users will see cost increases
- **JetBrains AI Assistant** — natural choice for Java/Kotlin/Python on IntelliJ/PyCharm/WebStorm; type-aware completions grounded in actual syntax trees; Junie (Jan 2026) is their autonomous full-task agent; requires a separate subscription from the IDE licence; AI Pro $10/mo, AI Ultimate $30/mo
- **Tabnine** — the privacy-first option; zero code retention, no training on your code; self-hosted deployment (VPC, on-premises, air-gapped); right choice for regulated industries; $12/mo (Dev), $39/user/mo (Enterprise); retired free plan in 2024

</details>

---

### All major hosted AI IDEs now support MCP — including the Forge MCP Server

Cloud-based platforms where the entire development experience — IDE, hosting, AI, and often database — is managed for you. Typically low-code or no-code.

All five platforms support MCP servers — meaning any of them can connect to the Forge MCP Server via a custom MCP configuration, giving their AI agents Forge knowledge.

| Platform | Creator | Best For | MCP Support | Forge-native? |
|---|---|---|---|---|
| **Atlassian App Studio** | Atlassian | Building Forge apps via natural language; no code required | ✅ Native | ✅ Yes |
| **Lovable** | Lovable | Full-stack web app MVPs from prompts; $100M ARR in 8 months | ✅ Custom MCP on paid plans | ⚙️ Via Forge MCP |
| **Bolt.new** | StackBlitz | Browser-based dev; visible code; zero local setup | ✅ Custom MCP | ⚙️ Via Forge MCP |
| **v0.dev** | Vercel | React/Tailwind UI component generation | ✅ Custom MCP | ⚙️ Via Forge MCP |
| **Replit** | Replit Inc. | Cloud coding + hosting + DB + AI agent | ✅ 1-click + custom MCP | ⚙️ Via Forge MCP |

> **The tradeoff:** Maximum speed to prototype — but general-purpose platforms often hit a "Technical Cliff" at production deployment. App Studio avoids this because Forge handles hosting, auth, and scaling automatically.
>
> ⚙️ *Via Forge MCP = can connect to the Forge MCP Server to gain Forge knowledge, but Forge app building is not a native, first-class workflow on that platform.*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- All five platforms support MCP — any of them can connect to the Forge MCP Server for Forge-aware AI generation
- **App Studio (Rovo Studio)** — Forge-specific; describe the app, Rovo selects modules, generates UI Kit code, wires backend + permissions; open beta March 2026, auto-rolled out May 2026; agents built in under 20 minutes; governance built-in; mostly free for internal/single-site apps
- **Lovable** — $100M ARR in 8 months; full-stack apps with Supabase; one-click deployment; limitation: backend limited to Supabase; still requires user to configure auth and RLS policies
- **Bolt.new** — StackBlitz WebContainer; full cloud IDE (file tree, terminal, preview) with AI; token-based billing ($40–100/mo for serious use); some npm packages incompatible with browser sandbox
- **v0.dev** — Vercel's frontend-only tool; production-quality React/Tailwind components; no backend; best for Vercel/Next.js developers
- **The "Technical Cliff"** — vibe-coding tools produce a beautiful mockup that fails at production infrastructure; App Studio sidesteps this entirely — Forge is the production infrastructure, serverless, with auth and scaling handled

</details>

---

### MCP is the universal adapter for AI agents — one standard, any tool

**MCP (Model Context Protocol)** is an open standard created by Anthropic (November 2024) for connecting AI agents to external tools, data, and services. Think of it as a universal adapter — like USB-C, but for AI agents.

**The problem it solves:**

```
Before MCP:  10 AI apps × 100 tools = 1,000 custom integrations  ❌
After MCP:   implement client once + implement server once = ∞ works  ✅
```

**How it works:**

```
┌─────────────────────────────────────┐
│  AI Agent (Host)                    │
│  e.g. Rovo Dev, Claude Code, Cursor │
│              │                      │
│      ┌───────▼────────┐             │
│      │   MCP Client   │             │
│      └───────┬────────┘             │
└──────────────┼──────────────────────┘
               │  JSON-RPC 2.0
    ┌──────────┼──────────┐
    ▼          ▼          ▼
┌────────┐ ┌────────┐ ┌────────┐
│ Forge  │ │Atlasn. │ │ GitHub │
│  MCP   │ │  MCP   │ │  MCP   │
└────────┘ └────────┘ └────────┘
```

MCP servers expose three primitives: **Tools** (actions to execute), **Resources** (data to read), **Prompts** (reusable instructions).

<details>
<summary>Illustration</summary>

**Title:** MCP — One Standard, Any Tool

A two-panel "before and after" comparison:

**Before MCP (left panel — messy, red tones):**
A tangled web of lines connecting 4 AI apps (Claude, Cursor, Rovo Dev, ChatGPT) to 5 tools (Jira, GitHub, Forge, Slack, Postgres). Every app has its own custom line to every tool — 20 crossing lines total, visually chaotic. Label: "N×M custom integrations".

**After MCP (right panel — clean, blue/green tones):**
The same 4 AI apps on the left, each connecting to a single central vertical bar labeled "MCP". The same 5 tools on the right, each connecting to the same bar. Clean parallel lines, no crossing. Label: "N+M standard connections".

Below the two panels, a row of three icons labeled **Tools**, **Resources**, **Prompts** — the three MCP primitives — each with a one-line description.

Style: split-panel layout, high contrast between the messy left and clean right, Atlassian brand colours.

</details>

#### Speaker notes

<details>
<summary>Speaker notes</summary>

MCP was created at Anthropic by David Soria Parra and Justin Spahr-Summers and released November 25, 2024. In December 2025, Anthropic donated it to the Linux Foundation under the Agentic AI Foundation (co-founded by Anthropic, Block, and OpenAI). OpenAI officially adopted MCP in March 2025 and integrated it across ChatGPT desktop. By February 2025, over 1,000 community-built MCP servers existed. Today there are thousands.

The USB-C analogy: before USB-C, every device had a different cable. Before MCP, every AI integration was custom-built. MCP is the standard connector.

**Architecture:**
- **Host** — the AI application the user runs (Claude Desktop, Cursor, Rovo Dev). Owns the session, manages permissions, enforces what the agent is allowed to do.
- **Client** — lives inside the host. Each client holds exactly one connection to one MCP server.
- **Server** — implements the protocol. Exposes tools, resources, and prompts. Can run locally (subprocess via STDIO) or remotely (HTTP).

**Three primitives:**
- **Tools** (model-controlled) — executable functions. Parameters defined in JSON Schema. Agent decides when to call them. Examples: create a Jira issue, search Confluence, deploy to Forge.
- **Resources** (application-controlled) — read-only data the agent can reference. Examples: Forge documentation, codebase files, API references.
- **Prompts** (user-controlled) — reusable instruction templates. The server defines them once; clients can invoke them.

**Communication:** JSON-RPC 2.0. Transport: STDIO for local servers, Streamable HTTP for remote servers.

**Security:** The host controls what tools the agent can call. Sensitive actions prompt the user for approval. The Atlassian MCP Server uses OAuth 2.1 and respects existing Atlassian permissions.

</details>

---

### Two types of MCP servers power Forge development: app-building tools and project-context tools

MCP servers extend what your AI agent can do. For Forge development, the relevant servers fall into two groups:

**🔨 App development** — tools that help the agent *build* the app:

| MCP Server | Provider | Key Capabilities |
|---|---|---|
| 🔶 **Forge MCP Server** | Atlassian | Forge how-to guides, module catalogs, manifest guidance, API search — Forge knowledge for any AI agent |
| 🐙 **GitHub MCP Server** | GitHub | Repository management, PR creation, issue tracking, code review |
| 📁 **Filesystem MCP** | Anthropic | Local file read/write for agents in sandboxed environments |
| 🌐 **Playwright MCP** | Microsoft | Browser automation, web scraping, UI testing |
| 🐘 **Postgres MCP** | Community | Natural language queries against PostgreSQL — useful for debugging |

**📋 Project context** — tools that help the agent *understand what to build and track progress*:

| MCP Server | Provider | Key Capabilities |
|---|---|---|
| 🔷 **Atlassian MCP Server** | Atlassian | Jira, Confluence, Bitbucket, Compass read/write — reads requirements, updates issue status, links PRs |
| 💬 **Slack MCP** | Community | Read channel discussions for context; post progress updates |

---

### Add the Forge MCP Server in one config block — zero installation required

The Forge MCP Server is a remote server — no local install, no dependencies. Just add one entry to your agent's MCP config file and restart.

```json
{
  "mcpServers": {
    "forge": {
      "url": "https://mcp.atlassian.com/v1/forge/mcp",
      "transport": "http"
    }
  }
}
```

**Config file locations by tool:**

| Tool | Config file location |
|---|---|
| **Claude Desktop** | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| **Cursor** | `~/.cursor/mcp.json` |
| **Windsurf** | `~/.codeium/windsurf/mcp_config.json` |
| **VS Code** | `settings.json` → `mcp.servers` key |
| **Rovo Dev** | `acli rovodev mcp` (opens config in default editor) |

> ⚠️ JSON doesn't allow trailing commas. Validate with `jsonlint.com`. Always fully restart the app (not just the window) after config changes.

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- This is the most actionable slide in the deck — audience members can do this in the next 10 minutes
- The Forge MCP Server is remote — unlike most MCP servers there is nothing to install locally; the URL is the server
- Common gotcha: people reload the window but the MCP client doesn't reconnect until the full app is restarted
- Second common gotcha: trailing comma in JSON causes silent failure — the MCP server simply doesn't appear
- Rovo Dev users: use `acli rovodev mcp` which opens the config in your default editor — no need to find the file path manually
- After adding: ask the agent "What Forge modules are available for Jira?" — if it returns a structured list from developer.atlassian.com, the server is connected

- **Forge MCP Server** — GA February 2026; remote server, no local install; just add the URL to your MCP config
- What it provides: how-to guides, module catalogs, manifest guidance, Forge doc search, agent-friendly structured responses
- Workflow: `forge-development-guide` → `forge-ui-kit-developer-guide` / `forge-modules-list` / `forge-app-manifest-guide` → `search-forge-docs` → correct Forge code
- Limitation: publicly available info only, no auth required; may become stale if knowledge index not refreshed
- **Atlassian MCP Server** — GA February 2026 (Claude first); expanded April 2026 to include Bitbucket; supports Jira, Confluence, Compass, Bitbucket read/write; 20+ supported AI clients; OAuth 2.1 + respects existing permissions
- **Config file locations:** Claude Desktop `~/Library/Application Support/Claude/claude_desktop_config.json` · Cursor `~/.cursor/mcp.json` · Windsurf `~/.codeium/windsurf/mcp_config.json` · VS Code `settings.json` (`mcp.servers` key)
- Common gotcha: JSON doesn't allow trailing commas; fully restart the app (not just the window) after config changes

</details>

---

### Agent skills are reusable instruction sets — they teach AI your team's specific way of working

**Agent Skills** are reusable packages of instructions, scripts, and resources that teach an AI agent how to perform specific tasks consistently — like giving a new team member a standard operating procedure that they can refer to whenever they need it.

**How skills work — Progressive Disclosure:**
1. **Discover** (~100 tokens) — agent sees skill name + description at startup
2. **Activate** — agent loads full SKILL.md when the task matches
3. **Execute** — agent follows instructions, loads referenced files as needed

<details>
<summary>Illustration</summary>

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

</details>

**Examples of useful skills for Forge development:**
- 📋 **Forge App Builder** — module selection, manifest setup, UI Kit patterns, deploy workflow
- 📋 **Forge App Review** — pre-deploy checklist: security, cost efficiency, performance
- 📋 **Commit** — commit message format, what to stage, PR structure
- 📋 **Changelog** — how to record changes in your project's specific format

> *Agent Skills are an open standard (agentskills.io, Apache 2.0), supported by Rovo Dev, Claude Code, GitHub Copilot, and Codex CLI.*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

Agent Skills are a concept formalised as an open standard at agentskills.io (Apache 2.0 licence), now supported by GitHub Copilot, Claude Code, OpenAI Codex, and Rovo Dev.

The best analogy: if an MCP server is like giving the agent a phone to call external services, a skill is like giving the agent your team's runbook — the specific way your team does things.

**Progressive disclosure** is efficient: skills don't load their full content into every prompt. Only ~100 tokens per skill at startup (name + description), then the full instructions load only when the task matches. This means you can have many skills without burning tokens unnecessarily.

The open standard means: build a skill once, use it across Claude Code, Codex CLI, GitHub Copilot, and Rovo Dev — without modification.

The Forge App Builder and Forge App Review skills are particularly valuable because they encode:
- Which Forge module to use for which UI surface (jira:issuePanel, confluence:macro, etc.)
- The correct manifest structure and required scopes for common API calls
- UI Kit component patterns and best practices
- Pre-deployment checks — security, cost, performance — so the agent doesn't miss anything before shipping

This is institutional knowledge about Forge that would otherwise live in a developer's head, re-explained every session. With a skill, it's encoded once and reused forever.

</details>

---

### `atlassian/forge-skills` is Atlassian's official skill bundle — scaffold, review, debug, and connect in one install

The Forge Skills Plugin bundles several Forge-focused skills plus MCP-backed tooling so your agent can scaffold apps, review them before deploy, debug production issues, and stay current on Forge APIs and the Atlassian Design System.

**Included skills:**

| Skill | What it does |
|---|---|
| 📋 **Forge App Builder** | Scaffolds Forge apps — module selection, manifest setup, UI Kit patterns, deploy workflow |
| 📋 **Forge App Review** | Pre-deploy checklist: security, cost efficiency, performance, architectural patterns |
| 📋 **Forge Debugger** | Traces production issues — blank panels, failed deploys, API errors |
| 📋 **Forge Connector** | Guides building `graph:connector` apps that ingest external data into Atlassian's Teamwork Graph, making it searchable in Rovo Search and surfaced in Rovo Chat. |

**MCP tooling included:**
- Gives your agent access to up-to-date Forge documentation, template registries, module configuration, manifest syntax, and UI Kit/backend API guides — so its knowledge stays current rather than relying on training data.
- Provides Atlassian Design System lookup for Custom UI apps: component discovery, token reference, and icon search via the @atlaskit library.

```bash
# Install via the Skills CLI
npx skills add atlassian/forge-skills

# For Rovo Dev (manual steps — plugin install not yet supported):
# acli rovodev mcp   (add .mcp.json entries, then restart Rovo Dev)
```

> 🔗 `github.com/atlassian/forge-skills` — works with Rovo Dev, Claude Code, Cursor, GitHub Copilot, and Codex CLI

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- This is the official Atlassian-published skill bundle — not a community project; maintained by Atlassian
- It's the fastest way to get a fully configured Forge development environment for any AI agent
- **Four skills in one install:** Builder (scaffold), Review (pre-deploy QA), Debugger (production tracing), Connector (Rovo Search integration)
- **MCP tooling bundled:** the installer also wires up the Forge MCP Server and the Atlassian Design System MCP — so you get live, up-to-date Forge docs and ADS component lookup in one step
- Rovo Dev doesn't currently support plugin installations but you can install the skills and MCP servers separately. The README explains how to do this step by step
- **Quick-check prompts after install:** "What Forge modules are available for Jira?" (tests Forge MCP) · "Review my Forge app for security issues before I deploy." (tests Forge App Review skill) · "My Forge issue panel is blank after deploy — help me trace it." (tests Forge Debugger)
- The **Forge Connector skill** is worth calling out separately: it's for teams that want to surface external data (e.g. a project management tool, a support system) inside Rovo Search and Rovo Chat — a powerful use case that goes beyond app-building

</details>

---

### `npx skills` is the package manager for agent skills — install once, update manually to stay current

`npx skills` (by Vercel Labs) is the npm equivalent for agent skills — it uses GitHub as its registry. Any public GitHub repo with a `SKILL.md` at the root is a valid skill source.

**What happens when you run `npx skills add atlassian/forge-skills`:**

```
1. Downloads the atlassian/forge-skills GitHub repo
2. Detects which agents are installed on your machine
3. Copies the SKILL.md files into each agent's skills directory:
   - Universal:  .agents/skills/         (Rovo Dev, Codex, Copilot, Cursor…)
   - Claude Code: .claude/skills/
   - Antigravity: .agent/skills/
4. Creates a skills-lock.json for reproducibility
```

**⚠️ Skills are a snapshot — they do not auto-update:**

| Need | Command |
|---|---|
| Check what updates are available | `npx skills check` |
| Update all installed skills | `npx skills update` |
| Update one skill | `npx skills update forge-skills` |

**Auto-update on every session start** (Claude Code):
```json
// ~/.claude/settings.json
{ "hooks": { "SessionStart": [{ "type": "command",
  "command": "npx skills update -g -y 2>/dev/null" }] } }
```
> Runs before context loads — zero token cost. Each session starts with current skills.

**Team consistency** — commit `skills-lock.json` and restore with `npx skills experimental_install` in CI.

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- The key mental model: `npx skills` is to agent skills what `npm` is to JavaScript packages — same concepts of install, update, lock file, and registry
- GitHub is the registry — `atlassian/forge-skills` maps directly to `github.com/atlassian/forge-skills`; any public repo with a SKILL.md is installable
- **Skills are static files on disk** — unlike MCP servers (which are always live), skills are a snapshot; if Atlassian updates the Forge App Review skill with new checks, you won't get those improvements until you run `npx skills update`
- The `skills-lock.json` file pins exact versions — commit it to your repo and teammates get identical skills via `npx skills experimental_install`; useful in CI too
- The `SessionStart` hook is the most practical approach for individuals: skills update silently before each session, zero friction, zero tokens
- `npx skills` supports 51+ agents — the universal `.agents/skills/` location works for most; agent-specific paths (`.claude/skills/`, etc.) are also handled automatically
- This is worth calling out because it's a common source of confusion: "why is the agent giving me outdated Forge module advice?" — answer: your skills are stale, run `npx skills update`

</details>

---

### MCP servers give agents live capabilities; skills give agents your team's static expertise

Skills and MCP Servers are complementary — not alternatives. Together they give an agent both the *tools* to act and the *knowledge* of how to act correctly.

| | MCP Server | Agent Skill |
|---|---|---|
| **What it is** | A tool / API connector | A reusable instruction set |
| **Provides** | Live data and capabilities | Static data and workflow instructions |
| **Format** | Running server process | Markdown file (SKILL.md) |
| **Best for** | Accessing live external systems | Encoding repeatable workflows |
| **Token cost** | Higher (live connections) | Lower (loaded on demand only) |

**They work together:**
```
Forge App Builder SKILL
  └── instructs the agent to consult the Forge MCP Server
        └── which provides up-to-date module catalogs & manifest guidance
              └── agent generates correct, current Forge code
```

> *MCP Servers give the agent its tools. Skills give the agent its expertise.*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

This distinction is important and worth dwelling on, because developers often wonder "should I use an MCP server or a skill?"

The answer is almost always: both, for different reasons.

**MCP gives the agent *capabilities*:**
- Access to Jira (read issues, update status)
- Access to Forge documentation (current module types, manifest syntax, API scopes)
- Ability to run terminal commands
- Ability to browse the web

**Skills give the agent *knowledge*:**
- Your commit message format
- Your pre-deploy checklist
- Your team's preferred Forge module patterns
- Your architectural standards and coding conventions

They complement each other beautifully. A Forge App Builder skill uses the Forge MCP Server under the hood:
1. The skill instructs the agent: "When building a Forge app, first consult the Forge MCP Server for current module recommendations"
2. The Forge MCP Server provides up-to-date docs (capability)
3. The skill then tells the agent what patterns your team prefers (knowledge)
4. Result: code that is both technically correct AND aligned with your team's standards

Without the MCP Server, the skill's instructions to "check current Forge docs" would produce hallucinated answers. Without the skill, the MCP Server would give generic Forge guidance without your team's specific preferences. Together they produce consistently excellent output.

**Token cost note:** Skills are much cheaper than MCP servers for encoding static knowledge. If the information doesn't change often (commit message format, Forge module patterns), use a skill. If the information changes frequently or requires live data (current Jira issue status, latest Forge API scopes), use an MCP server.

</details>

---

### MCP and skill invocation is discretionary — the agent decides whether to use them

Configuring an MCP server or a skill does not guarantee the agent will use it. The agent makes its own judgement call at inference time: if it believes its training data is sufficient to answer, it may skip the tool call entirely — silently producing stale or hallucinated output while appearing confident.

**Why this happens:**

```
Developer asks: "What Forge module should I use for a Jira issue panel?"

Agent (without explicit instruction):
  Option A → call Forge MCP Server → get current answer  ✅
  Option B → answer from training data → may be outdated  ⚠️

The agent chooses Option B if it believes it already knows.
```

**The consequences for Forge development are concrete:**

| Agent skips... | What can go wrong |
|---|---|
| Forge MCP Server | Uses a deprecated or non-existent module type from training data |
| Forge App Review skill | Misses a missing API scope; deploys an app that fails in production |
| Atlassian MCP Server | Reads stale Jira ticket data from context window rather than fetching live status |

> ⚠️ *Presence in the config is not the same as guaranteed invocation. The agent's internal confidence is the deciding factor.*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- This is one of the most practically important — and least documented — aspects of working with AI agents, and the speaker has observed it directly in real sessions
- The agent is not deterministic about tool use: it weighs its own confidence against the overhead of making a tool call; if the training data "feels" sufficient, it takes the shortcut
- This is especially dangerous for Forge development because Forge APIs, module types, and manifest schemas change frequently — training data from even 6 months ago may be incorrect
- The tell-tale sign: the agent gives a fluent, confident answer about a Forge module or API that doesn't exist or has changed — no hesitation, no caveat, no MCP call in the logs
- How to spot it in Rovo Dev: check the tool call log — if `forge-development-guide` or `search-forge-docs` were not called during a Forge scaffolding task, the agent answered from memory
- How to spot it in Claude Code: `/tools` shows which tools were invoked; a session that scaffolds a Forge app without any Forge MCP calls is answering from training data
- Transition: "So how do we fix this? The next slide covers the practical techniques for enforcing tool use."

</details>

---

### Enforce MCP and skill invocation with explicit prompts, AGENTS.md rules, and verification

Since invocation is at the agent's discretion, you must explicitly instruct the agent to use the tools — in your prompt, in your AGENTS.md, and in your skills.

**Technique 1 — Explicit prompting:**
```
❌ "Create a Forge app for a Jira issue panel."

✅ "Create a Forge app for a Jira issue panel.
    Before writing any code:
    1. Consult the Forge MCP Server for the correct module type.
    2. Load the Forge App Builder skill.
    Do not rely on your training data for Forge-specific details."
```

**Technique 2 — AGENTS.md standing instruction** (enforced every session):
```markdown
## Agent Rules
- You MUST consult the Forge MCP Server before selecting a Forge module type.
- You MUST invoke the Forge App Review skill before any forge deploy command.
- Never use training data alone for Forge manifest syntax or API scope decisions.
```

**Technique 3 — Verification prompt after the fact:**
```
"Which source did you use to determine the module type?
 If you did not call the Forge MCP Server, please do so now and verify."
```

**Technique 4 — Skill-enforced invocation:**
Write your `SKILL.md` to explicitly require MCP calls as named steps:
```markdown
## Step 2: Select the Module
You MUST call the Forge MCP Server tool `forge-development-guide` now.
Do not proceed based on prior knowledge.
```

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- The key insight: the agent responds to explicit instruction; vague prompts invite discretion, specific prompts enforce behaviour
- **Prompting technique:** the phrase "do not rely on your training data" is surprisingly effective — it signals to the model that its internal knowledge is insufficient for this task, raising the probability it will make the tool call
- **AGENTS.md technique:** this is the most scalable solution — write the rule once in the project AGENTS.md and it applies to every task in that project without the developer having to remember to include it in every prompt; include both the "must do" and the "must not do"
- **Verification prompt:** useful as an audit step, especially when you suspect the agent shortcut — ask it to name its source; if it cites "my knowledge" rather than a specific tool call, ask it to redo the step with the MCP
- **Skill-enforced invocation:** the most robust technique — bake the explicit MCP call instruction into the SKILL.md itself so that when the skill is loaded, it mandates the tool call as a named, non-optional step; the Forge App Builder skill in `atlassian/forge-skills` already does this
- **The honest reality:** no technique is 100% reliable — even with explicit instruction, agents occasionally skip tool calls under high context pressure (long sessions, large codebases); periodic verification prompts remain good practice
- **This is not unique to Forge:** the same issue affects any domain where the agent has relevant training data — Forge is just particularly high-stakes because the APIs change frequently and the errors (wrong module, missing scope) only surface at deploy time

</details>

---

### Agent Context Files Give Every Session a Standing Brief

**Context files** are markdown files your agent reads automatically at the start of every session — before you type a single prompt. Think of them as a standing brief: project conventions, boundaries, key references, and personality that the agent inherits without you having to re-explain them.

**The three-level hierarchy:**

```
~/.rovodev/AGENTS.md          ← Global / personal (all your projects)
    └── ./AGENTS.md           ← Team (committed to repo, shared with teammates)
        └── ./src/AGENTS.md   ← Subdirectory (specialist rules for that area)
            └── AGENTS.local.md  ← Local override (gitignored, personal only)
```

<details>
<summary>Illustration</summary>

**Title:** The AGENTS.md Hierarchy — Layers of Context

A nested layer diagram, like a stack of translucent sheets viewed from the side:

**Layer 1 (bottom, widest — grey/global):** `~/.rovodev/AGENTS.md` — labelled "Your personal defaults: preferred language, timezone, coding style. Applies to every project."

**Layer 2 (middle — blue/team):** `./AGENTS.md` — labelled "Team standards: architecture, build commands, coding conventions. Committed to git — shared with all teammates."

**Layer 3 (narrower — teal/subdirectory):** `./src/AGENTS.md` — labelled "Specialist rules: only applied when working in this directory."

**Layer 4 (top, smallest — orange/local):** `AGENTS.local.md` — labelled "Personal overrides: gitignored, your machine only."

An arrow on the right side points downward labeled "Higher specificity wins". A lock icon on Layer 4 indicates gitignored.

Style: layered/stacked card metaphor, each layer a different colour, clean labels, Atlassian palette.

</details>

**Context files vs. Skills:**

| | Context file (AGENTS.md) | Agent Skill (SKILL.md) |
|---|---|---|
| **When loaded** | Always — every session | On demand — when task matches |
| **Purpose** | Project identity & standards | Repeatable task workflows |
| **Committed?** | Yes (except `.local`) | Yes |
| **Typical size** | < 200 lines | < 5,000 tokens |

**What to put in AGENTS.md:**
- Project overview and directory structure
- Build and test commands
- Coding standards *specific to this project* (not general language basics)
- Domain terminology and key references
- Agent boundaries and constraints

> *Including an AGENTS.md reduced agent task completion time by 28% in a controlled study (ETH Zurich, 2025).*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

Context files are the "always-on" layer of agent configuration — as opposed to skills, which are "on-demand". The difference matters:

- AGENTS.md is loaded at startup of every session. The agent always knows your project's name, structure, coding conventions, and what it's not allowed to do.
- Skills are loaded only when the task matches. The Forge App Builder skill only loads when you ask the agent to build a Forge app — not when you ask it to write a commit message.

**The three-level hierarchy in practice:**
1. `~/.rovodev/AGENTS.md` (or `~/.agent.md`, `~/.claude/CLAUDE.md`, `~/.codex/AGENTS.md`) — your personal defaults. Things like your preferred language, timezone, coding style preferences. Applies to every project you work on.
2. `./AGENTS.md` in the project root — team-wide conventions. Committed to git so every developer on the team benefits. Covers the project's architecture, build commands, coding standards specific to this codebase.
3. `./src/AGENTS.md` or `./services/api/AGENTS.md` — subdirectory specialists. Rules that only apply when the agent is working in that part of the codebase. Not all tools support this — Codex CLI, Claude Code, and Rovo Dev do; Cursor applies project-level rules everywhere.
4. `AGENTS.local.md` — personal overrides. Add to `.gitignore`. Lets you customise the agent's behaviour for your machine without polluting the shared team config.

**Tool-specific naming:**
- Rovo Dev: `AGENTS.md` and `AGENTS.local.md` (project); `~/.rovodev/AGENTS.md` (global)
- Claude Code: `CLAUDE.md` and `CLAUDE.local.md` (project); `~/.claude/CLAUDE.md` (global)
- Cursor: `.cursor/rules/*.mdc` (project); Settings > Rules for AI (global)
- GitHub Copilot: `AGENTS.md` or `.github/copilot-instructions.md` (project)
- Codex CLI: `AGENTS.md` with hierarchical discovery (global → project → subdirectory)
- Windsurf: `AGENTS.md` (always-on at root); `.windsurf/rules/` with trigger modes

**The portability play:**
`AGENTS.md` is recognised natively by Codex CLI, GitHub Copilot, Rovo Dev, Windsurf, and Cline. Claude Code uses `CLAUDE.md` but can reference `AGENTS.md`. Maintaining `AGENTS.md` as the source of truth and symlinking or referencing it from tool-specific files minimises duplication.

**Sizing guidance:**
- Under 200 lines is the recommended target (Anthropic official guidance)
- Over 500 lines and most of it is being ignored — LLMs have limited instruction-following capacity
- A focused 50-line file outperforms a sprawling 1,000-line one
- Human-curated files outperform LLM-generated ones (ETH Zurich found LLM-generated files *reduced* success rates by ~3% on average)

**For this project:**
The `AGENTS.md` in this repository defines the agent's personality (research assistant for Forge + AI development), scope (what topics are in/out), boundaries (never commit without explicit request), key references (Presentation.md, PresentationFormat.md), and skills location (`.agents/skills/`). It's the reason any agent that opens this project immediately knows what it's working on.

</details>

---

### Agents Read Your Codebase on Demand — They Don't Load It All at Once

AI agents don't read your entire codebase into memory when they start. They navigate the file system selectively — discovering structure, then reading only what's relevant to the current task.

**How agents access file content:**

```
Agent receives task
      │
      ▼
Lists directory structure (awareness of what exists)
      │
      ▼
Selectively opens files using tools (open_files, grep, search...)
      │
      ▼
Large files shown collapsed (signatures only) → expand on demand
      │
      ▼
Acts on relevant content only
```

**Scoping vs. loading — an important distinction:**

| | What it means |
|---|---|
| **Scoped to a directory** | The agent's sandbox — it can only read/write within this boundary |
| **Context window** | What the agent actually has in memory right now — much smaller |
| **Selective reading** | The agent decides which files to open based on the task |

**Best practices for large codebases:**
- 🎯 **Launch from the most specific relevant directory** — not the monorepo root
- 🚫 **Use `.rovoignore` / `.gitignore`** to exclude `node_modules/`, `build/`, `dist/` etc. — reduces context pollution
- 📁 **Use AGENTS.md to describe directory structure** — saves the agent from discovering it via tool calls

> *Every file the agent opens costs tokens. A well-scoped launch and a good `.rovoignore` directly improve quality and reduce cost.*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

This is one of the most practically important things to understand about working with AI coding agents — and it's counterintuitive for developers who are used to IDEs that index the entire project upfront.

**The key mental model:**
The agent's *working directory* defines what it's allowed to touch. But that's not the same as what it has read. The agent starts with awareness of the directory tree (like doing `ls -la` and `find .`) and then selectively opens files when it needs to understand them.

For Rovo Dev specifically:
- Files are opened on demand via tool calls: `open_files`, `grep`, `expand_code_chunks`, `expand_folder`
- Large files are shown in a collapsed view (just function signatures and class definitions) — the agent has to explicitly expand sections it needs to read
- This is a deliberate design choice: collapsed views give structural awareness without burning tokens on every line

**Analogous behaviour in other agents:**
- Claude Code: uses `read_file`, `list_files`, `search_files` tool calls similarly
- Cursor / Windsurf: index the codebase for semantic search, but still read files on demand during agent tasks
- Codex CLI: similar file tool architecture — reads selectively based on task needs

**The launch directory matters:**
If you run an agent from `/monorepo-root/` it will need to navigate a potentially enormous tree to find the 3 files it actually needs. If you run it from `/monorepo-root/services/payments/` it starts immediately oriented to the relevant code. Rovo Dev specifically supports `acli rovodev --dir <path>` to set the working directory without changing your shell's current directory.

**`.rovoignore` and context hygiene:**
Just like `.gitignore` tells git what to skip, `.rovoignore` tells Rovo Dev what to exclude from its view. Common candidates:
- `node_modules/` — almost never relevant
- `build/`, `dist/`, `.next/`, `target/` — generated output
- Large data files, fixtures, or binary assets
- Third-party vendor directories

Other agents have equivalents: Claude Code respects `.gitignore` automatically and also reads `.claudeignore`; Cursor has its own ignore configuration.

**The token economics:**
Every `open_files` call, every `grep` result, every expanded code chunk costs input tokens. A well-scoped launch + good ignore file means the agent spends its token budget on the actual problem rather than navigating irrelevant structure. This directly translates to:
- Better quality responses (more context window available for the task)
- Lower cost per session
- Faster task completion (fewer navigation steps)

**What to put in AGENTS.md to help:**
A brief directory structure map in AGENTS.md means the agent doesn't have to discover it via tool calls:
```markdown
## Directory Structure
- `src/` — application source code
- `src/components/` — React UI components
- `src/resolvers/` — Forge resolver functions
- `static/` — frontend assets
- `test/` — Jest test suites
```
This alone can save 3–5 tool calls at the start of every session.

</details>

---

### A skill is just a SKILL.md file — version-controlled, portable, and team-shareable

Skills are simple markdown files stored in your project repository. Agents discover and load them automatically.

**Skill file structure** (using the canonical `.agents/skills/` location):
```
.agents/skills/
├── commit/
│   └── SKILL.md
├── changelog/
│   └── SKILL.md
└── forge-app-builder/
    ├── SKILL.md
    └── references/
        └── module-patterns.md
```

**A SKILL.md file looks like this:**
```markdown
---
name: forge-app-builder
description: Guides scaffolding a new Forge app from prompt
  to production-ready: module selection, manifest setup,
  UI Kit patterns, deploy, and install.
---

# Forge App Builder

## Step 1: Understand the Requirements
Ask the developer what Atlassian product the app targets...

## Step 2: Select the Right Module
Consult the Forge MCP Server for module recommendations...
```

**Benefits of skills:**
- ✅ **Version controlled** — improve them like code, review changes in PRs
- ✅ **Portable** — work across Claude Code, Codex, Copilot, Rovo Dev
- ✅ **Team-shareable** — check into your repo; every developer benefits
- ✅ **Lightweight** — loaded on demand, not burning tokens every session

#### Speaker notes

<details>
<summary>Speaker notes</summary>

The beauty of skills is their simplicity. A skill is just a markdown file in a directory. No servers to run, no APIs to configure, no deployment pipeline.

**Creating a skill:** In Claude Code you can type `/create-skill` and describe what you want. The agent asks clarifying questions and generates the SKILL.md with directory structure, instructions, and frontmatter automatically. Or just create the file yourself — it's markdown.

**The frontmatter matters:**
- `name` — short identifier (used in logs and references)
- `description` — THIS is what the agent reads at startup to decide if the skill is relevant. Write it carefully. Describe *when* to use this skill, not just *what* it is. The agent decides whether to load the full skill based only on this description.

**Recommended structure inside SKILL.md:**
- Overview — what this skill does
- When to use — explicit triggers
- Step-by-step instructions — the actual workflow
- References to external docs or files in `references/`

**Real example from this project:** This very presentation was built with an agent using a `research` skill (for conducting research), a `changelog` skill (for recording version changes), and a `commit` skill (for formatting commits). The agent reads these skills from `.agents/skills/` and applies them automatically when the task calls for it.

**Keep SKILL.md under 5,000 tokens** — the "load" step should be lean. Put long reference documents in a `references/` subfolder, loaded only when the agent explicitly needs them.

</details>

---

### Use .agents/skills/ in your repo — it's the standard location recognised by most agents natively

The SKILL.md format is a shared open standard — but each tool looks for skills in its own directory. The standard recommends `.agents/skills/` in your project root, checked into git and shared with the team.

**Project-level skills** (checked into your repo — shareable with the team):

| Tool | Project skills directory |
|---|---|
| **Codex CLI** | `.agents/skills/` ✅ standard |
| **GitHub Copilot** | `.agents/skills/`, `.github/skills/`, or `.claude/skills/` |
| **Rovo Dev** | `.agents/skills/` or `.rovodev/skills/` |
| **Claude Code** | `.claude/skills/` |
| **Cursor** | `.cursor/skills/` |
| **Windsurf** | `.windsurf/skills/` |

> 💡 **Recommended:** Put your team skills in `.agents/skills/` and symlink agent-specific directories to it — one source of truth, all agents see it. `npx skills add` handles this automatically.

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- Project-level skills live inside your repository, committed to git — when a teammate pulls, they immediately have all team skills
- `.agents/skills/` is the open standard path (agentskills.io). Rovo Dev, Codex CLI, and GitHub Copilot all recognise it natively
- Irony worth mentioning: Anthropic created both the Agent Skills open standard *and* Claude Code — yet Claude Code uses `.claude/skills/` instead of the standard it defined; this has caused community friction
- Symlink trick: `ln -s .agents/skills .claude/skills` — one source of truth for all agents
- `npx skills add` handles directory detection automatically — detects which agents are installed and places files in the right locations; lowest-friction path for teams getting started

</details>

---

### Global skills stay with you across every project — but Cursor is the exception

Personal skills live in your home directory and are available in all your projects on that machine — ideal for preferences that follow you everywhere.

**Global / personal skills** (available across all your projects):

| Tool | Global / personal skills directory |
|---|---|
| **Codex CLI** | `~/.codex/skills/` |
| **GitHub Copilot** | `~/.agents/skills/` or `~/.copilot/skills/` |
| **Rovo Dev** | `~/.agents/skills/` or `~/.rovodev/skills/` |
| **Claude Code** | `~/.claude/skills/` |
| **Windsurf** | `~/.codeium/windsurf/skills/` |
| **Cursor** | ❌ No global skills support |

**Good candidates for global personal skills:**
- Your preferred commit message format and PR conventions
- Your coding style preferences (language, indentation, naming)
- A "daily standup" skill that summarises your recent git activity

> ⚠️ **Cursor limitation:** Cursor is the only major agent with no global skills support. Personal skills must be copied into each project's `.cursor/skills/` manually — or use a setup script.

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- Global skills are personal — not committed to the repo, not shared with teammates; they follow the developer across all projects on their machine
- Project skills take precedence over global skills when names conflict
- Cursor's lack of global skills support is a genuine friction point — if your team uses Cursor alongside other agents, this is worth calling out so people aren't surprised
- `npx skills add -g` installs globally (user-level) rather than project-level; `npx skills add` without `-g` is project-scoped by default
- A useful pattern: global skill for personal style preferences + project skill for team Forge standards — layer them for maximum coverage

</details>

---

### Forge's constrained, declarative architecture makes it the ideal target for AI-assisted development

**Forge** is Atlassian's serverless app development platform — the foundation for building custom apps inside Jira, Confluence, and other Atlassian products. It is uniquely well-suited for AI-assisted development.

**Why Forge and AI are a natural fit:**

| Forge characteristic | Why AI agents love it |
|---|---|
| **Declarative manifest** | AI excels at generating correct declarative configuration |
| **Constrained module system** | Bounded problem space — fewer hallucinations, more reliable output |
| **Built-in auth + hosting** | Agent doesn't need to reason about infrastructure security |
| **Well-documented APIs** | Forge MCP Server feeds current docs directly to the agent |
| **JavaScript / React** | Languages LLMs understand exceptionally well |
| **Fast CLI feedback loop** | `forge tunnel` gives instant test results for agents to iterate on |

**Forge pricing (2026):**
- Most apps stay within the **generous free monthly allowance** — no cost
- Consumption-based charges only beyond the free tier — transparent billing
- Sandbox usage (first 5 sandboxes per production site) is **free** as of April 2026

#### Speaker notes

<details>
<summary>Speaker notes</summary>

Forge was launched in 2019 and has matured significantly. It's production infrastructure that thousands of apps run on — not an experiment.

Key Forge features:
- **Serverless FaaS** — Atlassian provisions, manages, monitors, and scales everything. No servers for developers to worry about.
- **Secure by default** — runs inside a second security layer enforcing tenant isolation and data egress restriction by design
- **Built-in auth** — platform handles authentication and identity automatically
- **Data residency** — data can be kept in the customer's region for compliance requirements
- **UI Kit + Custom UI** — UI Kit for React-based UIs with Atlassian Design System, Custom UI for full control. The new Frame component (recent) allows mixing both in the same app.

**Why the constrained problem space matters for AI:**
An open-ended infrastructure setup has millions of possible valid configurations — AI agents can go off in any direction. A Forge app has a fixed set of module types, known API scopes, a defined manifest format, and specific UI Kit components. The agent's search space is bounded. This means:
- Fewer hallucinations (the agent can't invent non-existent modules)
- More reliable output (correct manifest structure is well-documented)
- Faster iteration (fewer wrong turns)

**Pricing context:** The official Forge documentation states: "The vast majority of private apps developed by customers for use in a single site — even written naively without special regard for cost — will never exceed [the free allowance]." This removes a significant barrier to experimentation and AI-assisted development.

The April 2026 sandbox exemption is developer-friendly: usage from customers testing your app in up to 5 sandboxes per production site is now completely free, making it easier to let customers trial your app.

</details>

---

### Choose App Studio for a simpler setup

There are two AI-assisted paths to building a Forge app — choose based on technical comfort and the complexity of what you're building:

```
╔══════════════════════════════╗    ╔══════════════════════════════╗
║   PATH 1: NO-CODE            ║    ║   PATH 2: AI-ASSISTED        ║
║   Atlassian App Studio       ║    ║   PRO-CODE                   ║
║   (Rovo Studio)              ║    ║   Rovo Dev + Forge MCP       ║
╠══════════════════════════════╣    ╠══════════════════════════════╣
║ • Describe in plain English  ║    ║ • Use any AI agent:          ║
║ • Rovo designs + builds app  ║    ║   Rovo Dev, Claude Code,     ║
║ • No CLI, no code required   ║    ║   Cursor, Windsurf           ║
║ • Auto-deployed on Forge     ║    ║ • Forge MCP provides         ║
║ • Ready in < 20 minutes      ║    ║   domain knowledge           ║
║                              ║    ║ • Full control of code       ║
╠══════════════════════════════╣    ╠══════════════════════════════╣
║ Best for:                    ║    ║ Best for:                    ║
║ Admins, business users,      ║    ║ Developers building complex  ║
║ simple agents & workflows    ║    ║ integrations, custom logic   ║
╚══════════════════════════════╝    ╚══════════════════════════════╝
```

#### Speaker notes

<details>
<summary>Speaker notes</summary>

This is the core practical takeaway — two very different entry points, both powered by AI, suiting different personas.

**Path 1: Atlassian App Studio (Rovo Studio)**
Open beta March 2026, automatically rolled out from May 2026.

The workflow: you describe what you want ("Build a Jira panel that shows related Confluence pages"). Rovo:
1. Generates a feature spec outlining what the app does, where it lives, how it behaves
2. Selects the right Forge modules (e.g., `jira:issuePanel`, `confluence:macro`)
3. Generates UI with Forge UI Kit
4. Wires backend functions, storage, and permissions
5. Deploys automatically

Quote from a developer using Rovo Studio: "I started with a single, high-level requirement: 'Develop a curated list of team-bonding activities and format the output into a new Confluence page including all logistics and event details.' The Studio instantly understood the intent and populated the entire Agent Overview."

Governance is built in: org policies, roles, per-agent permissions, approvals, versioning, audit logs, monitoring. Enterprise-grade from day one.

**Path 2: AI-Assisted Pro-Code**
Use Rovo Dev CLI (or Claude Code, Cursor, Windsurf) with the Forge MCP Server connected.

The workflow:
1. Agent calls Forge MCP to understand which module to use and what scopes are needed
2. Agent scaffolds the app with `forge create`
3. Agent writes component code using UI Kit patterns from Forge MCP
4. `forge tunnel` provides real-time error feedback — agent reads and fixes
5. Forge App Review skill checks security, cost efficiency, performance before deploy
6. `forge deploy` and `forge install`

Key moment: "When I added Jira API calls, the agent automatically updated the manifest with the required scopes." This is the killer feature — the AI knows the Forge permission model and applies it correctly without being asked.

</details>

---

### The Forge MCP Server and Atlassian MCP Server open Atlassian data to any AI tool

Atlassian has built an open ecosystem — use whatever AI tool you want, and connect it securely to Forge and Atlassian data:

**Forge MCP Server** *(GA February 2026)*
Provides AI agents with deep Forge knowledge — how-to guides, module catalogs, manifest guidance, API search. Sourced from developer.atlassian.com. No authentication required. Any developer with any AI tool can use it.

**Atlassian MCP Server** *(GA February 2026, expanded April 2026)*
Connects any AI tool to Jira, Confluence, Bitbucket, and Compass with enterprise security. OAuth 2.1, full permission inheritance, admin whitelisting. Supported by 20+ AI clients including Claude, ChatGPT, Cursor, VS Code, Devin, GitHub, and more.

> *"Over a million people use AI on the Atlassian platform each month."*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- The strategic insight: Atlassian isn't forcing everyone onto Rovo Dev — they say "use whatever AI tool you want, we'll connect it to your Atlassian data securely." This is an ecosystem play that benefits Atlassian customers regardless of which agent they prefer
- Forge MCP Server: no auth required, zero install, sourced from developer.atlassian.com — any agent can use it immediately
- Atlassian MCP Server security model: OAuth 2.1, respects existing Jira/Confluence permissions (agent only sees what the authenticated user can see), admin whitelisting of allowed MCP clients, TLS 1.2+
- Bitbucket support added April 2026: AI clients can now browse repos, create commits, open PRs, and check pipeline results — closes the loop on the full development lifecycle
- Supported clients: AWS, ChatGPT, Claude, Cursor, Devin, Docker, Figma, GitHub, Google, Lovable, Mistral, Postman, Resolve, VS Code, WRITER, and more
- The 1 million monthly AI users figure: this is at production scale, not a prototype

</details>

---

### Reduce AI hallucinations with MCP, skills, and the human-in-the-loop

The three most common failure modes — and how to prevent them:

| Failure mode | Cause | Prevention |
|---|---|---|
| **Wrong Forge module** | Agent relies on stale training data | Forge MCP Server provides current module catalog |
| **Missing manifest scope** | Agent guesses at required permissions | Forge App Review skill checks scopes before deploy |
| **Incorrect UI Kit component** | Agent uses deprecated or non-existent component | ADS MCP Server provides live component lookup |

**The human-in-the-loop is your safety net:**
- Review agent-generated code before deploying — especially manifest changes
- Use `forge tunnel` to test before `forge deploy`
- The Forge App Review skill runs a pre-deploy checklist automatically

> *"The goal is not to trust AI blindly — it's to configure it so well that trust is well-placed."*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- Acknowledge the scepticism in the room — yes, AI agents make mistakes; this slide is for the people who are thinking "but what about reliability?"
- The solution is not to avoid agents — it is to configure them correctly (MCP + skills), keep yourself in the loop at key decision points, and use the built-in safety nets
- Error rates drop dramatically when agents have current, domain-specific context: the Forge MCP Server eliminates whole categories of hallucination by providing live, accurate module and manifest data
- The manifest scope issue is a great real-world example: without the Forge App Review skill, agents routinely forget to add required API scopes; with it, they catch this automatically before deploy
- "Human-in-the-loop" doesn't mean reviewing every line — it means being present at the right decision points: approving the plan, reviewing before deploy, checking the result

</details>

---

### Atlassian's internal AI tools show the depth of investment — and what's coming next

Beyond the public MCP servers, Atlassian has built a deep internal AI development stack:

**Atlassian App Studio / Rovo Studio** *(Open Beta March 2026)*
No-code Forge app builder. Describe your app in natural language — Rovo selects modules, generates UI Kit code, wires backend + permissions. Production Forge app in under 20 minutes. Enterprise governance built-in: org policies, roles, approvals, versioning, audit logs.

**Volt Studio** *(Internal)*
An internal Atlassian tool for building apps and automations at scale. Demonstrates that Atlassian uses AI-assisted development tooling internally — not just for customers.

**Socrates** *(Internal)*
Atlassian's internal MCP server for data and analytics capabilities, used internally for data-driven decision making with AI assistance.

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- App Studio is the most important product on this slide for the audience — it's the zero-code path to a deployed Forge app in under 20 minutes; worth a live demo if time allows
- The governance story is compelling for enterprise: org policies, per-agent permissions, approvals, versioning, audit logs — this is enterprise-grade from day one, not bolted on later
- Volt Studio and Socrates have limited public documentation; they signal that Atlassian is eating its own dog food — the same AI development patterns being recommended to customers are used internally at Atlassian
- Transition to next slide: "All of these tools — agents, MCP servers, skills, App Studio — come together into a single coherent developer workflow. Let's see what that looks like end to end."

</details>

---

### Agent + MCP Servers + Skills + Forge CLI = a complete AI-driven Forge development workflow

A recommended stack for building Forge apps with AI assistance in 2026:

```
┌─────────────────────────────────────────────────────────────────┐
│               YOUR AI FORGE DEVELOPMENT ENVIRONMENT            │
│                                                                 │
│  AI AGENT                                                       │
│  Rovo Dev CLI  /  Claude Code  /  Cursor  /  Windsurf           │
│                        │                                        │
│    ┌───────────────────┼───────────────────────────┐            │
│    │         MCP SERVERS (extend agent capabilities)│            │
│    │  🔶 Forge MCP    ─ Forge knowledge & docs      │            │
│    │  🔷 Atlassian MCP ─ Jira, Confluence, Bitbucket│            │
│    │  + Other MCP Servers if necessary               │            │
│    └────────────────────────────────────────────────┘           │
│                                                                 │
│    ┌────────────────────────────────────────────────┐           │
│    │      AGENT SKILLS (encode team knowledge)      │           │
│    │  📋 Forge App Builder   📋 Forge App Review     │           │
│    │  📋 Commit              📋 Changelog            │           │
│    └────────────────────────────────────────────────┘           │
│                                                                 │
│  FORGE CLI: forge tunnel → agent iterates → forge deploy        │
└─────────────────────────────────────────────────────────────────┘
```

**The result:** An AI agent that can scaffold, build, review, and deploy a complete Forge app — with your Atlassian context, Forge domain knowledge, and team workflow standards all baked in.

<details>
<summary>Illustration</summary>

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

</details>

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- This is the synthesis slide — show how all pieces click together into one practical workflow
- **Configure once:** Forge MCP + Atlassian MCP in agent config; Forge App Builder, Forge App Review, Commit, Changelog skills in `.agents/skills/`
- **Give a goal:** "Build a Jira issue panel that shows related Confluence pages. See PROJ-123." — the agent reads the Jira issue, selects the right Forge module, writes and wires the code
- **Agent tests:** runs `forge tunnel`, reads error output, iterates until tests pass — no human intervention needed
- **Agent reviews:** Forge App Review skill checks security, cost efficiency, performance, architectural patterns
- **Agent deploys:** `forge deploy` → `forge install` → marks PROJ-123 Done via Atlassian MCP
- **The bottom line:** a developer new to Forge can be productive on day one — the agent handles platform knowledge, the developer focuses on business logic

</details>

---

### Three levels of AI adoption — start where you are, progress at your pace

| Level | Goal | What to do | Result |
|---|---|---|---|
| **1 — Config Assistant** | Stop looking up documentation | Add the Forge MCP Server to your existing AI tool | Instant answers on manifest syntax, module types, API scopes |
| **2 — Pair Programmer** | Accelerate feature development | Add `atlassian/forge-skills` to get Forge App Builder + Review skills | You write the logic; the agent writes the boilerplate |
| **3 — Autonomous Agent** | Idea to deployment | Provide a Jira issue link; agent reads spec, creates app, deploys, and tests | Dramatic reduction in "Time to Value" |

> Start at Level 1 today — it takes under 10 minutes. Move to Level 2 when you're comfortable. Level 3 is ready when you are.

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- This framing removes the "all or nothing" barrier — many developers feel intimidated by the vision of a fully autonomous agent
- Level 1 (MCP Server only) delivers immediate value with zero workflow disruption — stay in your current IDE, just add one config entry
- Level 2 adds the forge-skills bundle: the agent now scaffolds Forge apps with correct module selection, manifest setup, and UI Kit patterns — the developer stays in control of the logic
- Level 3 is the autonomous flow: give it a Jira issue URL and walk away; the agent reads the spec, creates the app, runs forge tunnel, iterates on errors, and deploys
- Transition: "Let's walk through exactly how to get started at Level 1 right now."

</details>

---

### Start in minutes: add the Forge MCP Server to your current AI tool

You don't need to adopt everything at once. Here's a practical progression:

**⚡ Level 1 — Immediate value (30 minutes)**
1. Add the Forge MCP Server to your existing AI tool (Claude Desktop, Cursor, VS Code)
2. Ask it Forge questions — watch it give accurate, up-to-date answers from developer.atlassian.com
3. Use it to scaffold your next Forge app component

**🚀 Level 2 — Full agentic workflow (2 hours)**
1. Install Rovo Dev CLI *or* configure Claude Code / Cursor with agent mode
2. Add Forge MCP + Atlassian MCP to your MCP config
3. Add Forge App Builder and Forge App Review skills to `.agents/skills/`
4. Give the agent a Forge app goal and let it work

**🎯 Level 3 — No-code path (20 minutes)**
1. Open Atlassian App Studio in your Atlassian admin panel
2. Describe the app you want in natural language
3. Review the generated spec, adjust if needed, and deploy

**Key resources:**
- 📖 Forge docs: `developer.atlassian.com/platform/forge/`
- 🔌 Forge MCP Server: `mcp.atlassian.com/v1/forge/mcp`
- 🔷 Atlassian MCP Server: `developer.atlassian.com/cloud/jira/platform/mcp/`
- 📋 Agent Skills spec: `agentskills.io`

#### Speaker notes

<details>
<summary>Speaker notes</summary>

This is the action slide. The key message is: start small, see immediate value, then progressively adopt more of the stack.

**Level 1 — The Forge MCP Server is a game changer in isolation:**
No new tools required. Just add a JSON config entry to Claude Desktop, Cursor, or VS Code. The agent immediately gets accurate Forge knowledge instead of hallucinating from outdated training data. This alone is worth doing today.

Config snippet:
```json
{
  "mcpServers": {
    "forge": {
      "url": "https://mcp.atlassian.com/v1/forge/mcp",
      "transport": "http"
    }
  }
}
```

**Level 2 — The full agentic experience:**
Set aside 2 hours to configure and run your first fully agentic Forge app build. The first time you see the agent automatically add the right API scopes to the manifest, fix a UI Kit component error from `forge tunnel` output, and pre-emptively structure the code for cost efficiency — you'll understand why this is a step-change in productivity.

**Level 3 — No-code for the right use cases:**
If you're an Atlassian admin or building something relatively simple (an approval workflow, a custom form, a dashboard, a Rovo Agent), App Studio can have you in production in under 20 minutes. Share this path with non-developer colleagues — it's genuinely accessible.

**Questions to anticipate:**
- "Does this work with Claude Code / Cursor / Windsurf — not just Rovo Dev?" — Yes, the Forge MCP Server works with any MCP-compatible client.
- "How much does Forge cost?" — Most single-site apps stay within the free tier. Sandbox usage now free.
- "Is the generated code production-quality?" — Better than ever, but always review. The Forge App Review skill helps with pre-deploy auditing.
- "Can I use my team's existing Atlassian permissions?" — Yes, the Atlassian MCP Server respects all existing Jira/Confluence permissions automatically.

</details>

---

### The future of Forge development is agents writing agents

**What's coming:**

- 🔮 **Deeper Rovo + Forge integration** — Rovo Studio evolving from app builder to full app lifecycle manager: spec → build → review → deploy → monitor
- 📦 **`atlassian/forge-skills` expansion** — more skills covering JSM, Assets, Teamwork Graph connectors, and Rovo Chat integrations
- 🤖 **Forge apps that deploy AI agents** — Forge is already a platform for hosting Rovo agents; expect richer agent-building primitives
- 🌐 **MCP ecosystem growth** — the Atlassian MCP Server is actively adding capabilities; Bitbucket (April 2026) was the latest addition

> *The platform is ready. The standards are settled. The only variable is how quickly teams adopt them.*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- This slide is forward-looking — it's permission to be excited about where things are going, not just where they are today
- Rovo Studio is the most immediately exciting development: moving from "describe an app and it builds it" to managing the full lifecycle — spec, build, review, deploy, monitor — with governance baked in at every step
- The forge-skills bundle will grow: JSM Assets integration and Teamwork Graph connector skills are natural next steps as more teams build connectors
- The paradigm shift to leave them with: we're moving from writing every line of code to describing intent and orchestrating agents; Forge — with its declarative manifests, module system, and built-in security — is exceptionally well-positioned for this shift
- Transition: "Let's bring it all together in a summary."

</details>

---

### The AI dev tool landscape has crystallised into four categories — choose by autonomy level

**The AI software development landscape — May 2026:**

| Category | Key Players | Best For |
|---|---|---|
| **AI Dev Agents** | Rovo Dev, Claude Code, Codex CLI, Antigravity 2.0, Devin, Cline | Autonomous multi-step coding tasks |
| **AI-Native IDEs** | Cursor, Windsurf, Replit | Full AI-first development environment |
| **IDE Extensions** | GitHub Copilot, JetBrains AI Assistant, Tabnine | AI in your existing editor |
| **Hosted AI IDEs** | Atlassian App Studio, Lovable, Bolt.new | No-code / low-code to production |

The right choice depends on **how much autonomy you want the AI to have** — and how much control you want to retain.

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- This is the summary of the landscape — four clear categories, each serving a different developer persona and level of AI autonomy
- The key question to leave the audience with: "Where do you sit on the autonomy spectrum?" — most developers will start lower (extensions) and move higher (agents) as they build confidence
- Transition: "The landscape is the context. Now here are the three specific enablers that make building Forge apps with AI practical today."

</details>

---

### The tools are ready — AI agents, MCP Servers, and skills can build Forge apps today

> 💡 **Presenter note:** Conduct Q&A before advancing to this slide. End on the key message below, not on a question from the floor.

> **MCP Servers are the connection. Agent Skills are the knowledge. Forge is the platform.**

**Key enablers for Forge development:**

| Enabler | What it does |
|---|---|
| 🔶 **Forge MCP Server** | Gives any AI agent deep Forge knowledge from developer.atlassian.com |
| 🔷 **Atlassian MCP Server** | Connects any AI tool to Jira, Confluence, Bitbucket securely |
| 📋 **Agent Skills** | Encodes your team's Forge workflows as reusable instructions |
| 🔶 **Atlassian App Studio** | No-code path from natural language to deployed Forge app |

> **The bottom line:** Building Forge apps with AI is not just about writing code faster — it's about describing what you want and letting AI handle the rest. The tools are ready. Start today.

#### Speaker notes

<details>
<summary>Speaker notes</summary>

- MCP Servers are the glue — they let any agent connect to any tool through a standard protocol; the Forge MCP Server and Atlassian MCP Server make Atlassian a first-class citizen in every AI tool ecosystem — not lock-in, integration
- Agent Skills are the team's institutional memory — encode standards and workflows once, every AI agent in every session benefits automatically
- Forge is uniquely well-suited for AI-assisted development: constrained problem space, declarative configuration, rich up-to-date documentation, built-in security
- **The paradigm shift to leave them with:** we're moving from writing every line of code to describing intent and orchestrating agents; Forge — with its declarative manifests, module system, and built-in security — is exceptionally well-positioned for this shift
- **Final questions to expect:**
  - "Which agent should I use?" — Start with what you have. Rovo Dev is included in Atlassian Cloud Standard/Premium/Enterprise. Otherwise, Claude Code (free tier) + Forge MCP is an excellent free starting point
  - "How do I convince my team?" — Demo it. Take a real Jira issue, give it to an agent with the Forge MCP Server configured, show the result
  - "What about security and IP?" — Forge code runs on Atlassian infrastructure; Atlassian MCP respects existing permissions; check each AI vendor's data retention policies for code sent to external APIs; Tabnine and Windsurf (enterprise) offer self-hosted options for air-gapped environments

</details>
