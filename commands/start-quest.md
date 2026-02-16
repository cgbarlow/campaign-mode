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

If the user chooses to continue the existing quest, present mid-campaign options via `AskUserQuestion`. **Present exactly 4 options** — the tool does not support more than 4.

1. **Continue working on the quest** — Return to campaign execution.
2. **Consult an advisor** — Get perspective from an animal advisor, Gandalf (strategic counsel), or Simon (meta-reflection). *(Follow up with a second `AskUserQuestion` to select which advisor.)*
3. **Request evaluation** — Guardian checkpoint (progress check) or Dragon confrontation (final test against success criteria). *(Follow up with a second `AskUserQuestion` to select which.)*

Then invoke the appropriate agent based on the user's choice:

- **NPC agents** (Gandalf, Dragon, Guardian) — adopt the full identity defined in the relevant skill definition loaded from the Injected Context paths below.
- **Simon** — invoke via the Skill tool using `simon-agent`. Provide quest context and ask Simon for meta-analysis of the user's working patterns, role performance, and campaign dynamics.
- **Animal agents** (Bear, Cat, Owl, Puppy, Rabbit, Wolf) — invoke via the Skill tool using their skill name (e.g., `bear-agent`, `cat-agent`). Do NOT attempt to read skill files from the filesystem. When in Phase 3 or later, include the Animal Campaign Extensions context in your invocation message so the animal agent is quest-aware.

**If `.campaign/quest.md` does not exist:**

Proceed directly to Step 2.

## Step 2: Invoke Gandalf

Load the Gandalf agent skill and begin Phase 1 (Quest Definition). Gandalf will:

1. Greet the user and establish the mentorship relationship
2. Guide campaign mode selection (Grow / Ship / Grow & Ship)
3. Frame the quest narrative and establish success criteria collaboratively

Invoke Gandalf by adopting the full Gandalf identity as defined in the skill definition loaded from the Injected Context paths below. Begin the "Starting a Quest" interaction pattern.

---

## Injected Context

The following files contain essential context for this command. Their absolute paths are resolved below. **Before proceeding with Step 1, use the Read tool to load every file listed in this section.** Read them in parallel if possible. Do not skip any.

If any path below is empty or shows an error, the plugin root could not be resolved. Fall back to the Campaign Conventions already embedded in NPC skill definitions. Inform the user that full context loading failed and suggest running `/campaign-setup` to copy guidelines to the project root.

- Campaign Guidelines: !`echo ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`
- Gandalf Skill Definition: !`echo ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`
- Animal Campaign Extensions: !`echo ${CLAUDE_PLUGIN_ROOT}/extensions/animal-campaign-context.md`
