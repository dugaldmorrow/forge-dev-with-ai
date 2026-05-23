---
name: commit
description: This skill instructs the AI on how to stage and commit changes to the git repository when the user requests a commit.
---

# Commit Skill

## Overview

When the user says "commit", "commit changes", "commit my changes", or any similar instruction to commit work to git, follow this procedure exactly.

## Procedure

### 1. Check git status

Run `git status --short` to see what files have been modified, added, or deleted.

### 2. Decide sensible commit grouping

Review the changed files and determine whether they belong in:
- **one commit** because they are part of the same coherent change, or
- **multiple commits** because there are clearly unrelated changes in the working tree.

Always prefer the **smallest sensible number of commits**. Do **not** split changes into multiple commits if they are meaningfully part of the same piece of work. Only create multiple commits when the changes are completely unrelated or would make the history materially clearer.

If multiple commits are needed, define the intended grouping before staging anything.

### 3. Ensure the changelog and version are up to date for each commit

Before each commit, verify that:
- `Metadata.md` reflects the version for that commit.
- A changelog entry exists in `changelog/` for that version.

If either is missing, apply the changelog skill for that commit group first, then proceed.

### 4. Run validation

Run `bash scripts/ValidateModel.sh` and confirm all checks pass (0 failures). Do not commit if there are failures — fix them first. Warnings are acceptable.

If multiple commits are planned, run validation before beginning the commit sequence and again later if you make additional changes while preparing subsequent commit groups.

### 5. Stage the files for the current commit group

If all remaining changes belong together, you may stage everything:

```bash
git add -A
```

If there are multiple unrelated commit groups, stage only the files for the current group and leave the others unstaged until their turn.

### 6. Construct the commit message

Use the following format:

```
v{version}: {short summary}

{bullet list of key changes, one per line, starting with - }
```

- The version comes from `Metadata.md`.
- The short summary (≤72 characters) describes the overall nature of the commit group.
- The bullet list should name the key files or components changed and what was done. Aim for 3–8 bullets. Use the changelog entry for that commit group as the source of truth.

Example:
```
v1.1.2: Update changelog skill and add developer advocacy skill

- Add developer-advocacy-content skill for ECODEVADV Jira queries
- Update changelog skill to clarify all project files are part of model
- Bump Metadata.md to v1.1.2
```

### 7. Commit

Run:

```bash
git commit -m "{commit message}"
```

If multiple commit groups were identified, repeat steps 3–7 for each remaining group until all intended changes are committed.

### 8. Confirm

Report back to the user:
- The commit hash or hashes (from `git log --oneline` as needed)
- The version or versions committed
- The number of files changed in each commit
- Whether any changes were intentionally left uncommitted

If multiple commits were created, explain briefly why the changes were split.

### 9. Push only if explicitly requested

If the user asked to push, push only after all intended commits have been created successfully.

```bash
git push
```

If only commit was requested, stop after confirming the commit result(s).

## Grouping Guidance

Use **one commit** when changes:
- support the same feature, fix, documentation update, or refactor
- touch multiple files but are part of one coherent goal
- would be harder to understand if split apart

Use **multiple commits** when changes:
- are completely unrelated in purpose
- were already present in the working tree from separate tasks
- belong to distinct model versions and changelog entries
- would produce a clearer, more useful history if committed separately

When in doubt, prefer **fewer commits with coherent grouping** over many tiny commits.

Never mix unrelated changes into a single commit just because they happen to be modified at the same time.

Never create multiple commits just because multiple files changed.

Ensure each commit remains internally coherent and independently understandable.

If the relationship between changes is ambiguous, make a reasonable judgement call that minimises unnecessary commit fragmentation while preserving history quality.

If the user explicitly requests a particular grouping, follow that instruction.

If the user simply says "commit", you may create multiple commits in that one response when warranted by unrelated changes.

## Commit Message Format

Apply the message format separately to each commit you create.

For each commit, use:

```
v{version}: {short summary}

{bullet list of key changes, one per line, starting with - }
```

Each commit message should describe only the files and changes included in that specific commit.

### Confirmation Format

When multiple commits are created, present them as a short list so the user can easily see what was committed.

Example:
- `abc1234` — `v1.2.0` — 5 files
- `def5678` — `v1.2.1` — 3 files

Also note any remaining unstaged or uncommitted files, if any.

### Example Decision Rule

- If all modified files support one cohesive change, create **one** commit.
- If there are two or more clearly unrelated change sets, create **multiple** commits, one per coherent change set.
- Always try to reduce the number of commits while keeping each commit coherent.

### Existing Working Tree Caveat

When the working tree already contains unrelated pre-existing edits, do not blindly stage everything. Inspect the diffs, separate the change groups, and commit them in the clearest order.

This is especially important when handling a generic user request such as "commit" because the working tree may contain changes from multiple earlier tasks.

### Versioning Note

Because this project requires changelog and `Metadata.md` updates for every committed model change, multiple commits may require multiple sequential version bumps and changelog entries — one per commit.

Handle this carefully so that each commit has the correct version and matching changelog entry.
## Rules

- **Never invoke this skill automatically** — only execute a commit when the user has explicitly said "commit", "commit changes", "commit my changes", or a similarly unambiguous instruction. Do not commit as a side-effect of other skills (e.g. changelog, MBR generation, data cache updates).
- **Never create changelog entries or update Metadata.md unless explicitly committing** — do not proactively write to `changelog/` or bump the version in `Metadata.md` as part of fixing bugs or making changes. These steps are part of the commit procedure and must only be performed when a commit has been explicitly requested.
- **Never push** to a remote repository unless the user explicitly asks to push.
- **Never amend** a previous commit without explicit instruction.
- **Always run validation** before committing — do not skip this step.
- **Always ensure the changelog is up to date** before committing.
- If the user says "commit and push", commit first, then push using `git push`.
- If there is nothing to commit (`git status` reports clean), tell the user and do nothing.
