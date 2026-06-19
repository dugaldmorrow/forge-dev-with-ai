---
name: speaker-notes
description: Defines the required structure and content conventions for speaker notes in the presentation. Load this skill when creating, editing, or reviewing speaker notes for any slide. Use when user mentions "speaker notes" or "presenter notes".
---

# Speaker Notes Skill

## Overview

This skill defines the structure and content conventions for speaker notes in the presentation. All speaker notes must follow this structure consistently.

## Required Structure

Every slide's speaker notes must follow this exact structure, in order:

### 1. Spoken text (before the `<hr/>`)

The first part of the speaker notes contains the text the speaker is intended to read out during the presentation. This should be written as natural, flowing prose — the words the speaker will actually say. It should:

- Be written in the first person or as a direct address to the audience
- Read naturally when spoken aloud
- Avoid jargon or abbreviations that would be awkward to say
- Capture the key narrative point(s) of the slide
- Include any transition phrase that bridges to the next slide
- **Never include code syntax, brackets, backticks, or technical notation** — these are impossible to read aloud naturally. If referencing a filename or path, use the name as written if it reads naturally (e.g. "AGENTS.md", "SKILL.md") rather than expanding it phonetically.
- **Avoid em dashes (—) in spoken text** — they create an awkward pause when read aloud. Use a full stop or "and" or "which" instead to create a natural spoken break.
- **Be concise and crisp** — every sentence should earn its place. Remove filler, hedging, and redundant phrasing. The spoken text should feel punchy and confident when delivered aloud.
- **Use contractions and spoken-word phrasing** — write the way a confident speaker naturally talks. Prefer "that's" over "that is", "it's" over "it is", "you're" over "you are", "doesn't" over "does not", "we're" over "we are", and so on. Formal written prose reads awkwardly when spoken aloud.

### 2. Horizontal rule

A single `<hr/>` element separates the spoken text from the supporting detail below.

### 3. Supporting bullet points (after the `<hr/>`)

After the `<hr/>`, include a `<ul>` list of bullet points covering additional key details about the slide that the speaker should be aware of but does not necessarily need to read verbatim. These may include:

- Clarifications or elaborations on slide content
- Common audience questions and suggested answers
- Caveats, edge cases, or nuances not shown on the slide
- Presenter cues (e.g. **click to show row** before a fragment appears)
- Diagnostic tips or background context

### 4. References (after the bullet points, if applicable)

If there are publicly available references where the audience or speaker can find additional detail relating to the slide, include them after the bullet points as a further `<ul>` list with anchor links. Only include references that are publicly accessible.

## HTML Template

```html
<aside class="notes">
    <p>{Spoken text the presenter reads aloud.}</p>
    <hr/>
    <ul>
        <li>{Key detail or presenter cue}</li>
        <li>{Key detail or presenter cue}</li>
    </ul>
    <ul>
        <li><a href="{url}">{Reference title}</a> — {one-line description}</li>
    </ul>
</aside>
```

## Rules

- **Spoken text always comes first** — before the `<hr/>`.
- **The `<hr/>` is mandatory** — it is the visual separator between what is spoken and what is supplementary.
- **References are optional** — only include them if publicly accessible URLs exist. Do not fabricate links.
- **Presenter cues** (e.g. `<strong>click to show row</strong>`) belong in the bullet points section, not in the spoken text.
- Do not place supporting bullet points or references before the `<hr/>`.
- Keep the spoken text concise — it should be readable in the time allocated to the slide.
