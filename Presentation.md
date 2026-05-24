
# Forge App Development with AI

A presentation about AI-assisted software development, with a focus on building Forge apps using AI agents, MCP servers, and agent skills.

---

## Slides

### What is an AI Software Development Agent?

An AI software development agent is an autonomous system powered by a large language model (LLM) that can plan, reason, use tools, and execute multi-step coding tasks with minimal human intervention. Unlike a chatbot that answers one question at a time, an agent pursues a *goal* — reading your codebase, writing code, running tests, fixing failures, and iterating — until the job is done.

**Key characteristics:**
- 🎯 **Goal-directed** — works toward a defined objective across many steps
- 🔧 **Tool use** — reads/writes files, runs terminal commands, calls APIs, browses the web
- 🔁 **Reasoning loops** — plans, executes, observes results, and adjusts
- 🧠 **Context-aware** — understands your codebase, project structure, and prior work
- 🤝 **Human-in-the-loop** — works *with* you, not just *for* you

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

### What is Inference?

**Inference** is the execution phase of an AI model — when a trained model receives an input (a prompt) and generates an output (a response). Every time an LLM generates code, answers a question, or takes an action, it is performing inference.

**Why it matters for developers:**

| Concept | What it means |
|---|---|
| **Token-based billing** | You pay per token — every word in and out has a cost |
| **Agentic amplification** | Agents use 5–30× more tokens per task than a chatbot |
| **Context window** | The "working memory" of a session — longer context = more tokens |
| **LLMflation** | Inference costs drop ~10× per year — rapidly becoming cheaper |

> *By 2030, running inference on a 1-trillion-parameter model will cost over 90% less than in 2025.*

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

### The AI Dev Tool Landscape

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

### AI Software Development Agents

The most autonomous category — agents that independently plan, write, test, and ship code.

| Agent | Creator | LLMs | Configurable? | Distinctive Feature |
|---|---|---|---|---|
| **Rovo Dev** | Atlassian | GPT, Claude, Gemini + open-source | Limited (switch with /model) | Atlassian Teamwork Graph; usage-based credits |
| **Claude Code** | Anthropic | Claude only (Opus/Sonnet/Haiku) | Yes (/model command) | Agent View + /goal; locked to Anthropic ecosystem |
| **Codex CLI** | OpenAI | GPT-5.x series; local via Ollama | Yes (/model command) | ~4M weekly users; open source; Goal mode |
| **Google Antigravity 2.0** | Google | Gemini (default), Claude, GPT-OSS | Yes | Multi-model routing; launched May 19 2026 |
| **Devin** | Cognition AI | Proprietary SWE-1 / SWE-1.5 | ❌ No | First "autonomous AI software engineer"; from $20/mo |
| **Cline** | Community (MIT) | 200+ models (Claude, GPT, Gemini, Ollama…) | Yes — fully | 5M+ installs; bring your own API key; fully open source |

> *Claude Code and Devin 2.0 lead SWE-bench Verified benchmarks at ~71–73% task completion (up from ~14% at Devin's 2024 launch).*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

Let's look at each major agent:

**Rovo Dev (Atlassian)** — Atlassian's own coding agent. Distinctive because of the Teamwork Graph — it understands your Jira issues, Confluence docs, Bitbucket PRs, and Compass components, connecting context across your whole project. Available included with Standard, Premium, or Enterprise Cloud plans of Jira, Confluence, or JSM.

**Claude Code (Anthropic)** — Lives in your terminal. The May 2026 "Code with Claude" event introduced Agent View (manage a fleet of agents from one interface) and the /goal command (give an objective, the agent pursues it with a second supervisor Claude verifying the result). Works with Opus 4.6, Sonnet 4.6, Haiku 4.5 models. Enterprise: Amazon Bedrock or Google Vertex AI.

**Codex CLI (OpenAI)** — Open source (Rust), runs locally. NOT the original Codex API from 2021. Launched April 2025, now ~4M weekly active users (confirmed April 2026). Available as CLI, web (chatgpt.com/codex), IDE extensions, and Codex app. Goal mode for multi-hour/multi-day objectives. Powered by GPT-5.5.

**Google Antigravity 2.0** — Brand new, launched May 19 2026 at Google I/O. Desktop app + CLI (`agy`) + SDK + Gemini API managed agents tier. Powered by Gemini 3.5 Flash. Multi-agent parallel orchestration and scheduled background tasks. AI Ultra plan ($100/mo) for 5× higher limits.

**Devin (Cognition AI)** — The "first autonomous AI software engineer." Devin 2.0 (April 2025) slashed price from $500 to $20/month (Core plan). Interactive Planning: analyses your codebase, proposes a plan, lets you iterate together. Parallel Devins. SWE-bench: 71%. Real-world complex task completion: ~14-15% (independent testing).

**Cline** — MIT licensed, 5M+ installs, 58,000+ GitHub stars. Runs inside VS Code. Bring your own API keys (Claude, OpenAI, Gemini, or local via Ollama). The open-source choice for transparency and control. Lightweight extension — keep your existing VS Code setup.

</details>

---

### Spotlight: Atlassian Rovo Dev

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

### AI-Native IDEs

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

### IDE Extensions & Editor Companions

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

IDE Extensions are the most accessible entry point. You keep your existing editor, your existing workflow, and add AI capability on top. Lower disruption, lower switching cost.

**GitHub Copilot** is the most widely adopted AI coding assistant on the planet. Plugin — works inside VS Code, JetBrains IDEs, Neovim, Visual Studio. Has evolved far beyond autocomplete: Copilot Chat, Copilot Workspace, agent mode, autonomous PR creation, GitHub Spark for natural language app building, semantic code search. 5-tier pricing: Free ($0), Pro ($10/mo, 300 premium requests), Pro+ ($39/mo, 1500 premium requests), Business ($19/user/mo), Enterprise ($39/user/mo). Warning: Microsoft is moving toward token billing in May–June 2026 — the "all you can eat" era is ending. Heavy agentic users will see cost increases.

**JetBrains AI Assistant** is the natural choice for Java, Kotlin, Python developers on IntelliJ, PyCharm, WebStorm. Type-aware completion: the IDE already parses code into syntax trees, so AI suggestions are grounded in actual type information. Junie (launched January 2026) is their autonomous agent for full task execution. Pricing: AI Pro Individual $10/mo, AI Pro Business $20/mo, AI Ultimate $30/mo. Important: separate subscription from IDE licence — you need both.

**Tabnine** (launched 2018, predating Copilot) is the privacy-first option. Zero code retention, no training on your code, self-hosted deployment available (VPC, on-premises, air-gapped). Enterprise: custom model training on your codebase, MCP integration, CLI access, unlimited codebase connections. $12/mo (Dev), $39/user/mo (Enterprise). Retired free plan in 2024. The right choice for regulated industries or organisations with strict IP protection requirements.

</details>

---

### Hosted AI-Native IDEs

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

Hosted AI-Native IDEs remove all setup friction. Open a browser, describe what you want, and the AI builds it. No CLI, no npm install, no environment configuration.

**Atlassian App Studio (Rovo Studio)** — Forge-specific. Describe the app in natural language, Rovo designs the spec, selects Forge modules, generates UI Kit code, wires backend, storage, and permissions. Open beta March 2026, auto-rolled out from May 2026. No code required. Agents can be built in under 20 minutes. Governance built-in: org policies, roles, per-agent permissions, approvals, versioning, audit logs. Uses consumption-based Forge pricing — mostly free for internal/single-site apps.

**Lovable** — $100M ARR in 8 months (reportedly fastest-growing startup in history). Generates full-stack apps with Supabase integration, one-click deployment, GitHub sync. Feels like a product builder, not a code editor. Limitation: backend limited to Supabase. Real limitation: generates code but still requires user to configure auth, RLS policies, and deployment.

**Bolt.new** — StackBlitz's WebContainer approach: full cloud IDE (you can see file tree, terminal, preview) with AI assistance. Token-based billing ($40–100/month for serious development). Some npm packages incompatible with browser sandbox.

**v0.dev** — Vercel's frontend-only tool. Generates production-quality React/Tailwind components. No backend. Best for frontend developers already in the Vercel/Next.js ecosystem.

The "Technical Cliff" refers to the moment vibe-coding tools produce a beautiful mockup that fails at production infrastructure. App Studio sidesteps this entirely — Forge is the production infrastructure, serverless, with auth and scaling handled.

</details>

---

### What is an MCP Server?

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

### Key MCP Servers for Forge Developers

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

**Add the Forge MCP Server to any AI tool:**
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

#### Speaker notes

<details>
<summary>Speaker notes</summary>

The Forge MCP Server is the headline item for this audience. GA announced February 4, 2026; published March 2, 2026. It's a *remote* server — no local installation required, just add the URL to your MCP config.

**What the Forge MCP Server specifically provides:**
- **How-to guides** — information about building Forge apps with code snippets for common tasks
- **Module catalogs** — recommends the right Forge module for your use case (jira:issuePanel, confluence:macro, etc.)
- **Manifest guidance** — help with manifest structure, scopes, and permissions
- **Forge document search** — searches developer.atlassian.com for Forge and Atlassian Cloud API documentation
- **Agent-friendly responses** — structured so agents can turn guidance directly into working code

Workflow: Agent calls `forge-development-guide` → then `forge-ui-kit-developer-guide` / `forge-modules-list` / `forge-app-manifest-guide` as needed → then `search-forge-docs` for specifics → generates correct Forge code.

Note: The Forge MCP server only provides publicly available information, no auth required. Data is sourced from developer.atlassian.com. One limitation: information may become stale if the knowledge index is not refreshed regularly.

**Atlassian MCP Server** (GA February 2026, Claude as first partner; expanded April 2026 to include Bitbucket): Supports Jira, Confluence, Compass, Bitbucket. Read and write operations. Supported by 20+ AI clients including Claude, ChatGPT, Cursor, VS Code, Devin, GitHub, Lovable, Figma, Mistral. Security: OAuth 2.1, HTTPS/TLS 1.2+, respects existing Atlassian permissions, admin whitelisting controls.

**Configuration file locations by tool:**
- Claude Desktop: `~/Library/Application Support/Claude/claude_desktop_config.json` (Mac)
- Cursor: `~/.cursor/mcp.json`
- Windsurf: `~/.codeium/windsurf/mcp_config.json`
- VS Code: `settings.json` under the `mcp.servers` key

Common gotcha: JSON doesn't allow trailing commas. Validate with jsonlint.com. Also: fully restart the app (not just the window) after config changes.

</details>

---

### What is an AI Agent Skill?

**Agent Skills** are reusable packages of instructions, scripts, and resources that teach an AI agent how to perform specific tasks consistently — like giving a new team member a standard operating procedure that they can refer to whenever they need it.

**Skills vs. MCP Servers:**

| | MCP Server | Agent Skill |
|---|---|---|
| **What it is** | A tool/API connector | A reusable instruction set |
| **Provides** | Capabilities (can do things) | Knowledge (how to do things) |
| **Format** | Running server process | Markdown file (SKILL.md) |
| **Best for** | Accessing live external systems | Encoding repeatable workflows |
| **Token cost** | Higher (live connections) | Lower (loaded on demand only) |

**How skills work — Progressive Disclosure:**
1. **Discover** (~100 tokens) — agent sees skill name + description at startup
2. **Activate** — agent loads full SKILL.md when the task matches
3. **Execute** — agent follows instructions, loads referenced files as needed

> *"Skills are the agent's toolkit — the specific capabilities it can invoke to get things done. Instructions are the agent's mindset — what it knows and how it should behave."*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

Agent Skills are a concept formalised as an open standard at agentskills.io (Apache 2.0 licence), now supported by GitHub Copilot, Claude Code, OpenAI Codex, and Rovo Dev.

The best analogy: if an MCP server is like giving the agent a phone to call external services, a skill is like giving the agent your team's runbook — the specific way your team does things.

**Skills vs MCP in practice:**
- MCP gives the agent *capabilities* (access to Jira, ability to run terminal commands, Forge documentation)
- Skills give the agent *knowledge* (your commit message format, your pre-deploy checklist, your architectural standards)

They complement each other: a Forge App Builder skill uses the Forge MCP Server under the hood to get up-to-date Forge knowledge, while the skill itself encodes your team's specific patterns and preferences.

**Progressive disclosure** is efficient: skills don't load their full content into every prompt. Only ~100 tokens per skill at startup (name + description), then the full instructions load only when the task matches. This means you can have many skills without burning tokens unnecessarily.

The open standard means: build a skill once, use it across Claude Code, Codex CLI, GitHub Copilot, and Rovo Dev — without modification.

</details>

---

### Configuring Agent Skills

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

### Where to Put Your Skills

The SKILL.md format is a shared open standard — but each tool looks for skills in its own directory. The standard recommends `.agents/skills/` in your project root, but many tools use a tool-specific path instead.

**Project-level skills** (checked into your repo — shareable with the team):

| Tool | Project skills directory |
|---|---|
| **Codex CLI** | `.agents/skills/` ✅ standard |
| **GitHub Copilot** | `.agents/skills/`, `.github/skills/`, or `.claude/skills/` |
| **Rovo Dev** | `.agents/skills/` or `.rovodev/skills/` |
| **Claude Code** | `.claude/skills/` |
| **Cursor** | `.cursor/skills/` |
| **Windsurf** | `.windsurf/skills/` |

**Global skills** (personal, available across all your projects):

| Tool | Global / personal skills directory |
|---|---|
| **Codex CLI** | `~/.codex/skills/` |
| **GitHub Copilot** | `~/.agents/skills/` or `~/.copilot/skills/` |
| **Rovo Dev** | `~/.agents/skills/` or `~/.rovodev/skills/` |
| **Claude Code** | `~/.claude/skills/` |
| **Windsurf** | `~/.codeium/windsurf/skills/` |
| **Cursor** | ❌ No global skills support |

> 💡 **Recommended approach:** Use `.agents/skills/` in your project root for maximum portability. Rovo Dev, Codex CLI, and GitHub Copilot all recognise it natively. For Claude Code, Cursor, and Windsurf, create a symlink from their expected directory to `.agents/skills/`.

#### Speaker notes

<details>
<summary>Speaker notes</summary>

This is one of the messier corners of the agent skills ecosystem — the standard exists but compliance is inconsistent, and each tool carved out its own path.

**The story of the standard:**
The `.agents/skills/` path is the open standard defined at agentskills.io. Anthropic created both the Agent Skills open standard *and* Claude Code. Yet Claude Code itself uses `.claude/skills/` instead of `.agents/skills/` — the standard its own creators defined. This has caused real friction in the community since mid-2025.

**Two levels of skills:**
- **Project-level** — lives inside your repository, committed to git. When a teammate pulls the repo, they immediately have all the team's skills available. Perfect for encoding team standards (commit format, Forge app review checklist, etc.).
- **Global / personal** — lives in your home directory. Available in every project on your machine. Good for personal preferences (preferred code style, language settings, tools you always use).

Project skills take precedence over global skills when names conflict.

**The symlink trick:**
If you want to maintain one authoritative set of skills in `.agents/skills/` and have all tools see them, create symlinks:
```bash
# For Claude Code
ln -s .agents/skills .claude/skills

# For Cursor
ln -s .agents/skills .cursor/skills

# For Windsurf
ln -s .agents/skills .windsurf/skills

# For Rovo Dev
ln -s .agents/skills .rovodev/skills
```

**The installer shortcut:**
The `npx skills` CLI (and similar package managers) handles directory detection automatically — it detects which agents are installed and copies/symlinks skills to all the right places. For teams adopting skills for the first time, this is the lowest-friction path.

**Cursor's global skills limitation:**
Cursor is the only major tool with no global skills support. If you want a personal skill available in all your Cursor projects, you have to copy it into each project's `.cursor/skills/` directory manually (or use a setup script).

**For Forge developers specifically:**
If you're using Rovo Dev as your primary agent, `.agents/skills/` is the recommended location — Rovo Dev recognises it natively alongside `.rovodev/skills/`. If you're also using Cursor or Windsurf, create symlinks from their expected directories to your `.agents/skills/` source of truth.

</details>

---

### Forge: The Ideal Platform for AI-Built Atlassian Apps

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

### Building Forge Apps with AI: Two Paths

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

### Atlassian's AI Development Stack

Atlassian has built a comprehensive AI development ecosystem — and opened it to any AI tool:

**Forge MCP Server** *(GA February 2026)*
Provides AI agents with deep Forge knowledge — how-to guides, module catalogs, manifest guidance, API search. Sourced from developer.atlassian.com. No authentication required. Any developer with any AI tool can use it.

**Atlassian MCP Server** *(GA February 2026, expanded April 2026)*
Connects any AI tool to Jira, Confluence, Bitbucket, and Compass with enterprise security. OAuth 2.1, full permission inheritance, admin whitelisting. Supported by 20+ AI clients including Claude, ChatGPT, Cursor, VS Code, Devin, GitHub, and more.

**Atlassian App Studio / Rovo Studio** *(Open Beta March 2026)*
No-code Forge app builder. Natural language to production Forge app in under 20 minutes. Enterprise governance built-in.

**Volt Studio & Socrates** *(Internal)*
Internal Atlassian tools for app building and data analytics that reflect the depth of Atlassian's internal AI investment.

> *"Over a million people use AI on the Atlassian platform each month."*

#### Speaker notes

<details>
<summary>Speaker notes</summary>

This slide shows that Atlassian is a serious player in the AI development ecosystem — not just talking about AI but actually building and shipping at scale.

**The strategic insight in the Atlassian MCP Server:** Rather than trying to force everyone to use Rovo Dev, Atlassian says "use whatever AI tool you want — we'll connect it to your Atlassian data securely." This is an ecosystem play that benefits Atlassian customers regardless of which AI agent they prefer.

Supported clients for the Atlassian MCP Server: AWS, ChatGPT, Claude, Cursor, Devin, Docker, Figma, GitHub, Google, Lovable, Mistral, Postman, Resolve, VS Code, WRITER, and more.

**Bitbucket support** (added April 2026): AI clients can now browse repositories, create commits, open pull requests, and check pipeline results through the same MCP connection that already works with Jira and Confluence. This closes the loop on the full development lifecycle.

**Security model:** Enterprise-first. Atlassian-hosted (no separate infrastructure). OAuth 2.1. Respects existing Jira and Confluence permissions — the AI only sees what the authenticated user can see. Admins can whitelist which MCP clients are allowed. TLS 1.2+ for all traffic.

**Volt Studio and Socrates:** These are internal Atlassian tools with limited public documentation. Volt Studio appears to be an internal tool for building apps and automations. Socrates is an internal MCP server for data and analytics capabilities. These demonstrate that Atlassian uses AI development tooling deeply internally — they're eating their own dog food.

The 1 million monthly AI users figure: this isn't a prototype number. This is at scale, in production.

</details>

---

### Putting It All Together: The AI Forge Developer Stack

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

#### Speaker notes

<details>
<summary>Speaker notes</summary>

This is the synthesis slide — showing how all the pieces fit together into a coherent, practical workflow.

**The complete workflow in practice:**

1. **Configure once:** Add Forge MCP Server + Atlassian MCP Server to your AI agent config. Add Forge App Builder, Forge App Review, Commit, and Changelog skills to `.agents/skills/`.

2. **Start a session:** Launch Rovo Dev (or Claude Code / Cursor with MCP configured)

3. **Give a goal:** "Build a Jira issue panel that shows related Confluence pages and allows linking them. See the spec in PROJ-123."

4. **Agent reads context:** Checks Jira issue PROJ-123 via Atlassian MCP for requirements. Calls Forge MCP to understand which module to use, what scopes are needed, what UI Kit components are available.

5. **Agent builds:** Scaffolds the app with `forge create`, writes the component code, sets up backend functions, wires permissions in the manifest (including correct API scopes — automatically).

6. **Agent tests:** Uses `forge tunnel` to test in real Atlassian instance; reads error output and iterates until tests pass.

7. **Agent reviews:** Runs the Forge App Review skill — checks security, cost efficiency, performance, architectural patterns.

8. **Developer reviews:** You look at the generated code and the review report. Make any adjustments.

9. **Agent deploys:** `forge deploy` → `forge install` → updates Jira issue PROJ-123 status to Done via Atlassian MCP.

**The bottom line:** A developer who previously spent a week learning Forge module types, manifest syntax, API scopes, and UI Kit components can now start building productively on day one. The AI agent — equipped with the Forge MCP Server, Atlassian MCP Server, and appropriate skills — handles the platform knowledge, letting the developer focus on what matters: the unique business logic of their app.

</details>

---

### Getting Started Today

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

### Summary

**The AI software development landscape — May 2026:**

| Category | Key Players | Best For |
|---|---|---|
| **AI Dev Agents** | Rovo Dev, Claude Code, Codex CLI, Antigravity 2.0, Devin, Cline | Autonomous multi-step coding tasks |
| **AI-Native IDEs** | Cursor, Windsurf, Replit | Full AI-first development environment |
| **IDE Extensions** | GitHub Copilot, JetBrains AI Assistant, Tabnine | AI in your existing editor |
| **Hosted AI IDEs** | Atlassian App Studio, Lovable, Bolt.new | No-code / low-code to production |

**Key enablers for Forge development:**

| Enabler | What it does |
|---|---|
| 🔶 **Forge MCP Server** | Gives any AI agent deep Forge knowledge from developer.atlassian.com |
| 🔷 **Atlassian MCP Server** | Connects any AI tool to Jira, Confluence, Bitbucket securely |
| 📋 **Agent Skills** | Encodes your team's Forge workflows as reusable instructions |
| 🔶 **Atlassian App Studio** | No-code path from natural language to deployed Forge app |

> **The bottom line:** Building Forge apps with AI is not just about writing code faster — it's about describing what you want and letting AI figure out how to build it, with Forge, Rovo Dev, and MCP Servers handling the rest.

#### Speaker notes

<details>
<summary>Speaker notes</summary>

**Closing talking points:**

The landscape has crystallised into four clear categories. Each serves a different need and developer persona. The right choice depends on how much autonomy you want the AI to have and how much control you want to retain.

MCP Servers are the glue — they let any agent connect to any tool through a standard protocol. The Forge MCP Server and Atlassian MCP Server make Atlassian a first-class citizen in every AI tool ecosystem. This is not lock-in — it's integration.

Agent Skills are the team's institutional memory — encode your standards and workflows once, and every AI agent in every session benefits from them automatically.

Forge is uniquely well-suited for AI-assisted development: constrained problem space, declarative configuration, rich up-to-date documentation, built-in security. The Forge MCP Server brings this to any AI agent.

**The paradigm shift to leave them with:**
We're moving from a world where developers write every line of code to a world where developers describe intent and orchestrate agents. The Forge platform — with its declarative manifests, module system, and built-in security — is exceptionally well-positioned for this shift. The tools are ready. The MCP servers are live. The skills framework is open standard.

Start with Level 1. Add the Forge MCP Server to your current AI tool today.

**Final questions to expect:**
- "Which AI agent should I use?" — Start with what you have. If you're on Atlassian Cloud Standard/Premium/Enterprise, Rovo Dev is included. Otherwise, Claude Code (free tier) + Forge MCP is an excellent free starting point.
- "How do I convince my team?" — Start with a demo. Take a real Jira issue, give it to an AI agent with the Forge MCP Server configured, and show the result. The proof is in the output.
- "What about security and IP?" — All Forge code runs on Atlassian infrastructure. The Atlassian MCP Server uses your existing permissions. For code sent to external AI APIs, check each vendor's data retention policies. Tabnine and Windsurf (enterprise) offer self-hosted options for air-gapped environments.

</details>
