# Campaign Mode

A quest-based extension for the [Six Animals](https://github.com/SimonMcCallum/six-animals) team collaboration framework. Campaign Mode gives you **purpose, structure, and stakes** — transforming diverse AI perspectives into a structured quest with mentorship, checkpoints, and adversarial testing.

Where Six Animals answers *"how should we work together?"*, Campaign Mode answers *"what are we working toward, and what stands in our way?"*

## Why Campaign Mode?

You have a challenge. You want diverse perspectives, structured progress, and confidence that your work holds up. Campaign Mode provides:

| What you get | How it works |
|-------------|--------------|
| **Direction** | A quest framework that channels collaboration toward defined goals |
| **Your choice of focus** | Grow (learn), Ship (deliver), or both — you decide before the quest begins |
| **Adversarial testing** | A Dragon that stress-tests whether your work genuinely meets success criteria |
| **Quality gates** | A Guardian that ensures you're ready before advancing to harder challenges |
| **Mentorship** | A Gandalf that guides without rescuing — a guide on the side, not a sage on the stage |

Six Animals doesn't tell you who you are — it gives tools to communicate, suggests you can learn new behaviours, encourages giving space to others, and validates different ways of thinking. Campaign Mode extends this by giving those behaviours a **narrative container** — a structured journey where growth happens through doing, not just reflecting.

## Prerequisites

### Claude Code

Campaign Mode is delivered as [Claude Code skills](https://docs.anthropic.com/en/docs/claude-code) — markdown-based agent definitions that Claude Code discovers and makes available as slash commands. You need [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed and working.

### Six Animals (Recommended)

[Six Animals](https://github.com/SimonMcCallum/six-animals) provides six psychologically-grounded team role agents (Bear, Cat, Owl, Puppy, Rabbit, Wolf) plus Simon as educator/supervisor. Campaign Mode's NPC agents are designed to complement the animal agents — the animals form your advisory council, while the NPCs provide mentorship, gatekeeping, and adversarial challenge.

Six Animals works without Campaign Mode. Campaign Mode's NPC agents can be invoked standalone (each is a self-contained skill), but they are designed to work alongside the animal agents for the full campaign experience.

Install Six Animals following the instructions in the [Six Animals repository](https://github.com/SimonMcCallum/six-animals).

### How Skills Work

Claude Code discovers skills from `SKILL.md` files in `.claude/skills/` directories. When you install Campaign Mode (see below), the NPC agents become available as slash commands (`/gandalf-agent`, `/dragon-agent`, `/guardian-agent`) alongside any Six Animals commands you've already installed.

## How It Works

### You (The Protagonist)

You are the protagonist. You drive the quest. You invoke agents. You produce the work. You face the NPCs.

Campaign Mode has AI agents that advise, challenge, and evaluate — but **you** are the decision-maker. You shape the quest, choose which perspectives to consult, do the work, and present it for evaluation. The agents serve your quest; they don't drive it.

### Choose Your Campaign Mode

Before the quest begins, you choose how you want to approach the campaign:

| Mode | Focus | Framing |
|------|-------|---------|
| **Grow** | Learning experience | "What will you learn? Who will you become?" |
| **Ship** | Get work done | "What will you deliver? What does done look like?" |
| **Grow & Ship** (Default) | Both | "What will you learn AND deliver?" |

Your mode tunes how every NPC behaves — from how Gandalf frames the quest, to what the Dragon evaluates, to how fast the Guardian lets you progress. See [ADR-CM-005](docs/adrs/ADR-CM-005-Campaign-Mode-Selection.md) for the full decision record.

### Your Advisory Council (Six Animals)

The six animal agents operate as your advisory council with shared context:

| Animal | How they help your quest |
|--------|------------------------|
| **Bear** | Vision and direction — what are we actually trying to achieve? |
| **Cat** | Risk assessment — what could go wrong? What's the scope? |
| **Owl** | Timeline and process — are we on track? What's the structure? |
| **Puppy** | Morale and momentum — what opportunities are we missing? |
| **Rabbit** | Resources and stakeholders — who and what do we need? |
| **Wolf** | Team cohesion — is everyone contributing? Are we balanced? |

### Your Guides and Challengers (NPCs)

Three NPC agents operate **outside the party's shared context** to maintain objectivity:

| NPC | Role | What they do for you |
|-----|------|---------------------|
| **Gandalf** | Mentor | Frames your quest, establishes success criteria collaboratively, and mentors without rescuing — a guide on the side, not a sage on the stage |
| **Dragon** | Adversary | Tests whether your success criteria are genuinely met through rigorous, independent evaluation. Receives only success criteria, campaign mode, and your final work product |
| **Guardian** | Gatekeeper | Evaluates your progress at checkpoint stages with three gate decisions: approve, block with feedback, or conditional approval. "Not yet" is guidance, not judgement |

NPCs are deliberately isolated from party context. The Guardian and Dragon need independent judgement, not information contaminated by internal reasoning.

### The Supervisor (Simon)

Simon remains the educator and meta-analyst from Six Animals, with extended responsibilities in Campaign Mode:
- Debriefs after encounters and provides learning insights
- Coaches role performance across both animals and NPCs
- Optionally takes on GM (Game Master) responsibilities
- Shows you "behind the curtain" — the pedagogical and psychological dynamics at work

### Campaign Flow

```
1. Quest Definition       You choose your mode. Gandalf frames the challenge.
        |
2. Character Setup        Assign character profiles to animals (optional, mode-dependent)
        |
3. Campaign Execution     You work the quest, invoking animals for their strengths
        |
4. Guardian Checkpoint    You invoke the Guardian to evaluate readiness (mode-aware)
        |                 (repeats at key stages)
5. Dragon Confrontation   You invoke the Dragon to test success criteria (mode-aware)
        |
6. Debrief                Simon provides feedback (depth varies by mode)
```

## Installation

**Option 1: Clone the repo (project-level skills)**

```bash
git clone https://github.com/cgbarlow/campaign-mode.git
cd campaign-mode
# Skills are available as /gandalf-agent, /dragon-agent, /guardian-agent
```

**Option 2: Copy to your project**

```bash
# Copy the .claude/skills/ directory to your project
cp -r campaign-mode/.claude/skills/ your-project/.claude/skills/
```

**Option 3: Personal skills (all projects)**

```bash
# Copy to your personal skills directory
cp -r campaign-mode/.claude/skills/ ~/.claude/skills/
```

Claude Code auto-discovers `SKILL.md` files in `.claude/skills/` directories. Once copied, the NPC commands are available in any Claude Code session within that project (Options 1-2) or globally (Option 3).

## Available Commands

| Command | What it does |
|---------|-------------|
| `/gandalf-agent` | Frame a quest, choose your campaign mode, and establish success criteria |
| `/dragon-agent` | Challenge your work — test whether success criteria are genuinely met |
| `/guardian-agent` | Evaluate progress at a checkpoint — approve, block, or conditionally approve |

These work alongside the existing Six Animals commands (`/bear-agent`, `/cat-agent`, `/owl-agent`, `/puppy-agent`, `/rabbit-agent`, `/wolf-agent`, `/simon-agent`).

## Design Principles

1. **User Agency First** — You are the protagonist. Every design choice increases your agency. Mode selection, quest shaping, agent invocation — you drive.
2. **Context Isolation** — NPCs must not share context with party members. The Dragon operates at maximum isolation (success criteria + campaign mode + work product only). The Guardian evaluates each checkpoint independently.
3. **Complementary, Not Coupled** — Six Animals works without Campaign Mode. Campaign Mode's NPC agents can be invoked standalone but are designed to complement the animal agents.
4. **Broad Appeal First** — The quest framing is engaging but optional. Lead with problems solved, layer in the narrative for those who want it.
5. **Extensible Archetypes** — The animal archetypes are portable across cultures and themes. Campaign Mode supports different characterisations without being locked to any single genre.

## Architecture Decisions

Architectural decisions are documented as ADRs using the WH(Y) format in [docs/adrs/](docs/adrs/). Each ADR captures the context, decision, and reasoning behind key design choices.

| ADR | Title |
|-----|-------|
| [ADR-CM-001](docs/adrs/ADR-CM-001-Campaign-Mode-Architecture.md) | Campaign Mode Architecture |
| [ADR-CM-002](docs/adrs/ADR-CM-002-Quest-Agent-Decomposition.md) | Quest Agent Decomposition |
| [ADR-CM-003](docs/adrs/ADR-CM-003-NPC-Context-Isolation.md) | NPC Context Isolation |
| [ADR-CM-004](docs/adrs/ADR-CM-004-Skill-Based-Implementation.md) | Skill-Based Implementation |
| [ADR-CM-005](docs/adrs/ADR-CM-005-Campaign-Mode-Selection.md) | Campaign Mode Selection |
| [ADR-CM-006](docs/adrs/ADR-CM-006-Character-Generation.md) | Character Generation |

Supporting specifications and reference materials live alongside the ADRs in [docs/specs/](docs/specs/) and [docs/adrs/reference/](docs/adrs/reference/).

## Project Structure

```
campaign-mode/
├── .campaign/                           # Campaign state directory (created during Phase 2)
│   └── profiles/                        # Character profiles (.md files per animal/NPC)
├── .claude/
│   └── skills/                          # Claude Code skill auto-discovery directory
│       ├── gandalf-agent/
│       │   └── SKILL.md
│       ├── dragon-agent/
│       │   └── SKILL.md
│       └── guardian-agent/
│           └── SKILL.md
├── skills/                              # Canonical skill definitions
│   ├── gandalf-agent/
│   │   └── SKILL.md
│   ├── dragon-agent/
│   │   └── SKILL.md
│   └── guardian-agent/
│       └── SKILL.md
├── docs/
│   ├── north-star.md                    # Vision, architecture, and open questions
│   ├── initiation/                      # Design conversation history
│   │   └── initial-thinking-on-campaign-mode.txt
│   ├── reference/
│   │   └── The-Complete-Guide-to-Building-Skill-for-Claude.pdf
│   ├── adrs/                            # Architecture Decision Records
│   │   ├── ADR-CM-001-Campaign-Mode-Architecture.md
│   │   ├── ADR-CM-002-Quest-Agent-Decomposition.md
│   │   ├── ADR-CM-003-NPC-Context-Isolation.md
│   │   ├── ADR-CM-004-Skill-Based-Implementation.md
│   │   ├── ADR-CM-005-Campaign-Mode-Selection.md
│   │   ├── ADR-CM-006-Character-Generation.md
│   │   └── reference/                   # ADR format specifications and references
│   │       ├── ADR-FORMAT.md
│   │       ├── Recording_Architecture_Decisions.md
│   │       ├── SPEC-ADR-A-WHY-Format.md
│   │       ├── SPEC-ADR-B-Minimalism.md
│   │       ├── SPEC-ADR-C-Dependencies.md
│   │       ├── SPEC-ADR-D-Master-ADRs.md
│   │       └── SPEC-ADR-E-Definition-of-Done.md
│   └── specs/                           # Design specifications
│       ├── SPEC-CM-001-A-Skill-Architecture.md
│       ├── SPEC-CM-001-B-Campaign-Lifecycle.md
│       ├── SPEC-CM-002-A-Gandalf-Agent.md
│       ├── SPEC-CM-002-B-Dragon-Agent.md
│       ├── SPEC-CM-002-C-Guardian-Agent.md
│       ├── SPEC-CM-003-A-Context-Isolation-Protocol.md
│       ├── SPEC-CM-004-A-Skill-File-Structure.md
│       ├── SPEC-CM-005-A-Campaign-Mode-Profiles.md
│       ├── SPEC-CM-006-A-Character-Profile-Format.md
│       └── SPEC-CM-006-B-Campaign-State-Directory.md
└── README.md
```

## Roadmap

### v1 — Current State

- Gandalf, Dragon, and Guardian skill definitions with mode-aware behaviour (complete)
- Campaign mode selection: Grow, Ship, Grow & Ship (complete)
- Character generation system — two-depth profiles (flavour + behavioural modifiers), theme-agnostic, user-assigned, stored in `.campaign/profiles/` (complete)
- User-as-protagonist framing throughout (complete)
- Architecture Decision Records documenting key design choices (complete)
- Design specifications for each agent, lifecycle, mode profiles, context isolation, and character profiles (complete)
- North-star vision document with open questions (complete)

### Future

- Integration stubs in animal agent definitions for campaign-aware behaviour
- Simon's campaign-mode extensions (GM responsibilities, debrief protocol)
- Alternative cultural and thematic mappings
- Multi-quest campaign arcs
- Extended NPC roster

See [docs/north-star.md](docs/north-star.md) for the full vision and open questions.

## Relationship to Six Animals

Campaign Mode is an **independent but complementary** project. Six Animals provides the foundational team dynamics framework. Campaign Mode provides the quest structure, adversarial testing, and narrative layer. Together they create a complete system for guided collaborative work.

Six Animals works without Campaign Mode. Campaign Mode's NPC agents can be invoked standalone but are designed to complement the animal agents — the animals provide diverse advisory perspectives, while the NPCs provide quest structure, quality gates, and adversarial challenge.

| Project | Focus | Agents |
|---------|-------|--------|
| [Six Animals](https://github.com/SimonMcCallum/six-animals) | Team roles and collaboration dynamics | Bear, Cat, Owl, Puppy, Rabbit, Wolf + Simon |
| Campaign Mode | Quest structure, mentorship, and adversarial challenge | Gandalf, Dragon, Guardian |

## License

CC-BY-SA-4.0

## Authors

- **Chris Barlow** — Campaign Mode design and implementation
- **Dr. Simon McCallum** — Six Animals framework, pedagogical foundation, Simon agent design
