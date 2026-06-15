# Skipped Slides

Slides that have been removed from [Presentation.html](./Presentation.html) but retained here for reference.

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

### App Studio deploys Forge apps from plain language

1. Generates a feature spec outlining what the app does, where it lives, how it behaves
2. Developer reviews and approves the spec
3. Rovo builds the app: selects modules, generates UI Kit code, wires backend + permissions
4. One-click deploy to your Atlassian site

#### Speaker notes

<details>
<summary>Speaker notes</summary>

"App Studio is the zero-code path to a deployed Forge app. Worth a live demo if time allows. Describe the app, review the spec, and deploy. Governance is built-in: Atlassian admins control which apps can be installed and enterprise customers get approval workflows before deployment."

- The agent calls the Forge MCP Server to select the correct module type and scopes
- Current limitation: best for simpler apps; complex custom UI or resolver logic may still require a developer's hand

</details>

---

### Four categories — choose by abstraction level

| Category | Abstraction Level | Best For |
|---|---|---|
| **AI Coding Assistants** | Token / line | AI in your existing editor; lowest switching cost |
| **AI-Native IDEs** | Task / file | AI-first editing with you still in control |
| **AI Dev Agents** | Goal / feature | Multi-step coding tasks; hand off and review |
| **Autonomous Dev Platforms** | Intent / product | No-code / low-code to production; no environment to configure |

#### Speaker notes

<details>
<summary>Speaker notes</summary>

"To summarise the landscape: four categories, each sitting at a different level on the abstraction ladder. The higher you go, the less you specify how and the more you specify what. Choose based on where your team sits today on that ladder."

- AI Coding Assistants (token/line): the developer is still coding — the AI accelerates keystrokes, not decisions
- AI-Native IDEs (task/file): the developer directs; the AI executes a bounded piece of work within the session
- AI Dev Agents (goal/feature): the developer delegates; the AI plans, iterates, and reports back
- Autonomous Dev Platforms (intent/product): the developer describes the outcome; the AI handles architecture, implementation, and deployment
- Cursor and Rovo Dev often get compared but sit in different categories: Cursor is an AI-Native IDE (task/file level), Rovo Dev is an AI Dev Agent (goal/feature level)

</details>
