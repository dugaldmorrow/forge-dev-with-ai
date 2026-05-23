
---
name: changelog
description: This skill instructs the LLM on how to log changes to the model in order to keep a persistant record of changes over time.
---

# Instructions

## Overview

The model includes all files in this project — markdown documentation, SVG diagrams, scripts, data caches, assessments, reports, and agent skills. Any change to any file in the project constitutes a change to the model and must be recorded in the changelog.

Every time changes are made to this model, you must:

1. Determine the current version from `Metadata.md`.
2. Increment the version following semantic versioning rules (see below).
3. Write a changelog entry to `changelog/{version}-changelog.md`.
4. Update `Metadata.md` with the new version and today's date.

You must do this **at the end of every session** in which changes were made, or **immediately after completing a significant change** if instructed. Never skip the changelog step.

## Semantic Versioning Rules

The version in `Metadata.md` follows [Semantic Versioning](https://semver.org/): `MAJOR.MINOR.PATCH`.

| Change type | Version increment | Examples |
|---|---|---|
| **PATCH** | `x.y.Z+1` | Data cache updates, typo fixes, minor text edits, adding rows to existing tables |
| **MINOR** | `x.Y+1.0` | New files added, new sections added to existing files, new validation checks, new metrics, new SVGs, new assessments |
| **MAJOR** | `X+1.0.0` | Structural changes to the model, changes to SVG conventions, changes to the rubric, removal of components |

When multiple changes of different types occur in one session, use the **highest** applicable increment.

## Changelog File Format

Create the file at: `changelog/{new-version}-changelog.md`

Use the following template:

```markdown
# Changelog: {new-version}

**Date:** {DD-Mon-YYYY, HH:MM AEST}  
**Previous version:** {old-version}  
**Change type:** MAJOR | MINOR | PATCH

## Summary

{One paragraph summarising the overall nature of the changes in this version.}

## Changes

### {Category} (e.g. Documentation, Scripts, Data, SVG, Assessments, Skills)

- **{filename or component}**: {Description of what changed and why.}
- ...

### {Another Category}

- ...

## Validation

`bash scripts/ValidateModel.sh` — {N} passed | 0 failed | 0 warnings
```

## Rules

- **Always** increment the version — never reuse an existing version number.
- **Always** update `Metadata.md` with the new version and the current date in the format `D-Mon-YYYY, HH:MM AEST`.
- Group changes by logical category (Documentation, Scripts, Data, SVG, Assessments, Skills, etc.).
- Be specific: name each file changed and describe what changed, not just that a change was made.
- If validation was run, record the final result. If not, omit the Validation section.
- The changelog file is append-only — never edit a previously created changelog file.
- If more than one session's worth of changes has accumulated without a changelog entry, write a single entry covering all changes, using the highest applicable version increment.
