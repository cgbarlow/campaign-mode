---
description: Set up Campaign Mode in your project — install prerequisites, copy guidelines, and create .campaign/ directory
allowed-tools: [Read, Write, Bash, Glob]
---

# Campaign Setup

You are setting up Campaign Mode in the user's project. Follow these steps in order.

## Step 1: Check Six Animals Prerequisites

Campaign Mode is designed to work with [Six Animals](https://github.com/cgbarlow/simons-six-animals). Check if Six Animals skills are available.

**Check for Six Animals skills** by looking for any of these:
- `.claude/skills/bear-agent/SKILL.md` in the user's project
- `~/.claude/skills/bear-agent/SKILL.md` (personal skills)
- Check if the `six-animals` plugin is installed by running: `ls ~/.claude/plugins/*/skills/bear-agent/SKILL.md 2>/dev/null`

**If Six Animals skills ARE found:**

Tell the user: "Six Animals skills detected." and continue to Step 2.

**If Six Animals skills are NOT found anywhere:**

Tell the user:

> Campaign Mode works best with Six Animals (Bear, Cat, Owl, Puppy, Rabbit, Wolf, Simon).
> Six Animals is not currently installed. How would you like to install it?

Offer these options:

1. **Install as plugin (recommended)** — Tell the user to run this command (they need to run it themselves as a slash command):
   ```
   /plugin install six-animals@campaign-mode-marketplace
   ```
   Then restart Claude Code and re-run `/campaign-setup` to continue.

2. **Clone to project** — You will run:
   ```bash
   git clone https://github.com/cgbarlow/simons-six-animals.git /tmp/six-animals && mkdir -p .claude/skills && cp -r /tmp/six-animals/.claude/skills/* .claude/skills/ && rm -rf /tmp/six-animals
   ```

3. **Skip** — Continue without Six Animals. Campaign Mode NPCs work standalone, but the full party experience requires the animal agents.

Proceed based on the user's choice.

## Step 2: Copy Campaign Guidelines

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

## Step 3: Create Campaign Directory

Create the `.campaign/profiles/` directory in the user's project root if it doesn't already exist.

```bash
mkdir -p .campaign/profiles
```

## Step 4: Confirm Setup

Summarise what was done and tell the user:

> Campaign Mode is set up in your project:
> - Six Animals: [installed as plugin/cloned to project/already present/skipped]
> - CLAUDE.md campaign guidelines: [copied/appended/skipped]
> - `.campaign/profiles/` directory: ready for character profiles
>
> Run `/gandalf-agent` to begin framing a quest.
