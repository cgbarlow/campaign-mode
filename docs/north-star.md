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

Mode selection happens during Phase 1 (Quest Definition) and tunes all NPC behaviour for the duration of the campaign. See [ADR-CM-005](2_adrs/ADR-CM-005-Campaign-Mode-Selection.md) for the full decision record.

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

0. **Council (Optional)** - All six animal agents analyse the project through their archetype lenses (Bear: vision, Cat: risk, Owl: process, Puppy: opportunities, Rabbit: resources, Wolf: cohesion). Simon synthesises their findings into a consensus with prioritised next steps. Report saved to `.campaign/council-report.md`. Can be invoked before or during a quest.
1. **Quest Definition** - You choose your campaign mode (Grow / Ship / Grow & Ship). Gandalf frames the challenge and establishes success criteria.
2. **Character Setup** - Users optionally assign character profiles to animals (depth: flavour or modifier; theme: neutral, fantasy, or custom). Gandalf facilitates. Encouraged in Grow mode, skipped in Ship mode. Profiles stored in `.campaign/profiles/`.
3. **Campaign Execution** - You work through the quest, invoking animal agents for their archetype strengths
4. **Guardian Checkpoints** - At key stages, you invoke the Guardian to evaluate whether you're ready to progress
5. **Dragon Confrontation** - You invoke the Dragon to test whether all success criteria have been genuinely met
6. **Simon Debrief** - Simon provides feedback on the journey (full reflection in Grow mode, brief retrospective in Ship mode)

## Design Principles

1. **User Agency First** - The user is the protagonist. Every design choice should increase user agency, not reduce it. Mode selection, quest shaping, agent invocation — the user drives. This aligns with SDT's autonomy principle.
2. **Context Isolation** - NPCs must NOT share context with party members. The Guardian and Dragon need independent judgement, not information contaminated by the party's reasoning. Three isolation levels are defined: advisory (Gandalf), independent (Guardian), maximum (Dragon). In v1, isolation is enforced by instruction and sub-agent invocation; future plugin/API evolution may provide hard architectural enforcement. *(See [ADR-CM-003](2_adrs/ADR-CM-003-NPC-Context-Isolation.md))*
3. **Broad Appeal First** - The quest/D&D framing is exciting but niche. The core value proposition must be accessible to people who've never rolled a d20. Lead with *problems solved*, layer in the narrative for those who want it.
4. **Complementary, Not Coupled** - Six Animals works without Campaign Mode. Campaign Mode's NPC agents can be invoked standalone but are designed to complement the animal agents.
5. **MVP Discipline** - The Cat is concerned about scope creep. Start with the three NPCs, quest structure, and character generation. Alternative cultural mappings and extended NPC rosters are post-v1.
6. **Extensible Archetypes** - The animal archetypes are portable. They've already been mapped to Brazilian jungle animals. Campaign Mode should support different characterisations without being locked to fantasy/D&D.

## Implementation Strategy

Campaign Mode is delivered as a **Claude Code plugin** distributed via the marketplace, with skills as the authoring format. The plugin wraps the existing skill definitions and adds per-session guidelines (CLAUDE.md), a `/campaign-setup` command, and marketplace discoverability. Clone-and-copy remains available as a fallback for contributors and users who prefer manual installation. See [ADR-CM-007](2_adrs/ADR-CM-007-Plugin-Based-Distribution.md).

### v1 Scope
- Gandalf, Dragon, and Guardian skill definitions (SKILL.md files)
- Character generation system — two-depth profiles (flavour + behavioural modifiers), theme-agnostic, user-assigned, stored as `.campaign/profiles/*.md`
- Plugin packaging for Claude Code marketplace distribution ([ADR-CM-007](2_adrs/ADR-CM-007-Plugin-Based-Distribution.md))
- CLAUDE.md campaign guidelines loaded per session
- `/campaign-setup` command for project onboarding
- `/council` command — multi-perspective project diagnostic from all six animal agents with Simon synthesis
- Quest lifecycle slash commands (e.g., `/start-campaign`, `/checkpoint`, `/confront-dragon`)
- Integration stubs in animal agent definitions for campaign-aware behaviour
- Simon's campaign-mode extensions (GM responsibilities, debrief protocol)

### Post-v1 Possibilities
- Alternative cultural/thematic mappings (NZ native animals, musical instruments, etc.)
- Extended NPC roster
- Multi-quest campaign arcs
- Easter eggs (Simon Says pattern matching game)

### Deferred Content
The following quest-agent content is deferred to post-v1: NPC technical implementation (custom API-based agents with hard context isolation) and quest example library. Plugin-based distribution has been promoted to v1 scope via [ADR-CM-007](2_adrs/ADR-CM-007-Plugin-Based-Distribution.md).

## Decisions Made

The following Architecture Decision Records (ADRs) capture the key decisions made during Campaign Mode design:

| ADR | Title | Summary |
|-----|-------|---------|
| [ADR-CM-001](2_adrs/ADR-CM-001-Campaign-Mode-Architecture.md) | Campaign Mode Architecture (Master ADR) | 3-NPC bolt-on architecture delivered as Claude Code skills, complementing Six Animals |
| [ADR-CM-002](2_adrs/ADR-CM-002-Quest-Agent-Decomposition.md) | Quest Agent Decomposition | Decomposing quest-council's monolithic quest-agent into 3 focused NPCs (Gandalf, Dragon, Guardian) |
| [ADR-CM-003](2_adrs/ADR-CM-003-NPC-Context-Isolation.md) | NPC Context Isolation | Three isolation levels (advisory, independent, maximum) enforced by instruction, with future evolution path |
| [ADR-CM-004](2_adrs/ADR-CM-004-Skill-Based-Implementation.md) | Skill-Based Implementation | Claude Code skills (SKILL.md files) as implementation format, matching Six Animals patterns |
| [ADR-CM-005](2_adrs/ADR-CM-005-Campaign-Mode-Selection.md) | Campaign Mode Selection | Three campaign modes (Grow, Ship, Grow & Ship) selected by user, tuning all NPC behaviour |
| [ADR-CM-006](2_adrs/ADR-CM-006-Character-Generation.md) | Character Generation | User-driven character profiles (flavour + behavioural modifiers), theme-agnostic, stored in `.campaign/profiles/` |
| [ADR-CM-007](2_adrs/ADR-CM-007-Plugin-Based-Distribution.md) | Plugin-Based Distribution | Claude Code plugin packaging, CLAUDE.md per-session guidelines, `/campaign-setup` command |

---

## Open Questions

### Architecture & Implementation

1. ~~**Context isolation mechanism**~~ **RESOLVED** ([ADR-CM-003](2_adrs/ADR-CM-003-NPC-Context-Isolation.md)) - Context isolation is advisory/instruction-based in v1, with three levels: advisory (Gandalf), independent (Guardian), maximum (Dragon). NPCs are invoked as sub-agents with scoped input. Hard enforcement may require future plugin/API evolution.

2. **Simon's dual role** - Simon is currently the educator/supervisor in Six Animals. In Campaign Mode, should Simon also absorb the GM (Game Master) role, or should GM be a distinct fourth NPC? Combining simplifies the NPC count but risks role overload.

3. ~~**Slash command design**~~ **RESOLVED** ([ADR-CM-009](2_adrs/ADR-CM-009-Quest-Entry-Commands.md)) - Four command files implemented: `/campaign-setup` (onboarding), `/start-quest` (begin new quest), `/continue-quest` (re-enter active campaign), `/council` (multi-perspective diagnostic). Proactive elicitation means users never need to remember commands after setup.

4. ~~**Skill file structure**~~ **RESOLVED** ([ADR-CM-004](2_adrs/ADR-CM-004-Skill-Based-Implementation.md), [ADR-CM-007](2_adrs/ADR-CM-007-Plugin-Based-Distribution.md)) - NPC skills live in the campaign-mode repo as standalone SKILL.md files. Primary distribution via Claude Code plugin (marketplace). Fallback via clone (`skills/` canonical, `.claude/skills/` auto-discovery) or personal skills. Plugin adds CLAUDE.md per-session guidelines and `/campaign-setup` command.

5. ~~**State management**~~ **RESOLVED** ([ADR-CM-006](2_adrs/ADR-CM-006-Character-Generation.md), [ADR-CM-010](2_adrs/ADR-CM-010-Quest-State-Tracking.md)) - `.campaign/` directory stores profiles in `.campaign/profiles/` and quest state in `.campaign/quest.md`. Quest progress, checkpoint results, and Dragon confrontation outcomes are recorded in an append-only progress log. See [SPEC-CM-006-B](3_specs/SPEC-CM-006-B-Campaign-State-Directory.md).

### Design & Scope

6. ~~**Character generation**~~ **RESOLVED** ([ADR-CM-006](2_adrs/ADR-CM-006-Character-Generation.md)) - Two-depth character profiles (flavour + behavioural modifiers), theme-agnostic, user-assigned, stored as `.campaign/profiles/*.md`. See [SPEC-CM-006-A](3_specs/SPEC-CM-006-A-Character-Profile-Format.md).

7. ~~**Dragon success criteria**~~ **RESOLVED** (Dragon SKILL.md, [SPEC-CM-002-B](3_specs/SPEC-CM-002-B-Dragon-Agent.md)) - Gandalf defines success criteria collaboratively with the user during Phase 1 (Quest Definition). The Dragon receives only these criteria, the campaign mode, and the final work product at maximum isolation. The user shapes what "done" looks like; Gandalf facilitates; the Dragon evaluates.

8. ~~**Guardian trigger points**~~ **RESOLVED** (Guardian SKILL.md, [SPEC-CM-002-C](3_specs/SPEC-CM-002-C-Guardian-Agent.md)) - Guardian checkpoints are milestone-based and user-invoked. The user says "I'm ready for a checkpoint" and invokes the Guardian. Bypassing is prevented by design: proactive elicitation guides users toward checkpoints at natural stage boundaries, and the Guardian's three gate decisions (approve, block, conditional) control progression.

9. ~~**Fantasy framing vs. neutral framing**~~ **RESOLVED** - Decided to use Gandalf/Dragon/Guardian naming. Gandalf has broad cultural recognition, Dragon is universal, Guardian is already neutral. The names are evocative and memorable. Per the Extensible Archetypes principle, they can be re-skinned for different cultural contexts later.

10. **Mainstream onboarding** - What does "step 1" look like for someone who doesn't know Six Animals or D&D? What's the 30-second pitch that gets a mainstream user to try Campaign Mode?

### Collaboration & Ecosystem

11. **Separation from Six Animals website** - The conversation noted these should be "independent but complementary" on the website. What does that boundary look like in practice?

12. **Cultural adaptability** - If the animals can be remapped to different cultural contexts (Brazilian jungle, NZ native, etc.), can the NPCs be similarly remapped? What's the abstraction layer?

13. **Multi-user campaigns** - Is Campaign Mode single-user-with-AI-agents only, or could it support multiple humans each adopting animal roles in a shared campaign?

14. **Feedback loop to Six Animals** - Campaign Mode will surface insights about how the animal roles interact under pressure. How do those insights flow back to improve the core Six Animals framework?

15. ~~**Licensing alignment**~~ **RESOLVED** - Campaign Mode is licensed CC-BY-SA-4.0 (content-only project, no runtime code). "Gandalf" is a trademark of Middle-earth Enterprises, acknowledged in README as a cultural reference. Campaign Mode is not affiliated with or endorsed by the Tolkien Estate or Middle-earth Enterprises.
