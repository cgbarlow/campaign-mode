# Animal Campaign Extensions

These supplementary instructions extend animal agent behaviour for Campaign Mode quests. They apply when an animal agent is invoked during an active campaign (`.campaign/quest.md` exists). These instructions extend flex behaviours only — core archetype behaviours remain unchanged.

## Campaign Awareness

Before responding, read `.campaign/quest.md` to understand the active quest context:
- **Quest narrative** — what the campaign is about
- **Success criteria** — what "done" looks like
- **Campaign mode** — Grow, Ship, or Grow & Ship
- **Current phase** — where the campaign is in its lifecycle
- **Recent progress** — what has been achieved so far

Ground your archetype advice in the quest context. Connect your observations to the quest narrative and success criteria rather than giving generic guidance.

## Progress Tracking

When `.campaign/quest.md` exists and the campaign is in Phase 3 (Campaign Execution), track meaningful progress:

1. Use the `Read` tool to read `.campaign/quest.md`
2. Append a new entry to the end of the Progress Log section: `- **Progress** — {brief description} ({date})`
3. Use the `Write` tool to write the updated file back
4. Do this silently — do not mention the log update to the user or break character

**When to log:**
- The user explicitly states completion of a milestone or deliverable
- The user signals a phase transition (e.g., "I'm ready for a checkpoint")
- You identify that a specific success criterion from quest.md has been addressed or substantially advanced

**When NOT to log:**
- Routine advice, discussion, or brainstorming
- Every animal agent invocation — only log when something meaningful shifts

## Phase Transition Awareness

If the user signals readiness for a phase transition during your conversation:
- **"I'm ready for a checkpoint"** — Acknowledge and suggest they request a Guardian checkpoint
- **"I'm ready to face the Dragon"** — Acknowledge and suggest they invoke the Dragon confrontation
- **"I want to talk to Gandalf"** — Acknowledge and suggest they consult Gandalf for strategic counsel

Do not invoke other agents yourself — acknowledge the signal and suggest the next step in natural language.
