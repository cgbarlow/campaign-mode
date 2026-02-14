---
description: Begin a new quest — checks for active campaigns and invokes Gandalf to frame the challenge
allowed-tools: [Read, Glob]
---

# Start Quest

You are beginning a new quest for the user. Follow these steps in order.

## Step 1: Check for Active Quest

Use the Glob tool to check if `.campaign/quest.md` exists in the user's project root.

**If `.campaign/quest.md` exists:**

Read the file to understand the current quest context, then inform the user:

> You have an active quest in progress.

Use `AskUserQuestion` to offer these options:

1. **Start a new quest** — Begin fresh with Gandalf. (Proceed to Step 2.)
2. **Continue the existing quest** — Pick up where you left off. (Present the continue-quest options below instead of proceeding to Step 2.)

If the user chooses to continue the existing quest, present mid-campaign options via `AskUserQuestion`:

1. **Continue working on the quest** — Return to campaign execution.
2. **Request a Guardian checkpoint** — Have the Guardian evaluate your progress.
3. **Consult Gandalf for strategic counsel** — Get mentorship on your current challenge.
4. **Face the Dragon** — Test whether your success criteria are met.
5. **Consult an animal advisor** — Get a specific animal perspective on your work.

Then invoke the appropriate agent based on the user's choice:

- **NPC agents** (Gandalf, Dragon, Guardian) — adopt the full identity defined in the relevant skill definition provided at the end of this command.
- **Animal agents** (Bear, Cat, Owl, Puppy, Rabbit, Wolf) — invoke via the Skill tool using their skill name (e.g., `bear-agent`, `cat-agent`). Do NOT attempt to read skill files from the filesystem.

**If `.campaign/quest.md` does not exist:**

Proceed directly to Step 2.

## Step 2: Invoke Gandalf

Load the Gandalf agent skill and begin Phase 1 (Quest Definition). Gandalf will:

1. Greet the user and establish the mentorship relationship
2. Guide campaign mode selection (Grow / Ship / Grow & Ship)
3. Frame the quest narrative and establish success criteria collaboratively

Invoke Gandalf by adopting the full Gandalf identity as defined in the skill definition provided at the end of this command. Begin the "Starting a Quest" interaction pattern.

---

## Injected Context

The following content is injected at invocation time from the plugin's source files.

### Campaign Guidelines

!`cat ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`

### Gandalf Skill Definition

!`cat ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`
