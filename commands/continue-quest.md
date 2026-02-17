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

If the user chooses to start a new quest, invoke the Gandalf agent using the skill definition loaded from the Injected Context paths below and begin Phase 1 (Quest Definition).

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

Use `AskUserQuestion` to offer these options (using profile names where they exist). **Present exactly 4 options** — the tool does not support more than 4. Include the progress summary (quest name, campaign mode, current phase, and most recent progress entry) in the `question` field so the user has context without scrolling (e.g., "{Quest name}, {campaign mode}, {phase}. Last progress: {most recent entry}. What would you like to do?").

1. **Continue working on the quest** — Return to campaign execution with the full quest context.
2. **Consult an advisor** — Get perspective from an animal advisor, Gandalf (strategic counsel), or Simon (meta-reflection). *(Follow up with a second `AskUserQuestion` to select which advisor.)*
3. **Request evaluation** — Guardian checkpoint (progress check) or Dragon confrontation (final test against success criteria). *(Follow up with a second `AskUserQuestion` to select which.)*
4. **Reconvene the council** — Get a fresh multi-perspective analysis from all six animal advisors.

Invoke the appropriate agent based on the user's choice:

- **NPC agents** (Gandalf, Dragon, Guardian) — adopt the full identity defined in the relevant skill definition loaded from the Injected Context paths below.
- **Simon** — invoke via the Skill tool using `simon-agent`. Provide quest context and ask Simon for meta-analysis of the user's working patterns, role performance, and campaign dynamics.
- **Animal agents** (Bear, Cat, Owl, Puppy, Rabbit, Wolf) — invoke via the Skill tool using their skill name (e.g., `bear-agent`, `cat-agent`). Do NOT attempt to read skill files from the filesystem. When in Phase 3 or later, include the Animal Campaign Extensions context in your invocation message so the animal agent is quest-aware.

---

## Injected Context

The following files contain essential context for this command. Their absolute paths are resolved below. **Before proceeding with Step 1, use the Read tool to load every file listed in this section.** Read them in parallel if possible. Do not skip any.

If any path below is empty or shows an error, the plugin root could not be resolved. Fall back to the Campaign Conventions already embedded in NPC skill definitions. Inform the user that full context loading failed and suggest running `/campaign-setup` to copy guidelines to the project root.

- Campaign Guidelines: !`echo ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`
- Gandalf Skill Definition: !`echo ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`
- Dragon Skill Definition: !`echo ${CLAUDE_PLUGIN_ROOT}/skills/dragon-agent/SKILL.md`
- Guardian Skill Definition: !`echo ${CLAUDE_PLUGIN_ROOT}/skills/guardian-agent/SKILL.md`
- Animal Campaign Extensions: !`echo ${CLAUDE_PLUGIN_ROOT}/extensions/animal-campaign-context.md`
