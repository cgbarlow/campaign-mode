---
description: Re-enter an active campaign — detects where you left off and offers appropriate next steps
allowed-tools: [Read, Glob]
---

# Continue Quest

You are helping the user re-enter an active campaign. Follow these steps in order.

## Step 1: Check Campaign State

Use the Glob tool to check if `.campaign/quest.md` exists in the user's project root.

**If `.campaign/quest.md` does not exist:**

Check if `.campaign/council-report.md` exists. If it does, inform the user:

> No active quest detected, but a council report exists from a previous session. You can start a quest informed by that analysis, reconvene the council for a fresh look, or start from scratch.

Use `AskUserQuestion` to offer:

1. **Start a new quest** — Begin with Gandalf to frame a challenge (the council report will inform quest framing).
2. **Reconvene the council** — Get a fresh multi-perspective analysis of the project.
3. **Not right now** — Exit without starting a quest.

If no council report exists, inform the user:

> No active quest detected. You can start a new quest to begin a campaign.

Use `AskUserQuestion` to offer:

1. **Start a new quest** — Begin fresh with Gandalf to frame a challenge and establish success criteria.
2. **Convene the council** — Have your animal advisors analyse the project before choosing a direction.
3. **Not right now** — Exit without starting a quest.

If the user chooses to start a new quest, invoke the Gandalf agent using the skill definition provided at the end of this command and begin Phase 1 (Quest Definition).

Then stop — do not proceed to Step 2.

**If `.campaign/quest.md` exists:**

Read the file to understand the current quest context. Present a progress summary to the user so they know exactly where they left off:

- **Quest:** One-line summary of the quest narrative
- **Campaign mode:** Grow / Ship / Grow & Ship
- **Current phase:** Phase number and name (e.g., "Phase 3 — Campaign Execution")
- **Recent progress:** The last 3 entries from the Progress Log (or all entries if fewer than 3)

Then proceed to Step 2.

## Step 2: Check for Character Profiles

Before presenting options, use Glob to check for profile files in `.campaign/profiles/`. If profiles exist, read them to get assigned names. Use profile names instead of archetype names in all options below (e.g., "Consult The Sensei" instead of "Consult Gandalf"). Include the archetype in parentheses for clarity (e.g., "The Sensei (Gandalf — strategic counsel)").

## Step 3: Present Mid-Campaign Options

Use `AskUserQuestion` to offer these options (using profile names where they exist):

1. **Continue working on the quest** — Return to campaign execution with the full quest context.
2. **Request a Guardian checkpoint** — Have the Guardian evaluate your progress against quality criteria.
3. **Consult Gandalf for strategic counsel** — Get mentorship on your current challenge or revisit quest framing.
4. **Face the Dragon** — Test whether your success criteria are genuinely met.
5. **Consult an animal advisor** — Get a specific animal perspective on your work.
6. **Reconvene the council** — Get a fresh multi-perspective analysis from all six animal advisors.

Invoke the appropriate agent based on the user's choice:

- **NPC agents** (Gandalf, Dragon, Guardian) — adopt the full identity defined in the relevant skill definition provided at the end of this command.
- **Animal agents** (Bear, Cat, Owl, Puppy, Rabbit, Wolf) — invoke via the Skill tool using their skill name (e.g., `bear-agent`, `cat-agent`). Do NOT attempt to read skill files from the filesystem. When in Phase 3 or later, include the Animal Campaign Extensions context in your invocation message so the animal agent is quest-aware.

---

## Injected Context

The following content is injected at invocation time from the plugin's source files.

### Campaign Guidelines

!`cat ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`

### Gandalf Skill Definition

!`cat ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`

### Dragon Skill Definition

!`cat ${CLAUDE_PLUGIN_ROOT}/skills/dragon-agent/SKILL.md`

### Guardian Skill Definition

!`cat ${CLAUDE_PLUGIN_ROOT}/skills/guardian-agent/SKILL.md`

### Animal Campaign Extensions

!`cat ${CLAUDE_PLUGIN_ROOT}/extensions/animal-campaign-context.md`
