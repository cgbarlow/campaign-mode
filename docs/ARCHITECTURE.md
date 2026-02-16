# Architecture

Campaign Mode's design decisions, principles, and project structure.

## Design Principles

1. **User Agency First** — You are the protagonist. Every design choice increases your agency. Mode selection, quest shaping, agent invocation — you drive.
2. **Proactive Elicitation** — Agents offer the next step at every phase transition. You never need to remember slash commands — you choose from options. Ending a phase without offering next steps is a bug.
3. **Context Isolation** — NPCs must not share context with party members. The Dragon operates at maximum isolation (success criteria + campaign mode + work product only). The Guardian evaluates each checkpoint independently.
4. **Complementary, Not Coupled** — Six Animals works without Campaign Mode. Campaign Mode's NPC agents can be invoked standalone but are designed to complement the animal agents.
5. **Broad Appeal First** — The quest framing is engaging but optional. Lead with problems solved, layer in the narrative for those who want it.
6. **Extensible Archetypes** — The animal archetypes are portable across cultures and themes. Campaign Mode supports different characterisations without being locked to any single genre.

## Architecture Decision Records

Architectural decisions are documented as ADRs using the WH(Y) format in [2_adrs/](2_adrs/). Each ADR captures the context, decision, and reasoning behind key design choices.

| ADR | Title |
|-----|-------|
| [ADR-CM-001](2_adrs/ADR-CM-001-Campaign-Mode-Architecture.md) | Campaign Mode Architecture |
| [ADR-CM-002](2_adrs/ADR-CM-002-Quest-Agent-Decomposition.md) | Quest Agent Decomposition |
| [ADR-CM-003](2_adrs/ADR-CM-003-NPC-Context-Isolation.md) | NPC Context Isolation |
| [ADR-CM-004](2_adrs/ADR-CM-004-Skill-Based-Implementation.md) | Skill-Based Implementation |
| [ADR-CM-005](2_adrs/ADR-CM-005-Campaign-Mode-Selection.md) | Campaign Mode Selection |
| [ADR-CM-006](2_adrs/ADR-CM-006-Character-Generation.md) | Character Generation |
| [ADR-CM-007](2_adrs/ADR-CM-007-Plugin-Based-Distribution.md) | Plugin-Based Distribution |
| [ADR-CM-008](2_adrs/ADR-CM-008-Proactive-Elicitation.md) | Proactive Elicitation |
| [ADR-CM-009](2_adrs/ADR-CM-009-Quest-Entry-Commands.md) | Quest Entry Commands |
| [ADR-CM-010](2_adrs/ADR-CM-010-Quest-State-Tracking.md) | Quest State Tracking |
| [ADR-CM-011](2_adrs/ADR-CM-011-Council-Feature.md) | Council Feature |
| [ADR-CM-012](2_adrs/ADR-CM-012-Plugin-Desktop-Compatibility.md) | Plugin Desktop Compatibility |
| [ADR-CM-013](2_adrs/ADR-CM-013-Plugin-Guidelines-Parity.md) | Plugin Guidelines Parity |
| [ADR-CM-014](2_adrs/ADR-CM-014-Animal-Campaign-Extensions.md) | Animal Campaign Extensions |
| [ADR-CM-015](2_adrs/ADR-CM-015-Plugin-Injection-Sandbox-Fix.md) | Plugin Injection Sandbox Fix |
| [ADR-CM-016](2_adrs/ADR-CM-016-Profile-Packs.md) | Profile Packs |
| [ADR-CM-017](2_adrs/ADR-CM-017-Proactive-Party-Engagement.md) | Proactive Party Engagement |

Supporting specifications and reference materials live alongside the ADRs in [3_specs/](3_specs/) and [2_adrs/reference/](2_adrs/reference/).

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
│   ├── ARCHITECTURE.md                  # This file
│   ├── 0_reference/
│   │   └── The-Complete-Guide-to-Building-Skill-for-Claude.pdf
│   ├── 1_initiation/                    # Design conversation history
│   │   └── initial-thinking-on-campaign-mode.txt
│   ├── 2_adrs/                          # Architecture Decision Records
│   ├── 3_specs/                         # Design specifications
│   ├── 4_examples/                      # Example content
│   │   ├── council-report.md            # Example council diagnostic report
│   │   └── profiles/                    # Example character profiles
│   └── 5_roadmap/                       # Roadmap documents
├── profile-packs/                       # Pre-built profile template sets
│   ├── fantasy/                         # D&D-inspired theme (9 profiles)
│   ├── hundred-acre-wood/               # Winnie-the-Pooh theme (9 profiles)
│   └── family-parenting/                # Family & Parenting theme (9 profiles)
├── CHANGELOG.md                         # Version history
├── CLAUDE.md                            # Campaign guidelines (loaded per session)
├── CONTRIBUTING.md                      # Contribution guidelines
└── README.md
```

## Alternative Installation Methods

The recommended installation is via the Claude Code plugin marketplace (see [README](../README.md#quick-start)). These alternatives are available for contributors and advanced users.

### Clone the repo

```bash
git clone https://github.com/cgbarlow/campaign-mode.git
cd campaign-mode
# Skills auto-discovered via .claude/skills/
# CLAUDE.md guidelines loaded per session
```

### Copy to your project

```bash
cp -r campaign-mode/.claude/skills/ your-project/.claude/skills/
cp campaign-mode/CLAUDE.md your-project/CLAUDE.md
```

### Personal skills (all projects)

```bash
cp -r campaign-mode/.claude/skills/ ~/.claude/skills/
```

Note: Personal skills do not include CLAUDE.md or commands. Use a plugin install for the full experience.
