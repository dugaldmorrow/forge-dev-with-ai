---
name: quiz
description: Tests the user's understanding of the presentation content by posing a single, thoughtfully chosen question at an appropriate interval. Tracks question history in a state file to avoid repeating questions and to respect a minimum cooldown between quizzes, so the user is never annoyed.
---

# Quiz Skill

## Overview

This skill challenges the user with one question about the content of the presentation "Forge App Development with AI". Its goal is to reinforce understanding of the key ideas in a low-friction, non-intrusive way.

Apply this skill when:
- The user explicitly asks to be quizzed, tested, or asked a question about the presentation.
- The user has just finished reviewing, editing, or discussing a section of the presentation and a self-check would be valuable.
- The skill is loaded as part of a standing brief (e.g. via `AGENTS.md`) and the cadence rules permit a new question.

**Never ask more than one question per invocation.** After receiving the user's answer, provide brief, encouraging feedback and explain the correct answer if needed — then stop. Do not chain multiple questions in a single session unless the user explicitly asks for more.

---

## Cadence Rules — Read the State File First

Before asking any question, you **must** read the state file at `.agents/skills/quiz/quiz-state.json`.

### Decision logic

1. **Read** `.agents/skills/quiz/quiz-state.json`. If the file does not exist, treat `last_asked_iso` as `null` and `asked_ids` as `[]`.
2. **Calculate elapsed time** since `last_asked_iso`. If `last_asked_iso` is `null`, elapsed time is infinite.
3. **Apply the cooldown rule**: if elapsed time is **less than 24 hours**, do **not** ask a question. Acknowledge silently and proceed with whatever the user actually asked. Do not tell the user you are skipping the quiz — just skip it.
4. **If cooldown has elapsed** (or this is the first ever run), choose a question and proceed.

### Choosing a question

- Prefer questions whose `id` is **not** in `asked_ids`.
- If all questions have been asked, reset — treat all questions as available again and clear `asked_ids` in the state file.
- Among available questions, prefer those that **contrast with the most recently asked question's `topic`** (i.e., vary the topics so consecutive quizzes cover different areas).
- Use **pseudo-random selection** weighted toward questions not asked recently — do not always pick the first available question.

### Updating the state file

After asking a question (regardless of whether the user answers), **immediately update** `.agents/skills/quiz/quiz-state.json`:

```json
{
  "last_asked_iso": "<ISO 8601 UTC timestamp of now>",
  "last_asked_id": <id of question just asked>,
  "asked_ids": [<all previously asked ids, plus the one just asked>]
}
```

Write the file using the `create_file` or `find_and_replace_code` tool. Never leave the state file in an inconsistent state.

---

## Question Format

Present each question clearly. Use this format:

```
💡 **Quick knowledge check:**

{question text}

{answer options if multiple-choice, or a blank line if open-ended}

Take your time — there's no pressure.
```

After the user responds, reply with:

```
{✅ Correct! / 🤔 Good try! / 💬 Here's the answer:}

{1–3 sentences explaining the correct answer and why it matters, referencing the presentation.}
```

Then ask: "Would you like another question, or shall we get back to work?"

---

## Question Bank

The following 20 questions are derived directly from the presentation slides. Each has a unique `id`, a `topic` tag for rotation, a `type` (multiple-choice `mc` or open-ended `oe`), the `question` text, the `correct_answer`, and `answer_options` (for mc only).

---

### Q1
- **id**: 1
- **topic**: agents-vs-autocomplete
- **type**: mc
- **question**: What is the fundamental difference between AI autocomplete tools and AI agents?
- **answer_options**:
  - A) Autocomplete tools are free; agents cost money
  - B) Autocomplete predicts the next token; agents pursue goals across multiple steps
  - C) Agents only work inside IDEs; autocomplete works anywhere
  - D) Autocomplete is more accurate than agents
- **correct_answer**: B
- **explanation**: The presentation draws a clear line: autocomplete (like early GitHub Copilot) predicts the next token based on context. Agents plan, execute, and iterate toward a goal — they take actions, use tools, and course-correct.

---

### Q2
- **id**: 2
- **topic**: four-categories
- **type**: oe
- **question**: Name the four categories of AI development tools described in the presentation.
- **correct_answer**: AI software development agents, AI-Native IDEs, IDE Extensions & Editor Companions, and Hosted AI-Native IDEs.
- **explanation**: These four categories organise the AI development tool landscape by the level of autonomy and integration. Agents are most autonomous; IDE extensions are most lightweight.

---

### Q3
- **id**: 3
- **topic**: mcp
- **type**: mc
- **question**: What does MCP stand for, and what role does it play in AI development?
- **answer_options**:
  - A) Multi-Cloud Protocol — it connects cloud providers
  - B) Model Context Protocol — it connects AI agents to external tools and data sources
  - C) Managed Code Pipeline — it automates CI/CD
  - D) Module Configuration Package — it manages npm dependencies
- **correct_answer**: B
- **explanation**: MCP (Model Context Protocol) is described in the presentation as a "universal adapter" — it allows any AI agent to connect to any tool or data source through a standardised interface, including the Forge MCP Server.

---

### Q4
- **id**: 4
- **topic**: forge-mcp
- **type**: oe
- **question**: What are the three MCP servers specifically mentioned in the presentation as accelerating Forge development?
- **correct_answer**: The Forge MCP Server, the Atlassian MCP Server, and the Socrates MCP Server.
- **explanation**: The presentation highlights these three as the core MCP server stack for Forge development. The Forge MCP Server provides Forge-specific knowledge; the Atlassian MCP Server provides live Atlassian context; Socrates provides data platform access.

---

### Q5
- **id**: 5
- **topic**: skills
- **type**: mc
- **question**: According to the presentation, approximately how many tokens does loading a skill consume at startup?
- **answer_options**:
  - A) ~10 tokens
  - B) ~100 tokens
  - C) ~1,000 tokens
  - D) ~10,000 tokens
- **correct_answer**: B
- **explanation**: The slide "Skills load progressively — ~100 tokens at startup" highlights that skills are designed to be lightweight. The agent loads a brief description at startup and fetches full content only when the skill is actually invoked.

---

### Q6
- **id**: 6
- **topic**: skills-vs-mcp
- **type**: mc
- **question**: Which statement best describes the distinction between MCP servers and agent skills?
- **answer_options**:
  - A) MCP servers are for Jira; skills are for Confluence
  - B) MCP gives the agent capabilities (tools and data); skills give the agent expertise (how to do a task)
  - C) Skills are remote; MCP is local
  - D) MCP and skills are interchangeable — they do the same thing
- **correct_answer**: B
- **explanation**: The presentation slide "MCP gives capabilities; skills give expertise" makes this distinction explicit. MCP servers expose tools and live data; skills encode reusable, opinionated workflows and domain knowledge.

---

### Q7
- **id**: 7
- **topic**: skills-vs-mcp
- **type**: mc
- **question**: Where do skills run relative to where MCP servers run?
- **answer_options**:
  - A) Skills are remote; MCP servers are local
  - B) Both are always remote
  - C) Skills are local (files in your repo); MCP servers are remote processes
  - D) Both are always local
- **correct_answer**: C
- **explanation**: The "Skills = Local; MCP = Remote" slide clarifies this. Skills are markdown files stored in your repository (e.g. `.agents/skills/`). MCP servers are separate processes that the agent connects to over a protocol.

---

### Q8
- **id**: 8
- **topic**: agents
- **type**: oe
- **question**: Name at least four of the six major AI coding agents compared in the presentation.
- **correct_answer**: Atlassian Rovo Dev, Google Antigravity 2.0, Claude Code (Anthropic), Codex CLI (OpenAI), Devin, and Cline.
- **explanation**: These six agents are presented in the "Six major AI coding agents compared" slide. They represent the leading autonomous agent solutions available to developers.

---

### Q9
- **id**: 9
- **topic**: rovo-dev
- **type**: oe
- **question**: What is the key differentiator of Rovo Dev compared to other AI coding agents?
- **correct_answer**: Rovo Dev retrieves Atlassian context more completely — it has native, deep integration with Jira, Confluence, and other Atlassian products, giving it richer project and organisational context.
- **explanation**: The slide "Rovo Dev retrieves Atlassian context more completely" captures this. Because Rovo Dev is built by Atlassian, it can access the full breadth of Atlassian product data natively, not just via generic MCP.

---

### Q10
- **id**: 10
- **topic**: four-categories
- **type**: mc
- **question**: Which of the following is classified as a "Hosted AI-Native IDE" in the presentation?
- **answer_options**:
  - A) GitHub Copilot
  - B) Cursor
  - C) Atlassian App Studio
  - D) JetBrains AI Assistant
- **correct_answer**: C
- **explanation**: Atlassian App Studio is the Hosted AI-Native IDE mentioned in the presentation. Cursor and Windsurf are AI-Native IDEs (locally installed). GitHub Copilot and JetBrains AI Assistant are IDE extensions.

---

### Q11
- **id**: 11
- **topic**: forge
- **type**: oe
- **question**: Why does the presentation claim Forge's architecture makes it ideal for AI-assisted development?
- **correct_answer**: Forge's constrained, opinionated architecture (sandboxed runtime, defined APIs, manifest-driven configuration) reduces the surface area of possible errors, making it easier for AI agents to generate correct, production-ready code.
- **explanation**: The slide "Forge's constraints make it ideal for AI" explains that Forge's guardrails — rather than being a limitation — actually help AI agents produce reliable output by narrowing the decision space.

---

### Q12
- **id**: 12
- **topic**: tool-invocation
- **type**: mc
- **question**: What does the presentation identify as the deciding factor in whether an agent invokes an MCP server or skill?
- **answer_options**:
  - A) The order they appear in the config file
  - B) The agent's internal confidence — whether it "believes" the tool is needed
  - C) The cost of the API call
  - D) The size of the tool's response
- **correct_answer**: B
- **explanation**: The warning slide states: "Presence in the config is not the same as guaranteed invocation. The agent's internal confidence is the deciding factor." Simply having an MCP server configured does not guarantee the agent will use it.

---

### Q13
- **id**: 13
- **topic**: tool-invocation
- **type**: oe
- **question**: What technique does the presentation recommend to force an agent to use a specific MCP tool or skill?
- **correct_answer**: Using @-mentions (e.g. `@forge-mcp`) to explicitly reference the tool in your prompt, signalling to the agent that it should invoke that specific capability.
- **explanation**: The slide "Use @-mentions to force tool invocation" describes this technique. It is one of the five techniques for improving tool invocation reliability.

---

### Q14
- **id**: 14
- **topic**: agents-md
- **type**: mc
- **question**: What is the purpose of an `AGENTS.md` file in a repository?
- **answer_options**:
  - A) It lists all the agents installed on the developer's machine
  - B) It provides a standing brief that gives every AI agent session persistent context about the project
  - C) It is a log of every action the agent has taken
  - D) It configures which LLM model the agent uses
- **correct_answer**: B
- **explanation**: "AGENTS.md gives every session a standing brief" — the file gives the AI agent persistent, project-specific context (personality, scope, key references, boundaries) at the start of every session without the user having to re-explain it.

---

### Q15
- **id**: 15
- **topic**: skills
- **type**: mc
- **question**: Where is the standard location for storing agent skills in a project?
- **answer_options**:
  - A) `/.mcp/skills/`
  - B) `/config/agents/`
  - C) `.agents/skills/`
  - D) `/src/skills/`
- **correct_answer**: C
- **explanation**: The slide "Use `.agents/skills/` — the standard location" establishes this convention. Storing skills here makes them discoverable by agents and keeps them version-controlled alongside the project.

---

### Q16
- **id**: 16
- **topic**: forge-mcp
- **type**: oe
- **question**: What does the presentation say App Studio can do that represents the upper boundary of AI-assisted Forge development?
- **correct_answer**: App Studio can deploy Forge apps from plain language descriptions — the developer describes what they want in natural language and App Studio generates and deploys the app.
- **explanation**: The slide "App Studio deploys Forge apps from plain language" illustrates the most automated end of the spectrum. It represents Level 3 AI adoption: no code required.

---

### Q17
- **id**: 17
- **topic**: adoption-levels
- **type**: mc
- **question**: The presentation describes three levels of AI adoption for Forge development. What is the recommended first step for Level 1?
- **answer_options**:
  - A) Build a complete Forge app using only AI
  - B) Add the Forge MCP Server to your AI tool now
  - C) Write an AGENTS.md file for your repository
  - D) Switch to an AI-native IDE like Cursor
- **correct_answer**: B
- **explanation**: "Level 1: add the Forge MCP Server now" is the simplest, lowest-friction starting point. It connects the agent to Forge-specific knowledge without requiring any code changes or workflow overhaul.

---

### Q18
- **id**: 18
- **topic**: governance
- **type**: oe
- **question**: What does the presentation say is necessary to keep AI-assisted Forge builds production-ready?
- **correct_answer**: Governance — human review, defined boundaries (via AGENTS.md and skills), and using MCP and skills together to reduce hallucinations and maintain quality standards.
- **explanation**: The slides "Governance keeps agentic builds production-ready" and "Reduce hallucinations with MCP, skills, and review" emphasise that autonomy must be paired with guardrails: agent skills encode the right workflow, MCP provides accurate context, and human review validates the output.

---

### Q19
- **id**: 19
- **topic**: ai-plugins
- **type**: mc
- **question**: What does the "Forge AI Plugin" bundle together?
- **answer_options**:
  - A) A Forge app, a Jira board, and a Confluence space
  - B) Skills, MCP server configuration, and host app metadata
  - C) An LLM model, a vector database, and a REST API
  - D) A CI/CD pipeline, test suite, and deployment manifest
- **correct_answer**: B
- **explanation**: The slide "The Forge AI Plugin bundles skills, MCP, and host metadata" describes how AI plugins package all three concerns together — making it easy to distribute a complete, opinionated AI development setup for Forge.

---

### Q20
- **id**: 20
- **topic**: three-key-messages
- **type**: oe
- **question**: What are the three key messages at the heart of this presentation?
- **correct_answer**: (1) MCP servers connect agents to Forge knowledge. (2) Agent skills encode reusable workflows and expertise. (3) Forge's constrained architecture is ideal for AI-assisted development.
- **explanation**: These three messages run through the entire presentation as the core thesis. Together they form the practical stack: agent + MCP + skills + Forge.

---

## Feedback Guidelines

When evaluating the user's answer:

- **Multiple-choice**: compare the letter or option chosen to `correct_answer`. Minor variations in phrasing are fine — focus on the intent.
- **Open-ended**: look for the key concepts in `correct_answer`. The user does not need to match the exact wording. Award credit for partial answers and gently fill in any gaps.
- **Tone**: always encouraging. Never make the user feel bad for a wrong answer. Frame incorrect answers as an opportunity to learn.
- **Length**: keep feedback concise — 2–4 sentences maximum. Link back to the slide or theme where relevant.

---

## Rules

- **Always** check the state file before asking a question. Never skip this step.
- **Never** ask more than one question per invocation unless the user explicitly asks for more.
- **Never** repeat a question that appears in `asked_ids` until all 20 have been asked.
- **Always** update the state file immediately after choosing a question, before waiting for the user's answer.
- **Respect the 24-hour cooldown** — if invoked as part of a standing brief (e.g. via `AGENTS.md`) and the cooldown has not elapsed, silently skip the quiz.
- **Never** make the user feel tested or judged. The tone is always curious and supportive.
- **Vary topics** — avoid asking two questions with the same `topic` tag in consecutive sessions.
- If the state file is corrupted or unreadable, treat it as missing and start fresh.
