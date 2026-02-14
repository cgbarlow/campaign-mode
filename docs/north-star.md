# Campaign Mode - North Star

## What Is Campaign Mode?

Campaign Mode is a **quest-based extension** for the [Six Animals](https://github.com/cgbarlow/six-animals) team collaboration framework. It transforms the six animal archetypes from standalone advisory roles into an **active party of collaborators** who work together on structured quests, guided and challenged by a cast of NPC (non-player character) agents.

Where Six Animals answers *"how should we work together?"*, Campaign Mode answers *"what are we working toward, and what stands in our way?"*

## Why Does This Exist?

### The Problem Six Animals Solves
Six Animals provides psychologically-grounded team roles (Bear, Cat, Owl, Puppy, Rabbit, Wolf) that reduce group friction, create psychological safety, and accelerate team formation. Simon acts as an educator/supervisor observing from the side.

### The Gap Campaign Mode Fills
Six Animals gives you **roles**. Campaign Mode gives those roles **purpose, structure, and stakes**. It provides:

- **Direction** - A quest framework that channels the animals' collaborative energy toward defined goals
- **Tension** - An adversarial Dragon agent that stress-tests whether the team has truly addressed their challenge
- **Gatekeeping** - A Guardian agent that enforces quality thresholds before the team can progress, preventing the "just push through" anti-pattern common in AI-assisted workflows
- **Mentorship** - A Gandalf agent that coaches the party's performance and helps them grow through the quest

### The Broader Value Proposition
*(From Rachael's insight)* Six Animals doesn't tell you who you are - it gives tools to communicate, suggests you can learn new behaviours, encourages giving space to others, and validates different ways of thinking. Campaign Mode extends this by giving those behaviours a **narrative container** - a structured journey where growth happens through doing, not just reflecting.

## The User as Protagonist

Campaign Mode has 10 AI agents — but the human is the protagonist. The user is the **decision-maker** who drives the quest, invokes agents, produces work, and faces NPCs. Every agent exists to serve the user's quest; none of them drive it.

This is grounded in Self Determination Theory's autonomy principle: the user is an agent with autonomy, not a passive recipient of AI-generated plans. The user:

- **Drives the quest** — chooses the challenge, shapes the success criteria, produces the work
- **Invokes agents** — decides which animal perspectives to consult and when
- **Faces NPCs** — presents work to the Guardian, confronts the Dragon, accepts or reshapes Gandalf's framing
- **Chooses their mode** — selects how they want to approach the campaign (Grow, Ship, or Grow & Ship)

## Campaign Mode Selection

Users approach campaigns with different priorities. Mode selection gives the user agency over their experience before the campaign begins:

| Mode | Priority | Framing |
|------|----------|---------|
| **Grow** | Self-discovery, reflection, transformation | "What will you learn? Who will you become?" |
| **Ship** | Deliverables, efficiency, blind-spot coverage | "What will you deliver? What does done look like?" |
| **Grow & Ship** (Default) | Both learning and delivery | "What will you learn AND deliver?" |

Mode selection happens during Phase 1 (Quest Definition) and tunes all NPC behaviour for the duration of the campaign. See [ADR-CM-005](adrs/ADR-CM-005-Campaign-Mode-Selection.md) for the full decision record.

## Core Architecture

### The Party (Six Animals - Shared Context)
The six animal agents operate as **party members** with shared context, each contributing their archetype's strengths:

| Animal | Campaign Role |
|--------|--------------|
| **Bear** | Vision and direction for the quest |
| **Cat** | Risk assessment and scope management |
| **Owl** | Timeline, process, and progress tracking |
| **Puppy** | Morale, momentum, and opportunity spotting |
| **Rabbit** | Resource identification and stakeholder facilitation |
| **Wolf** | Team cohesion and balanced participation |

### The NPCs (Campaign Mode - Isolated Context)
Three NPC agents operate **outside the party's shared context** to maintain objectivity and prevent the AI from gaming the system:

| NPC | Role | Analog |
|-----|------|--------|
| **Gandalf** | Mentor - frames the quest, defines success criteria, and mentors the party without rescuing them (guide on the side, not sage on the stage) | Quest-giver / Mentor archetype |
| **Dragon** | Adversary - operates at maximum context isolation to test success criteria adversarially but fairly, evaluating the work product alone without access to party reasoning | Final boss / Acceptance test |
| **Guardian** | Gatekeeper - provides three gate decisions (approve, block with feedback, conditional approval) to control progression based on deliverable quality, not intent | Stage gate / Quality gate |

### The Supervisor (Simon - Meta Layer)
Simon remains the **educator and meta-analyst**, operating above the quest narrative:
- Debriefs after encounters and provides learning insights
- Coaches role performance across both animals and NPCs
- Shows players "behind the curtain" - the pedagogical and psychological dynamics at work
- Optionally takes on GM (Game Master) responsibilities when quest mode is active

## How It Works (Envisioned Flow)

1. **Quest Definition** - You choose your campaign mode (Grow / Ship / Grow & Ship). Gandalf frames the challenge and establishes success criteria.
2. **Character Setup** - Animals optionally adopt characterisations/profiles (encouraged in Grow mode, skipped in Ship mode)
3. **Campaign Execution** - You work through the quest, invoking animal agents for their archetype strengths
4. **Guardian Checkpoints** - At key stages, you invoke the Guardian to evaluate whether you're ready to progress
5. **Dragon Confrontation** - You invoke the Dragon to test whether all success criteria have been genuinely met
6. **Simon Debrief** - Simon provides feedback on the journey (full reflection in Grow mode, brief retrospective in Ship mode)

## Design Principles

1. **User Agency First** - The user is the protagonist. Every design choice should increase user agency, not reduce it. Mode selection, quest shaping, agent invocation — the user drives. This aligns with SDT's autonomy principle.
2. **Context Isolation** - NPCs must NOT share context with party members. The Guardian and Dragon need independent judgement, not information contaminated by the party's reasoning. Three isolation levels are defined: advisory (Gandalf), independent (Guardian), maximum (Dragon). In v1, isolation is enforced by instruction and sub-agent invocation; future plugin/API evolution may provide hard architectural enforcement. *(See [ADR-CM-003](adrs/ADR-CM-003-NPC-Context-Isolation.md))*
3. **Broad Appeal First** - The quest/D&D framing is exciting but niche. The core value proposition must be accessible to people who've never rolled a d20. Lead with *problems solved*, layer in the narrative for those who want it.
4. **Complementary, Not Coupled** - Six Animals works without Campaign Mode. Campaign Mode's NPC agents can be invoked standalone but are designed to complement the animal agents.
5. **MVP Discipline** - The Cat is concerned about scope creep. Start with the three NPCs and quest structure. Character generation, alternative cultural mappings, and extended NPC rosters are post-v1.
6. **Extensible Archetypes** - The animal archetypes are portable. They've already been mapped to Brazilian jungle animals. Campaign Mode should support different characterisations without being locked to fantasy/D&D.

## Implementation Strategy

Campaign Mode will be delivered as **Claude Code skills** (matching the Six Animals pattern) with potential evolution toward a Claude plugin for proper context isolation.

### v1 Scope
- Gandalf, Dragon, and Guardian skill definitions (SKILL.md files)
- Quest lifecycle slash commands (e.g., `/start-campaign`, `/checkpoint`, `/confront-dragon`)
- Integration stubs in animal agent definitions for campaign-aware behaviour
- Simon's campaign-mode extensions (GM responsibilities, debrief protocol)

### Post-v1 Possibilities
- Character generation system (animal + character profile combinations)
- Alternative cultural/thematic mappings (NZ native animals, musical instruments, etc.)
- Extended NPC roster
- Multi-quest campaign arcs
- Easter eggs (Simon Says pattern matching game)

### Deferred Content
The following quest-agent content is deferred to post-v1: NPC technical implementation (custom API / plugin-based agents) and quest example library. These are valuable but not required for the bolt-on skill-based delivery of v1.

## Decisions Made

The following Architecture Decision Records (ADRs) capture the key decisions made during Campaign Mode design:

| ADR | Title | Summary |
|-----|-------|---------|
| [ADR-CM-001](adrs/ADR-CM-001-Campaign-Mode-Architecture.md) | Campaign Mode Architecture (Master ADR) | 3-NPC bolt-on architecture delivered as Claude Code skills, complementing Six Animals |
| [ADR-CM-002](adrs/ADR-CM-002-Quest-Agent-Decomposition.md) | Quest Agent Decomposition | Decomposing quest-council's monolithic quest-agent into 3 focused NPCs (Gandalf, Dragon, Guardian) |
| [ADR-CM-003](adrs/ADR-CM-003-NPC-Context-Isolation.md) | NPC Context Isolation | Three isolation levels (advisory, independent, maximum) enforced by instruction, with future evolution path |
| [ADR-CM-004](adrs/ADR-CM-004-Skill-Based-Implementation.md) | Skill-Based Implementation | Claude Code skills (SKILL.md files) as implementation format, matching Six Animals patterns |
| [ADR-CM-005](adrs/ADR-CM-005-Campaign-Mode-Selection.md) | Campaign Mode Selection | Three campaign modes (Grow, Ship, Grow & Ship) selected by user, tuning all NPC behaviour |

---

## Open Questions

### Architecture & Implementation

1. ~~**Context isolation mechanism**~~ **RESOLVED** ([ADR-CM-003](adrs/ADR-CM-003-NPC-Context-Isolation.md)) - Context isolation is advisory/instruction-based in v1, with three levels: advisory (Gandalf), independent (Guardian), maximum (Dragon). NPCs are invoked as sub-agents with scoped input. Hard enforcement may require future plugin/API evolution.

2. **Simon's dual role** - Simon is currently the educator/supervisor in Six Animals. In Campaign Mode, should Simon also absorb the GM (Game Master) role, or should GM be a distinct fourth NPC? Combining simplifies the NPC count but risks role overload.

3. **Slash command design** - What is the full command vocabulary for campaign lifecycle? How does `/start-campaign` differ from the original `/start-quest`? What commands does the user need vs. what happens automatically?

4. ~~**Skill file structure**~~ **RESOLVED** ([ADR-CM-004](adrs/ADR-CM-004-Skill-Based-Implementation.md)) - NPC skills live in the campaign-mode repo as standalone SKILL.md files in dual locations: `skills/` (canonical) and `.claude/skills/` (auto-discovery). Installation via clone, copy, or personal skills. Follows the same pattern as Six Animals.

5. **State management** - How does campaign state persist across sessions? Where does quest progress, checkpoint status, and character profiles live?

### Design & Scope

6. **Character generation** - Is this v1 or post-v1? The conversation wavered. If v1, how deep does it go - simple flavour text, or mechanically meaningful profiles that alter agent behaviour?

7. **Dragon success criteria** - Who defines what the Dragon checks for? Is it Gandalf (quest-giver defines acceptance), the user, or derived from the animal agents' own goals?

8. **Guardian trigger points** - What triggers a Guardian checkpoint? Is it time-based, milestone-based, or manually invoked? How do we prevent the party (or the AI) from bypassing the Guardian?

9. ~~**Fantasy framing vs. neutral framing**~~ **RESOLVED** - Decided to use Gandalf/Dragon/Guardian naming. Gandalf has broad cultural recognition, Dragon is universal, Guardian is already neutral. The names are evocative and memorable. Per the Extensible Archetypes principle, they can be re-skinned for different cultural contexts later.

10. **Mainstream onboarding** - What does "step 1" look like for someone who doesn't know Six Animals or D&D? What's the 30-second pitch that gets a mainstream user to try Campaign Mode?

### Collaboration & Ecosystem

11. **Separation from Six Animals website** - The conversation noted these should be "independent but complementary" on the website. What does that boundary look like in practice?

12. **Cultural adaptability** - If the animals can be remapped to different cultural contexts (Brazilian jungle, NZ native, etc.), can the NPCs be similarly remapped? What's the abstraction layer?

13. **Multi-user campaigns** - Is Campaign Mode single-user-with-AI-agents only, or could it support multiple humans each adopting animal roles in a shared campaign?

14. **Feedback loop to Six Animals** - Campaign Mode will surface insights about how the animal roles interact under pressure. How do those insights flow back to improve the core Six Animals framework?

15. **Licensing alignment** - Six Animals uses MIT (code) + CC-BY-SA-4.0 (content). Does Campaign Mode follow the same model? Are there IP considerations with Gandalf/Dragon naming (Tolkien estate)?
