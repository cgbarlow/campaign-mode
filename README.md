# Campaign Mode

A quest-based extension for the [Six Animals](https://github.com/SimonMcCallum/six-animals) team collaboration framework. Campaign Mode transforms the six animal archetypes from standalone advisory roles into an **active party** working together on structured quests, guided and challenged by NPC (non-player character) agents.

Where Six Animals answers *"how should we work together?"*, Campaign Mode answers *"what are we working toward, and what stands in our way?"*

![Campaign Mode agents gathered in a fantasy tavern — the six animal advisors (Bear, Cat, Owl, Puppy, Rabbit, Wolf) plan around a map table while Simon observes from by the hearth, Gandalf and the Guardian stand watch, and the Dragon peers in through the window](docs/campaign-mode-agents.jpg)

## Quick Start

### Claude Desktop

1. **Open Settings** — Claude Desktop → Settings → Extensions
2. **Add by URL** — select "Add marketplace from GitHub" and enter:
   ```
   https://github.com/cgbarlow/campaign-mode/
   ```
3. **Install the plugin** — find Campaign Mode in the marketplace and install
4. **Set up your project** — run:
   ```
   /campaign-setup
   ```
   This checks for Six Animals, copies guidelines, and creates `.campaign/`.
5. **Choose your path:**
   - `/council` — Have all six animal advisors analyse your project before deciding what to work on
   - `/start-quest` — Jump straight into quest framing with Gandalf

### Claude Code CLI

1. **Install Claude Code** ([full guide](https://code.claude.com/docs/en/quickstart)):
   ```bash
   curl -fsSL https://claude.ai/install.sh | bash
   ```
2. **Add the marketplace** — in a Claude Code session:
   ```
   /plugin marketplace add cgbarlow/campaign-mode
   ```
3. **Install the plugin:**
   ```
   /plugin install campaign-mode@campaign-mode-marketplace
   ```
4. **Set up your project:**
   ```
   /campaign-setup
   ```
   This checks for Six Animals, copies guidelines, and creates `.campaign/`.
5. **Choose your path:**
   - `/council` — Have all six animal advisors analyse your project before deciding what to work on
   - `/start-quest` — Jump straight into quest framing with Gandalf

That's it. Every agent offers you structured next steps — you never need to memorise commands after setup.

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

### Claude Desktop or Claude Code

Campaign Mode is delivered as a plugin with [Claude Code skills](https://docs.anthropic.com/en/docs/claude-code) — markdown-based agent definitions available as slash commands. It works with both [Claude Desktop](https://claude.ai/download) and [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code).

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

Your mode tunes how every NPC behaves — from how Gandalf frames the quest, to what the Dragon evaluates, to how fast the Guardian lets you progress. See [ADR-CM-005](docs/2_adrs/ADR-CM-005-Campaign-Mode-Selection.md) for the full decision record.

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

Simon is the educator, meta-analyst, and synthesiser — operating *above* the quest while Gandalf operates *within* it. Where Gandalf mentors your actions and frames challenges, Simon observes your patterns, reflects on how you are working, and coaches role performance.

**Simon's three campaign touchpoints:**
- **Council synthesis** — After all six animals deliver their perspectives, Simon pulls threads together, identifies patterns the individual animals couldn't see alone, and produces a consensus assessment
- **Mid-campaign reflection** — Available at any time during the campaign for meta-analysis: how are you working, what roles are you playing, what dynamics is Simon noticing?
- **Post-Dragon debrief** — After the Dragon confrontation concludes, Simon provides a reflective debrief scaled to your campaign mode (full pedagogical reflection in Grow, brief retrospective in Ship)

**How Simon differs from Gandalf:**
- Gandalf guides action — "Here is how to frame this challenge"
- Simon reflects on patterns — "Here is how you have been working, and what I notice about your approach"
- Gandalf is a quest-level mentor; Simon is a meta-level educator

### Campaign Flow

```
   Council (optional)     Animals analyse the project; Simon synthesises findings
        |                 Report saved to .campaign/council-report.md
        |                 Options: Start a quest / Council complete
        |
1. Quest Definition       You choose your mode. Gandalf frames the challenge.
        |                 Gandalf writes .campaign/quest.md with criteria, mode, narrative
        |                 Gandalf offers: Begin working / Review summary / Consult advisor
2. Character Setup        Assign character profiles to animals (optional, mode-dependent)
        |
3. Campaign Execution     You work the quest, invoking animals for their strengths
        |                 Simon available for mid-campaign reflection at any time
        |                 Say "I'm ready for a checkpoint" or "I'm ready to face the Dragon"
4. Guardian Checkpoint    Guardian reads quest.md, evaluates readiness (mode-aware)
        |                 Guardian logs verdict to quest.md, offers next step (repeats at key stages)
5. Dragon Confrontation   Dragon reads quest.md, tests success criteria (mode-aware)
        |                 Dragon logs verdict to quest.md. Dragon offers: Begin debrief / Return to quest
6. Debrief                Simon provides feedback (depth varies by mode)
```

Campaign state is persisted in `.campaign/quest.md` — so you can leave and return between sessions. Use `/continue-quest` to pick up where you left off.

At every phase transition, the active agent offers you structured next-step options — you never need to remember slash commands to keep the campaign moving.

## Examples

| Example | Description |
|---------|-------------|
| [Council Report](docs/4_examples/council-report.md) | Multi-perspective project diagnostic from all six animal agents with Simon synthesis |
| [Bear — The Paladin](docs/4_examples/profiles/bear-paladin.md) | Flavour-depth fantasy profile for Bear |
| [Cat — The Rogue](docs/4_examples/profiles/cat-rogue.md) | Modifier-depth fantasy profile for Cat (includes behavioural modifiers) |
| [Wolf — The Warden](docs/4_examples/profiles/wolf-warden.md) | Flavour-depth fantasy profile for Wolf |

See [SPEC-CM-006-A](docs/3_specs/SPEC-CM-006-A-Character-Profile-Format.md) for the character profile format specification.

## Installation

### Option 1: Claude Desktop (recommended)

1. Open Claude Desktop → Settings → Extensions
2. Select "Add marketplace by URL" and enter:
   ```
   https://github.com/cgbarlow/campaign-mode/
   ```
3. Find Campaign Mode in the marketplace and install
4. Run `/campaign-setup` in your project to complete setup:
   ```
   /campaign-setup
   ```

> `/campaign-setup` will offer to install [Six Animals](https://github.com/SimonMcCallum/six-animals) if it's not already present.

### Option 2: Claude Code CLI

Install [Claude Code](https://code.claude.com/docs/en/quickstart) if you haven't already:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Then in a Claude Code session:

```
/plugin marketplace add cgbarlow/campaign-mode
```

```
/plugin install campaign-mode@campaign-mode-marketplace
```

Run `/campaign-setup` in your project to complete setup:

```
/campaign-setup
```

> `/campaign-setup` will offer to install [Six Animals](https://github.com/SimonMcCallum/six-animals) if it's not already present. You can also install it separately from the same marketplace:
> ```
> /plugin install six-animals@campaign-mode-marketplace
> ```

### Option 3: Clone the repo (for contributors)

```bash
git clone https://github.com/cgbarlow/campaign-mode.git
cd campaign-mode
# Skills auto-discovered via .claude/skills/
# CLAUDE.md guidelines loaded per session
```

### Option 4: Copy to your project

```bash
cp -r campaign-mode/.claude/skills/ your-project/.claude/skills/
cp campaign-mode/CLAUDE.md your-project/CLAUDE.md
```

### Option 5: Personal skills (all projects)

```bash
cp -r campaign-mode/.claude/skills/ ~/.claude/skills/
```

Note: Personal skills do not include CLAUDE.md or commands. Use a plugin install for the full experience.

## Available Commands

| Command | What it does |
|---------|-------------|
| `/campaign-setup` | Set up Campaign Mode in your project — install Six Animals if needed, copy guidelines, create `.campaign/` directory |
| `/council` | Convene the Council — all six animal agents analyse your project, then Simon synthesises their findings into a consensus |
| `/start-quest` | Begin a new quest — checks for active campaigns, then invokes Gandalf to frame the challenge |
| `/continue-quest` | Re-enter an active campaign — detects where you left off and offers next-step options |
| `/gandalf-agent` | Frame a quest, choose your campaign mode, and establish success criteria |
| `/dragon-agent` | Challenge your work — test whether success criteria are genuinely met |
| `/guardian-agent` | Evaluate progress at a checkpoint — approve, block, or conditionally approve |

These work alongside the existing Six Animals commands (`/bear-agent`, `/cat-agent`, `/owl-agent`, `/puppy-agent`, `/rabbit-agent`, `/wolf-agent`, `/simon-agent`).

## Design Principles

1. **User Agency First** — You are the protagonist. Every design choice increases your agency. Mode selection, quest shaping, agent invocation — you drive.
2. **Proactive Elicitation** — Agents offer the next step at every phase transition. You never need to remember slash commands — you choose from options. Ending a phase without offering next steps is a bug.
3. **Context Isolation** — NPCs must not share context with party members. The Dragon operates at maximum isolation (success criteria + campaign mode + work product only). The Guardian evaluates each checkpoint independently.
4. **Complementary, Not Coupled** — Six Animals works without Campaign Mode. Campaign Mode's NPC agents can be invoked standalone but are designed to complement the animal agents.
5. **Broad Appeal First** — The quest framing is engaging but optional. Lead with problems solved, layer in the narrative for those who want it.
6. **Extensible Archetypes** — The animal archetypes are portable across cultures and themes. Campaign Mode supports different characterisations without being locked to any single genre.

## Architecture Decisions

Architectural decisions are documented as ADRs using the WH(Y) format in [docs/2_adrs/](docs/2_adrs/). Each ADR captures the context, decision, and reasoning behind key design choices.

| ADR | Title |
|-----|-------|
| [ADR-CM-001](docs/2_adrs/ADR-CM-001-Campaign-Mode-Architecture.md) | Campaign Mode Architecture |
| [ADR-CM-002](docs/2_adrs/ADR-CM-002-Quest-Agent-Decomposition.md) | Quest Agent Decomposition |
| [ADR-CM-003](docs/2_adrs/ADR-CM-003-NPC-Context-Isolation.md) | NPC Context Isolation |
| [ADR-CM-004](docs/2_adrs/ADR-CM-004-Skill-Based-Implementation.md) | Skill-Based Implementation |
| [ADR-CM-005](docs/2_adrs/ADR-CM-005-Campaign-Mode-Selection.md) | Campaign Mode Selection |
| [ADR-CM-006](docs/2_adrs/ADR-CM-006-Character-Generation.md) | Character Generation |
| [ADR-CM-007](docs/2_adrs/ADR-CM-007-Plugin-Based-Distribution.md) | Plugin-Based Distribution |
| [ADR-CM-008](docs/2_adrs/ADR-CM-008-Proactive-Elicitation.md) | Proactive Elicitation |
| [ADR-CM-009](docs/2_adrs/ADR-CM-009-Quest-Entry-Commands.md) | Quest Entry Commands |
| [ADR-CM-010](docs/2_adrs/ADR-CM-010-Quest-State-Tracking.md) | Quest State Tracking |
| [ADR-CM-011](docs/2_adrs/ADR-CM-011-Council-Feature.md) | Council Feature |
| [ADR-CM-012](docs/2_adrs/ADR-CM-012-Plugin-Desktop-Compatibility.md) | Plugin Desktop Compatibility |
| [ADR-CM-013](docs/2_adrs/ADR-CM-013-Plugin-Guidelines-Parity.md) | Plugin Guidelines Parity |
| [ADR-CM-014](docs/2_adrs/ADR-CM-014-Animal-Campaign-Extensions.md) | Animal Campaign Extensions |
| [ADR-CM-015](docs/2_adrs/ADR-CM-015-Plugin-Injection-Sandbox-Fix.md) | Plugin Injection Sandbox Fix |

Supporting specifications and reference materials live alongside the ADRs in [docs/3_specs/](docs/3_specs/) and [docs/2_adrs/reference/](docs/2_adrs/reference/).

## Project Structure

```
campaign-mode/
├── .campaign/                           # Campaign state directory
│   ├── quest.md                         # Quest definition, criteria, progress log (created Phase 1)
│   ├── council-report.md               # Council analysis report (created by /council)
│   └── profiles/                        # Character profiles (.md files per animal/NPC)
├── .claude/
│   └── skills/                          # Claude Code skill auto-discovery (clone path)
│       ├── gandalf-agent/
│       │   └── SKILL.md
│       ├── dragon-agent/
│       │   └── SKILL.md
│       └── guardian-agent/
│           └── SKILL.md
├── .claude-plugin/
│   └── plugin.json                      # Plugin manifest (plugin path)
├── extensions/
│   └── animal-campaign-context.md       # Animal agent campaign behaviour extensions
├── .github/
│   └── ISSUE_TEMPLATE/                  # GitHub issue templates
│       ├── bug-report.md
│       ├── feature-request.md
│       └── profile-submission.md
├── skills/                              # Canonical skill definitions
│   ├── gandalf-agent/
│   │   └── SKILL.md
│   ├── dragon-agent/
│   │   └── SKILL.md
│   └── guardian-agent/
│       └── SKILL.md
├── commands/                            # Slash commands (plugin path)
│   ├── campaign-setup.md               # /campaign-setup command
│   ├── council.md                      # /council command
│   ├── start-quest.md                  # /start-quest command
│   └── continue-quest.md              # /continue-quest command
├── docs/
│   ├── north-star.md                    # Vision, architecture, and open questions
│   ├── 0_reference/
│   │   └── The-Complete-Guide-to-Building-Skill-for-Claude.pdf
│   ├── 1_initiation/                    # Design conversation history
│   │   └── initial-thinking-on-campaign-mode.txt
│   ├── 2_adrs/                          # Architecture Decision Records
│   │   ├── ADR-CM-001-Campaign-Mode-Architecture.md
│   │   ├── ADR-CM-002-Quest-Agent-Decomposition.md
│   │   ├── ADR-CM-003-NPC-Context-Isolation.md
│   │   ├── ADR-CM-004-Skill-Based-Implementation.md
│   │   ├── ADR-CM-005-Campaign-Mode-Selection.md
│   │   ├── ADR-CM-006-Character-Generation.md
│   │   ├── ADR-CM-007-Plugin-Based-Distribution.md
│   │   ├── ADR-CM-008-Proactive-Elicitation.md
│   │   ├── ADR-CM-012-Plugin-Desktop-Compatibility.md
│   │   ├── ADR-CM-013-Plugin-Guidelines-Parity.md
│   │   ├── ADR-CM-014-Animal-Campaign-Extensions.md
│   │   ├── ADR-CM-015-Plugin-Injection-Sandbox-Fix.md
│   │   ├── ADR-CM-016-Profile-Packs.md
│   │   └── reference/                   # ADR format specifications and references
│   ├── 3_specs/                         # Design specifications
│   │   ├── SPEC-CM-001-A-Skill-Architecture.md
│   │   ├── SPEC-CM-001-B-Campaign-Lifecycle.md
│   │   ├── SPEC-CM-002-A-Gandalf-Agent.md
│   │   ├── SPEC-CM-002-B-Dragon-Agent.md
│   │   ├── SPEC-CM-002-C-Guardian-Agent.md
│   │   ├── SPEC-CM-003-A-Context-Isolation-Protocol.md
│   │   ├── SPEC-CM-004-A-Skill-File-Structure.md
│   │   ├── SPEC-CM-005-A-Campaign-Mode-Profiles.md
│   │   ├── SPEC-CM-006-A-Character-Profile-Format.md
│   │   ├── SPEC-CM-006-B-Campaign-State-Directory.md
│   │   ├── SPEC-CM-007-A-Plugin-Structure.md
│   │   ├── SPEC-CM-007-B-Campaign-Guidelines.md
│   │   ├── SPEC-CM-007-C-Plugin-Path-Resolution.md
│   │   ├── SPEC-CM-007-D-Plugin-Guidelines-Injection.md
│   │   ├── SPEC-CM-008-A-Animal-Campaign-Extensions.md
│   │   └── SPEC-CM-009-A-Profile-Pack-Format.md
│   ├── 4_examples/                      # Example content
│   │   ├── council-report.md            # Example council diagnostic report
│   │   └── profiles/                    # Example character profiles
│   │       ├── bear-paladin.md
│   │       ├── cat-rogue.md
│   │       └── wolf-warden.md
│   └── 5_roadmap/                       # Roadmap documents
│       ├── ROADMAP-CM-001-Guidelines-Parity.md
│       ├── ROADMAP-CM-002-Animal-Campaign-Extensions.md
│       └── ROADMAP-CM-003-v0.2.8.md
├── profile-packs/                       # Pre-built profile template sets
│   ├── fantasy/                         # D&D-inspired theme (9 profiles)
│   ├── hundred-acre-wood/               # Winnie-the-Pooh theme (9 profiles)
│   └── family-parenting/                # Family & Parenting theme (9 profiles)
├── CLAUDE.md                            # Campaign guidelines (loaded per session)
├── CONTRIBUTING.md                      # Contribution guidelines
└── README.md
```

## Roadmap

### v0.3.2 — Current Release

- **Family & Parenting pack** — New 9-profile theme: The Elder, The Teenager, The Family Therapist, The Neighbour Kid, The Co-Parent, The Older Sibling + The Paediatrician, The Social Worker, Great Aunt Betty
- Third built-in pack added to Gandalf Phase 2 dialogue, SPEC-CM-006-A theme tables, and SPEC-CM-009-A built-in packs

### v0.3.1

- Custom profile theme selection now offers **Suggested** (Gandalf designs a set fitting the quest's setting and tone) instead of Fantasy, which is now covered by theme packs
- Retained **Neutral** (professional roles) and **Custom** (describe your own vibe) options

### v0.3.0

- **Profile Packs** — Pre-built theme templates selectable during Gandalf's Phase 2 flow. Pick a pack and all 9 profiles (6 animals + 3 NPCs) are installed instantly.
- **Fantasy pack** — Complete 9-profile D&D-inspired set: Paladin, Rogue, Sage, Bard, Artificer, Warden + Archmage, Sentinel, Ancient Wyrm
- **Hundred Acre Wood pack** — Complete 9-profile Pooh-inspired set: Pooh, Eeyore, Owl, Tigger, Rabbit, Piglet + Christopher Robin, Kanga, Heffalump
- **Unified profile format** (SPEC-CM-006-A v1.1) — All agent types now use the same frontmatter: `archetype`/`skin-name`/`theme`. Dropped explicit `depth` field (inferred from content). Relaxed body section naming. Migration guide included for v1.0 profiles.
- ADR-CM-016 documents the profile packs decision
- SPEC-CM-009-A defines the profile pack directory structure, file requirements, and contribution process
- Gandalf Phase 2 dialogue now offers "Install a theme pack" alongside vanilla and custom options
- CONTRIBUTING.md expanded with profile pack submission guidelines
- Added `.gitignore` to campaign-mode repo to properly exclude `.campaign/` state directory

### v0.2.8

- Added hero image to README — D&D concept art tavern scene featuring all Campaign Mode agents
- **Critical fix:** Plugin injection now works for all installation methods — replaced `!`cat`` with `!`echo`` + Read tool to bypass Claude Code's sandbox restriction (GitHub #9354). Affects all 12 injection points across 4 command files.
- `/campaign-setup` now begins with a Gandalf welcome greeting explaining Campaign Mode, all agent roles (NPCs, animals, Simon), and what to expect
- Simon is now offered as a mid-campaign option in `/continue-quest` and `/start-quest` for meta-analysis and reflection
- Expanded "The Supervisor (Simon)" section in README to clarify the Gandalf/Simon distinction and Simon's three campaign touchpoints
- ADR-CM-015 documents the plugin injection sandbox fix
- Updated SPEC-CM-007-C (v1.2), SPEC-CM-007-D (v1.1), SPEC-CM-008-A (v1.1) with new injection syntax
- See [ROADMAP-CM-003](docs/5_roadmap/ROADMAP-CM-003-v0.2.8.md) for full details

### v0.2.7

- Gandalf SKILL.md now has mechanical Phase 3 progress tracking instructions (Read/Write tool steps) matching the detail level of Phase 1/2 — fixes Gandalf not updating `quest.md` during campaign execution
- Animal agents (Bear, Cat, Owl, Puppy, Rabbit, Wolf) now receive campaign extensions when invoked through quest commands — enabling quest-aware advice, progress tracking, and phase transition awareness
- New `extensions/animal-campaign-context.md` defines campaign behaviour extensions for animal agents, injected into `/continue-quest`, `/start-quest`, and `/council` via dynamic context injection
- Six Animals SKILL.md files gain a generic "Context Extensions" stub, priming animals to respect supplementary instructions from any orchestration context
- ADR-CM-014 and SPEC-CM-008-A document the animal campaign extensions approach and cross-project dependency
- See [ROADMAP-CM-002](docs/5_roadmap/ROADMAP-CM-002-Animal-Campaign-Extensions.md) for full details

### v0.2.6

- CLAUDE.md campaign conventions now injected into all command invocation paths (`/start-quest`, `/continue-quest`, `/council`) via dynamic context injection
- NPC SKILL.md files now include a condensed "Campaign Conventions" section covering cross-cutting rules (identity, lifecycle, elicitation, debrief) for direct skill invocations
- Corrected SPEC-CM-007-B: plugin CLAUDE.md is NOT auto-loaded by the plugin infrastructure
- ADR-CM-013 and SPEC-CM-007-D document the hybrid injection + condensed subset approach
- See [ROADMAP-CM-001](docs/5_roadmap/ROADMAP-CM-001-Guidelines-Parity.md) for full details

### v0.2.5

- Claude Desktop installation instructions in Quick Start and Installation sections
- `start-quest` and `continue-quest` now invoke animal agents via the Skill tool instead of attempting to read skill files from the filesystem — animal skills belong to the Six Animals plugin, not Campaign Mode

### v0.2.4

- Plugin commands now work in Claude Desktop via dynamic context injection (`!`command`` syntax with `${CLAUDE_PLUGIN_ROOT}`)
- Commands inject skill definitions at invocation time instead of referencing file paths at runtime
- ADR-CM-012 and SPEC-CM-007-C document the approach

### v0.2

- `/council` command — multi-perspective project diagnostic from all six animal agents with Simon synthesis, persistent report in `.campaign/council-report.md`
- `/campaign-setup` now offers structured next steps (start quest, convene council, just exploring) instead of slash command references
- `/continue-quest` detects council reports and offers reconvene option in both no-quest and mid-campaign paths
- Quick Start guide in README

### v0.1

- Gandalf, Dragon, and Guardian skill definitions with mode-aware behaviour
- Campaign mode selection: Grow, Ship, Grow & Ship
- Character generation system — two-depth profiles (flavour + behavioural modifiers), theme-agnostic, user-assigned, stored in `.campaign/profiles/`
- Proactive elicitation — agents offer structured next-step options at every phase transition via `AskUserQuestion`; no slash command references in user-facing text
- Campaign Debrief Protocol — Dragon-to-Simon handoff with mode-aware context
- Dragon Voice and Tone — imposing, terse, authoritative confrontation presence
- Plugin packaging for Claude Code marketplace distribution
- CLAUDE.md campaign guidelines loaded per session
- `/campaign-setup` command for project onboarding
- `/start-quest` and `/continue-quest` commands for ergonomic quest entry and mid-campaign re-entry
- Quest state persistence — campaign mode, success criteria, and progress log stored in `.campaign/quest.md` for durable state across sessions
- Speaker identification — every agent response begins with an emoji + bold name tag; profile name overrides apply when character profiles are assigned
- User-as-protagonist framing throughout
- Architecture Decision Records documenting key design choices (ADR-CM-001 through ADR-CM-011)
- Design specifications for each agent, lifecycle, mode profiles, context isolation, character profiles, and plugin structure
- North-star vision document with open questions

### Future

- Integration stubs in animal agent definitions for campaign-aware behaviour
- Simon's campaign-mode extensions (GM responsibilities, expanded debrief)
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

## Contributing

Contributions are welcome — bug reports, feature ideas, character profiles, campaign experiences, and documentation improvements. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Acknowledgements

"Gandalf" is a trademark of Middle-earth Enterprises, used here as a cultural reference to describe an archetypal mentor role. Campaign Mode is not affiliated with or endorsed by the Tolkien Estate or Middle-earth Enterprises. "Dragon" and "Guardian" are generic terms used in their common English sense.

## License

CC-BY-SA-4.0

## Authors

- **Chris Barlow** — Campaign Mode design and implementation
- **Dr. Simon McCallum** — Six Animals framework, pedagogical foundation, Simon agent design
