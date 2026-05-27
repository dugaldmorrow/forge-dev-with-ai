# Skipped Slides

Slides that have been removed from [Presentation.md](./Presentation.md) but retained here for reference.

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
