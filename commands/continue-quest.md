---
description: Re-enter an active campaign — detects where you left off and offers appropriate next steps
allowed-tools: [Read, Glob]
---

# Continue Quest

You are helping the user re-enter an active campaign. Follow these steps in order.

## Step 1: Check Campaign State

Use the Glob tool to check if `.campaign/quest.md` exists in the user's project root.

**If `.campaign/quest.md` does not exist:**

Inform the user:

> No active quest detected. You can start a new quest to begin a campaign.

Use `AskUserQuestion` to offer:

1. **Start a new quest** — Begin fresh with Gandalf to frame a challenge and establish success criteria.
2. **Not right now** — Exit without starting a quest.

If the user chooses to start a new quest, invoke the Gandalf agent by loading the skill from `skills/gandalf-agent/SKILL.md` and beginning Phase 1 (Quest Definition).

Then stop — do not proceed to Step 2.

**If `.campaign/quest.md` exists:**

Read the file to understand the current quest context. Present a progress summary to the user so they know exactly where they left off:

- **Quest:** One-line summary of the quest narrative
- **Campaign mode:** Grow / Ship / Grow & Ship
- **Current phase:** Phase number and name (e.g., "Phase 3 — Campaign Execution")
- **Recent progress:** The last 3 entries from the Progress Log (or all entries if fewer than 3)

Then proceed to Step 2.

## Step 2: Present Mid-Campaign Options

Use `AskUserQuestion` to offer these options:

1. **Continue working on the quest** — Return to campaign execution with the full quest context.
2. **Request a Guardian checkpoint** — Have the Guardian evaluate your progress against quality criteria.
3. **Consult Gandalf for strategic counsel** — Get mentorship on your current challenge or revisit quest framing.
4. **Face the Dragon** — Test whether your success criteria are genuinely met.
5. **Consult an animal advisor** — Get a specific animal perspective on your work.

Invoke the appropriate agent based on the user's choice. When invoking an agent, load their skill from `skills/{agent}/SKILL.md` and adopt the full identity defined in the skill file.
