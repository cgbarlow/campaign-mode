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
| **Gandalf** | Mentor - guides the party's performance on the quest, provides strategic counsel | Quest-giver / Mentor archetype |
| **Dragon** | Adversary - represents the challenge to be overcome, checks if success criteria are truly met | Final boss / Acceptance test |
| **Guardian** | Gatekeeper - must approve progress before the party can advance to the next stage | Stage gate / Quality gate |

### The Supervisor (Simon - Meta Layer)
Simon remains the **educator and meta-analyst**, operating above the quest narrative:
- Debriefs after encounters and provides learning insights
- Coaches role performance across both animals and NPCs
- Shows players "behind the curtain" - the pedagogical and psychological dynamics at work
- Optionally takes on GM (Game Master) responsibilities when quest mode is active

## How It Works (Envisioned Flow)

1. **Quest Definition** - Gandalf frames the challenge and establishes success criteria
2. **Character Setup** - Animals optionally adopt characterisations/profiles (e.g., Cat becomes a Halfling Thief, Bear becomes a Human Paladin)
3. **Campaign Execution** - The party works through the quest, with animals contributing from their archetype strengths
4. **Guardian Checkpoints** - At key stages, the Guardian evaluates whether the party can progress
5. **Dragon Confrontation** - The Dragon tests whether all success criteria have been genuinely met
6. **Simon Debrief** - Simon provides educational feedback on the journey, role performance, and group dynamics

## Design Principles

1. **Context Isolation** - NPCs must NOT share context with party members. The Guardian and Dragon need independent judgement, not information contaminated by the party's reasoning. Sub-agents are the implementation mechanism.
2. **Broad Appeal First** - The quest/D&D framing is exciting but niche. The core value proposition must be accessible to people who've never rolled a d20. Lead with *problems solved*, layer in the narrative for those who want it.
3. **Complementary, Not Coupled** - Six Animals works without Campaign Mode. Campaign Mode enhances Six Animals but should be presented as an independent-but-complementary addition, not a dependency.
4. **MVP Discipline** - The Cat is concerned about scope creep. Start with the three NPCs and quest structure. Character generation, alternative cultural mappings, and extended NPC rosters are post-v1.
5. **Extensible Archetypes** - The animal archetypes are portable. They've already been mapped to Brazilian jungle animals. Campaign Mode should support different characterisations without being locked to fantasy/D&D.

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

---

## Open Questions

### Architecture & Implementation

1. **Context isolation mechanism** - How exactly do we enforce that NPC sub-agents cannot access party context within Claude Code's current skill/agent architecture? Is the Claude Agents team functionality sufficient, or do we need a plugin?

2. **Simon's dual role** - Simon is currently the educator/supervisor in Six Animals. In Campaign Mode, should Simon also absorb the GM (Game Master) role, or should GM be a distinct fourth NPC? Combining simplifies the NPC count but risks role overload.

3. **Slash command design** - What is the full command vocabulary for campaign lifecycle? How does `/start-campaign` differ from the original `/start-quest`? What commands does the user need vs. what happens automatically?

4. **Skill file structure** - Should NPC skill definitions live in the six-animals repo (as extensions) or in the campaign-mode repo (as a separate installable package)? What's the installation/activation story?

5. **State management** - How does campaign state persist across sessions? Where does quest progress, checkpoint status, and character profiles live?

### Design & Scope

6. **Character generation** - Is this v1 or post-v1? The conversation wavered. If v1, how deep does it go - simple flavour text, or mechanically meaningful profiles that alter agent behaviour?

7. **Dragon success criteria** - Who defines what the Dragon checks for? Is it Gandalf (quest-giver defines acceptance), the user, or derived from the animal agents' own goals?

8. **Guardian trigger points** - What triggers a Guardian checkpoint? Is it time-based, milestone-based, or manually invoked? How do we prevent the party (or the AI) from bypassing the Guardian?

9. **Fantasy framing vs. neutral framing** - Should v1 use Gandalf/Dragon/Guardian naming (evocative but niche), or more neutral terms (Mentor/Challenge/Gate) with fantasy as an optional skin?

10. **Mainstream onboarding** - What does "step 1" look like for someone who doesn't know Six Animals or D&D? What's the 30-second pitch that gets a mainstream user to try Campaign Mode?

### Collaboration & Ecosystem

11. **Separation from Six Animals website** - The conversation noted these should be "independent but complementary" on the website. What does that boundary look like in practice?

12. **Cultural adaptability** - If the animals can be remapped to different cultural contexts (Brazilian jungle, NZ native, etc.), can the NPCs be similarly remapped? What's the abstraction layer?

13. **Multi-user campaigns** - Is Campaign Mode single-user-with-AI-agents only, or could it support multiple humans each adopting animal roles in a shared campaign?

14. **Feedback loop to Six Animals** - Campaign Mode will surface insights about how the animal roles interact under pressure. How do those insights flow back to improve the core Six Animals framework?

15. **Licensing alignment** - Six Animals uses MIT (code) + CC-BY-SA-4.0 (content). Does Campaign Mode follow the same model? Are there IP considerations with Gandalf/Dragon naming (Tolkien estate)?
