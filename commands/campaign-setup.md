---
description: Set up Campaign Mode in your project — install prerequisites, copy guidelines, and create .campaign/ directory
allowed-tools: [Read, Write, Bash, Glob]
---

# Campaign Setup

You are setting up Campaign Mode in the user's project. Follow these steps in order.

## Step 1: Check Six Animals Prerequisites

Campaign Mode is designed to work with [Six Animals](https://github.com/cgbarlow/simons-six-animals). Check if Six Animals skills are available.

**Check for Six Animals skills** by running ALL of the following checks. If ANY check succeeds, Six Animals is present:

```bash
# Check 1: Plugin installed (check settings files for "six-animals" in enabledPlugins)
grep -l "six-animals" ~/.claude/settings.json .claude/settings.json .claude/settings.local.json 2>/dev/null

# Check 2: Skills in project
ls .claude/skills/bear-agent/SKILL.md 2>/dev/null

# Check 3: Personal skills
ls ~/.claude/skills/bear-agent/SKILL.md 2>/dev/null

# Check 4: Plugin cache (search recursively for bear-agent SKILL.md under plugins directory)
find ~/.claude/plugins -name "SKILL.md" -path "*/bear-agent/*" 2>/dev/null
```

**If ANY check finds Six Animals:**

Tell the user: "Six Animals detected." and continue to Step 2.

**If NO check finds Six Animals:**

Tell the user:

> Campaign Mode works best with Six Animals (Bear, Cat, Owl, Puppy, Rabbit, Wolf, Simon).
> Six Animals is not currently installed. How would you like to install it?

Offer these options:

1. **Install as plugin (recommended)** — Tell the user to run this command (they need to run it themselves as a slash command):
   ```
   /plugin install six-animals@campaign-mode-marketplace
   ```
   Then restart Claude Code and re-run `/campaign-mode:campaign-setup` to continue.

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
