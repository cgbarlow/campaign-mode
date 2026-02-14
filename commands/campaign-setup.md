---
description: Set up Campaign Mode in your project — copy guidelines and create .campaign/ directory
allowed-tools: [Read, Write, Bash, Glob]
---

# Campaign Setup

You are setting up Campaign Mode in the user's project. Follow these steps:

## Step 1: Copy Campaign Guidelines

Check if a CLAUDE.md file exists in the user's project root.

**If no CLAUDE.md exists:**
- Read the Campaign Mode CLAUDE.md from this plugin's root directory
- Write it to the user's project root as CLAUDE.md

**If CLAUDE.md already exists:**
- Inform the user: "Found an existing CLAUDE.md in your project."
- Ask the user to choose:
  - **Append** — Add campaign guidelines to the end of the existing file (separated by a blank line and `---`)
  - **Replace** — Overwrite with campaign guidelines
  - **Skip** — Leave CLAUDE.md unchanged
- Proceed based on their choice

## Step 2: Create Campaign Directory

Create the `.campaign/profiles/` directory in the user's project root if it doesn't already exist.

```bash
mkdir -p .campaign/profiles
```

## Step 3: Confirm Setup

Tell the user:

> Campaign Mode is set up in your project:
> - CLAUDE.md campaign guidelines [copied/appended/skipped]
> - `.campaign/profiles/` directory ready for character profiles
>
> Run `/gandalf-agent` to begin framing a quest.
