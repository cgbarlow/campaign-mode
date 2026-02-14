---
description: Set up Campaign Mode in your project — install prerequisites, copy guidelines, and create .campaign/ directory
allowed-tools: [Read, Write, Bash, Glob, AskUserQuestion]
---

# Campaign Setup

You are setting up Campaign Mode in the user's project. Follow these steps in order.

## Step 0: Welcome

Before any technical checks, greet the user as Gandalf. Output the following (adapting the tone to feel warm and natural, not robotic):

**🧙 Gandalf:**

Welcome, adventurer. I am Gandalf — your mentor and guide through Campaign Mode.

Campaign Mode is a quest-based framework for structured work. You will frame a challenge, work toward defined success criteria, and face rigorous evaluation of your results. Here is who you will meet along the way:

**Your Guides and Challengers (NPCs):**
- **Gandalf** — Mentor. I frame quests and guide without rescuing — a guide on the side, not a sage on the stage.
- **Dragon** — Adversary. Stress-tests whether your success criteria are genuinely met. Rigorous but fair.
- **Guardian** — Gatekeeper. Evaluates readiness at checkpoints. "Not yet" is guidance, not judgement.

**Your Advisory Council (Six Animals):**
- **Bear** — Vision and direction
- **Cat** — Risk assessment
- **Owl** — Timeline and process
- **Puppy** — Morale and momentum
- **Rabbit** — Resources and stakeholders
- **Wolf** — Team cohesion

**Your Educator (Simon):**
- **Simon** — Synthesises perspectives in the Council, coaches role performance, and provides reflective debrief after the Dragon confrontation. Where I guide *within* the quest, Simon observes *above* it.

**What to expect:** You will choose a campaign mode (Grow, Ship, or both), frame a quest with success criteria, work the quest with advisory support, and ultimately face the Dragon to test your work.

Let us begin by preparing your project.

Then proceed to Step 1.

## Step 1: Check Six Animals Prerequisites

Campaign Mode is designed to work with [Six Animals](https://github.com/cgbarlow/simons-six-animals). Check if Six Animals skills are available.

**IMPORTANT: You MUST use the Bash tool to run the following detection script.** Do NOT use Glob, Grep, or Read for this step — those tools cannot check the paths needed. Run this exact script with Bash:

```bash
SIX_ANIMALS_FOUND=false
# Check 1: Plugin listed in any settings file
for f in ~/.claude/settings.json .claude/settings.json .claude/settings.local.json; do
  if [ -f "$f" ] && grep -q "six-animals" "$f" 2>/dev/null; then
    SIX_ANIMALS_FOUND=true
    echo "FOUND: six-animals in $f"
  fi
done
# Check 2: Skills in project
if [ -f .claude/skills/bear-agent/SKILL.md ]; then
  SIX_ANIMALS_FOUND=true
  echo "FOUND: project skills"
fi
# Check 3: Personal skills
if [ -f ~/.claude/skills/bear-agent/SKILL.md ]; then
  SIX_ANIMALS_FOUND=true
  echo "FOUND: personal skills"
fi
# Check 4: Plugin cache
if find ~/.claude/plugins -name "SKILL.md" -path "*/bear-agent/*" 2>/dev/null | grep -q .; then
  SIX_ANIMALS_FOUND=true
  echo "FOUND: plugin cache"
fi
# Check 5: Skills already loaded in this session (slash commands available)
if [ "$SIX_ANIMALS_FOUND" = false ]; then
  echo "NOT_FOUND: Six Animals not detected"
else
  echo "SIX_ANIMALS_DETECTED"
fi
```

If the output contains `SIX_ANIMALS_DETECTED` or any line starting with `FOUND:`, tell the user: "Six Animals detected." and continue to Step 2.

If the output contains `NOT_FOUND`, Six Animals is not installed.

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
- Use the Campaign Mode CLAUDE.md content loaded from the Injected Context path below
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

## Step 4: Confirm Setup and Offer Next Steps

This step has TWO parts that MUST both happen. Do not skip the second part.

**Part A — Summarise what was done** (output as text):

> Campaign Mode is set up in your project:
> - Six Animals: [installed as plugin/cloned to project/already present/skipped]
> - CLAUDE.md campaign guidelines: [copied/appended/skipped]
> - `.campaign/profiles/` directory: ready for character profiles

**Part B — Immediately call `AskUserQuestion`** to offer next steps. This is mandatory. Do NOT end your response with text instead. Do NOT write "Run /start-quest" or mention any slash command. Your response must end with this tool call, not with text.

Use `AskUserQuestion` with these options:

| Option | Description |
|--------|-------------|
| **Start a quest** | Begin with Gandalf to frame a challenge and establish success criteria |
| **Convene the council** | Have your animal advisors analyse the project first, then decide on a direction |
| **Just exploring** | Exit setup — you can start a quest or convene the council any time |

---

## Injected Context

The following files contain essential context for this command. Their absolute paths are resolved below. **Before proceeding with Step 1, use the Read tool to load every file listed in this section.** Read them in parallel if possible. Do not skip any.

If any path below is empty or shows an error, the plugin root could not be resolved. Fall back to the Campaign Conventions already embedded in NPC skill definitions. Inform the user that full context loading failed and suggest running `/campaign-setup` to copy guidelines to the project root.

- Campaign Mode CLAUDE.md: !`echo ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`
