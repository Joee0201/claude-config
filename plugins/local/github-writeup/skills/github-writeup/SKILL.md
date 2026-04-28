---
name: github-writeup
description: This skill should be used when the user wants to "push to GitHub", "create a repo", "write a README", "document this for GitHub", "publish this", "generate a GitHub page", or wants GitHub documentation written for their code or files. Generates a polished preview page explaining what the project does, followed by the relevant code with context.
version: 1.0.0
allowed-tools: [Read, Glob, Grep, Bash]
---

# GitHub Write-Up Skill

Generates polished GitHub documentation for repos, files, and pushes. Always produces two sections in order: a **Preview Page** then the **Code/Files**.

## Workflow

### Step 1: Understand What's Being Published

Before writing anything, gather context:
- Read the files the user is pushing or referencing
- Check `git log --oneline -10` to understand recent changes
- Check `git diff HEAD~1` or staged diff if relevant
- Identify the project type (CLI tool, library, config, script, etc.)

### Step 2: Generate the Preview Page

Write a `## Preview` section that a visitor would see on GitHub. It must include:

1. **One-line tagline** — what it does, in plain English (no jargon)
2. **What it is** — 2-3 sentences explaining the purpose and who it's for
3. **What it does** — bullet list of key features or capabilities (3-6 bullets max)
4. **How to use it** — minimal getting-started steps (install, configure, run)
5. **Why it exists** — one sentence on the motivation or problem it solves

Keep it human. Avoid buzzwords. Write as if explaining to a smart friend who hasn't seen the code.

### Step 3: Show the Code

After the preview, show the relevant code or files with:
- Proper fenced code blocks with language tags (` ```python `, ` ```json `, etc.)
- File path as a header above each block
- Only include files relevant to what's being pushed — don't dump everything

### Step 4: Offer to Write the README

Ask if the user wants to save this as a `README.md` in the repo root and push it. If yes:
- Write the README using the preview content as the body
- Add a License section if none exists
- Commit with message: `docs: add README`

## Output Format

```
---

## Preview

**[one-line tagline]**

[2-3 sentence description]

**What it does:**
- bullet
- bullet
- bullet

**Getting started:**
[minimal steps]

**Why:** [one sentence motivation]

---

## Files

### path/to/file.ext
\`\`\`lang
[file contents]
\`\`\`

---
```

## Rules

- Never write generic filler like "This repo contains..." or "Welcome to..."
- If the project has no clear purpose yet, say so and ask the user to describe it
- Keep the preview scannable — someone should understand the project in 30 seconds
- Don't invent features; only document what's actually in the code
