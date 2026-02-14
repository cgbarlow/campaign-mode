# Campaign Mode

A quest-based extension for the [Six Animals](https://github.com/cgbarlow/six-animals) team collaboration framework. Campaign Mode transforms the six animal archetypes from standalone advisory roles into an **active party** working together on structured quests, guided and challenged by NPC (non-player character) agents.

Where Six Animals answers *"how should we work together?"*, Campaign Mode answers *"what are we working toward, and what stands in our way?"*

## Why Campaign Mode?

Six Animals gives you **roles**. Campaign Mode gives those roles **purpose, structure, and stakes**.

| What Six Animals provides | What Campaign Mode adds |
|---------------------------|------------------------|
| Team role archetypes | A quest framework that channels collaboration toward defined goals |
| Psychological safety through personas | Narrative structure that makes growth happen through doing |
| Behavioural guidance | Adversarial testing to verify the team's work holds up |
| Self-directed reflection | External checkpoints that enforce quality before progressing |

Six Animals doesn't tell you who you are — it gives tools to communicate, suggests you can learn new behaviours, encourages giving space to others, and validates different ways of thinking. Campaign Mode extends this by giving those behaviours a **narrative container**.

## How It Works

### The Party (Six Animals)

The six animal agents operate as party members with shared context:

| Animal | Campaign Role |
|--------|--------------|
| **Bear** | Vision and direction for the quest |
| **Cat** | Risk assessment and scope management |
| **Owl** | Timeline, process, and progress tracking |
| **Puppy** | Morale, momentum, and opportunity spotting |
| **Rabbit** | Resource identification and stakeholder facilitation |
| **Wolf** | Team cohesion and balanced participation |

### The NPCs (Campaign Mode)

Three NPC agents operate **outside the party's shared context** to maintain objectivity:

| NPC | Role | Purpose |
|-----|------|---------|
| **Gandalf** | Mentor | Frames the quest, provides strategic counsel, guides the party's growth |
| **Dragon** | Adversary | Represents the challenge to overcome — tests whether success criteria are truly met |
| **Guardian** | Gatekeeper | Evaluates progress at key stages — the party cannot advance without approval |

NPCs are deliberately isolated from party context. The Guardian and Dragon need independent judgement, not information contaminated by the party's reasoning.

### The Supervisor (Simon)

Simon remains the educator and meta-analyst from Six Animals, with extended responsibilities in Campaign Mode:
- Debriefs after encounters and provides learning insights
- Coaches role performance across both animals and NPCs
- Optionally takes on GM (Game Master) responsibilities
- Shows players "behind the curtain" — the pedagogical and psychological dynamics at work

### Campaign Flow

```
1. Quest Definition     Gandalf frames the challenge and establishes success criteria
        |
2. Character Setup      Animals optionally adopt character profiles
        |
3. Campaign Execution   The party works the quest, each animal contributing their strengths
        |
4. Guardian Checkpoint  Guardian evaluates whether the party can progress
        |               (repeats at key stages)
5. Dragon Confrontation Dragon tests whether all success criteria are genuinely met
        |
6. Simon Debrief        Educational feedback on the journey, roles, and group dynamics
```

## Installation

Campaign Mode is delivered as [Claude Code skills](https://docs.anthropic.com/en/docs/claude-code), matching the Six Animals pattern.

**Prerequisites:** [Six Animals](https://github.com/cgbarlow/six-animals) installed as project or personal skills.

**Option 1: Project-level skills**

Clone the repo and the NPC skills are available within this project:

```bash
git clone https://github.com/cgbarlow/campaign-mode.git
cd campaign-mode
# Skills are available as /gandalf-agent, /dragon-agent, /guardian-agent
```

**Option 2: Copy to your project**

```bash
cp -r campaign-mode/.claude/skills/ your-project/.claude/skills/
```

**Option 3: Personal skills (all projects)**

```bash
cp -r campaign-mode/.claude/skills/ ~/.claude/skills/
```

## Available Commands

| Command | What it does |
|---------|-------------|
| `/gandalf-agent` | Frame a quest, provide mentorship, and establish success criteria |
| `/dragon-agent` | Challenge the party — test whether success criteria are genuinely met |
| `/guardian-agent` | Evaluate progress at a checkpoint — approve or block advancement |

These work alongside the existing Six Animals commands (`/bear-agent`, `/cat-agent`, `/owl-agent`, `/puppy-agent`, `/rabbit-agent`, `/wolf-agent`, `/simon-agent`).

## Design Principles

1. **Complementary, Not Coupled** — Six Animals works without Campaign Mode. Campaign Mode enhances Six Animals but is not a dependency.
2. **Context Isolation** — NPCs must not share context with party members. Sub-agents enforce this boundary.
3. **Broad Appeal First** — The quest framing is engaging but optional. Lead with problems solved, layer in the narrative for those who want it.
4. **Extensible Archetypes** — The animal archetypes are portable across cultures and themes. Campaign Mode supports different characterisations without being locked to any single genre.

## Project Structure

```
campaign-mode/
├── .claude/
│   └── skills/              # Claude Code skill discovery directory
│       ├── gandalf-agent/
│       ├── dragon-agent/
│       └── guardian-agent/
├── skills/                   # Canonical skill definitions
│   ├── gandalf-agent/SKILL.md
│   ├── dragon-agent/SKILL.md
│   └── guardian-agent/SKILL.md
├── docs/
│   ├── north-star.md         # Vision, architecture, and open questions
│   └── initiation/           # Design conversation history
└── README.md
```

## Roadmap

### v1
- Gandalf, Dragon, and Guardian skill definitions
- Quest lifecycle commands
- Integration stubs in animal agent definitions for campaign-aware behaviour
- Simon's campaign-mode extensions (GM responsibilities, debrief protocol)

### Future
- Character generation system (animal + character profile combinations)
- Alternative cultural/thematic mappings
- Multi-quest campaign arcs
- Extended NPC roster

## Relationship to Six Animals

Campaign Mode is an **independent but complementary** project. Six Animals provides the foundational team dynamics framework. Campaign Mode provides the quest structure, adversarial testing, and narrative layer. Together they create a complete system for guided collaborative work — but either can be used on its own.

| Project | Focus | Agents |
|---------|-------|--------|
| [Six Animals](https://github.com/cgbarlow/six-animals) | Team roles and collaboration dynamics | Bear, Cat, Owl, Puppy, Rabbit, Wolf + Simon |
| Campaign Mode | Quest structure, mentorship, and adversarial challenge | Gandalf, Dragon, Guardian |

## License

CC-BY-SA-4.0

## Authors

- **Chris Barlow** — Campaign Mode design and implementation
- **Dr. Simon McCallum** — Six Animals framework, pedagogical foundation, Simon agent design