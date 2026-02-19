# Changelog

All notable changes to Campaign Mode are documented here.

## v0.4.5 — Current Release

- **Fix: Agents not auto-saving conversation transcripts before transition options** — The transcript recording instruction existed in its own section but was not cross-referenced at the point where agents actually present transition/Next Perspective options. Added explicit "ensure transcript is recorded" reminders inside the Next Perspective section (animal-campaign-context.md), Guardian Gate Decisions, and Dragon Interaction Patterns — right where the model reads when it's about to present options.

## v0.4.4

- **Fix: Gandalf skipping Phase 2 (Character Profile) offer** — Core Skill #6 (Conversation Transcript Recording) was incorrectly placed before Core Skill #5 (Character Profile Facilitation) in Gandalf's SKILL.md, causing the model to skip the profile offer and jump straight to the Phase 3 transition. Moved transcript recording to after profile facilitation, restoring correct document order (1→2→3→4→5→6).

## v0.4.3

- **Conversation Transcript Recording** — Every agent consultation now produces a full verbatim transcript saved to `.campaign/conversations/`. One file per session, written silently at the end of each consultation. Users can review past advice, trace reasoning evolution, and pick up context from previous sessions.
  - Transcripts use date-first filenames (`{YYYY-MM-DD}-{HH-MM}-{agent}.md`) for chronological sorting
  - YAML frontmatter captures agent, profile name, phase, campaign mode, and date
  - Full verbatim exchange with speaker tags, plus outcome section for verdicts and recommendations
  - Context isolation preserved: Guardian and Dragon write their own transcripts but must NOT read any — party reasoning remains off-limits to independent evaluators
  - All agents (animals, Gandalf, Guardian, Dragon, Council) record transcripts at their respective consultation endpoints
- ADR-CM-019 documents the conversation transcript recording decision
- SPEC-CM-012-A specifies the full transcript format, write protocol, isolation rules, and per-agent timing
- `/continue-quest` progress summary now includes 3 most recent conversation transcripts
- `/continue-quest` and `/start-quest` allowed-tools expanded to include Write and Bash for transcript recording
- `/council` now records a council session transcript (Step 6b)
- Updated: CLAUDE.md, animal-campaign-context.md, Gandalf SKILL.md, Guardian SKILL.md, Dragon SKILL.md, continue-quest.md, start-quest.md, council.md, SPEC-CM-006-B (v1.3), SPEC-CM-003-A (v1.1)

## v0.4.2

- **AskUserQuestion UX conventions** — Hybrid approach to address Claude Desktop focus-stealing on `AskUserQuestion`. Phase transition questions keep `AskUserQuestion` with mandatory context summaries; mid-flow advisory questions switch to plain-text numbered choices.
  - **Phase transitions** (keep `AskUserQuestion` + context summary): campaign mode selection, transition to execution, transition to Dragon, Guardian approve/conditional, Dragon slain, continue-quest menu, start-quest menu
  - **Mid-flow advisory** (switch to plain text): animal Next Perspective handoffs, Guardian block recovery, Dragon prevails recovery
  - Every `AskUserQuestion` now requires a 1-2 sentence summary in the `question` field so users can decide without scrolling up
  - Plain-text questions use numbered options; agents parse the user's response (number, partial label, or free-form description)
- ADR-CM-018 documents the AskUserQuestion UX conventions decision
- SPEC-CM-011-A specifies the full classification, context summary requirements, and plain-text format
- Updated: CLAUDE.md, animal-campaign-context.md, Guardian SKILL.md, Dragon SKILL.md, Gandalf SKILL.md, continue-quest.md, start-quest.md

## v0.4.1

- **Fix: AskUserQuestion exceeding 4-option limit** — Consolidated option lists in `continue-quest` (7→4), `start-quest` (6→3), `animal-campaign-context` (5→4), and `gandalf-agent` animal menu (6→4). Related options are now grouped with follow-up questions where needed.

## v0.4.0

- **Proactive animal engagement in Phase 3** — Animals are no longer passive tools. Four new mechanisms make the advisory council an active team during Campaign Execution:
  - **Recommended first advisor** — Gandalf analyses quest characteristics and recommends which animal to consult first at Phase 3 entry (risk → Cat, timeline → Owl, vision → Bear, motivation → Puppy, resources → Rabbit, collaboration → Wolf)
  - **Next Perspective handoffs** — After every Phase 3 consultation, animals use `AskUserQuestion` to suggest the next advisor based on what was discussed, with an archetype complement fallback table
  - **Proactive trigger detection** — Each archetype detects trigger signals for other archetypes (e.g., Cat detects risk mentions, Owl detects timeline concerns) and prioritises them in suggestions
  - **Party Assignments** — quest.md now includes a table mapping each success criterion to primary and secondary animal advisors, written by Gandalf during Phase 1
- ADR-CM-017 documents the proactive party engagement decision
- SPEC-CM-010-A specifies all four mechanisms in detail
- Animal campaign extensions (`extensions/animal-campaign-context.md`) expanded with three new sections: Next Perspective, Proactive Engagement, Criterion Progress Awareness
- Gandalf Phase 3 transition now offers a recommended first advisor instead of generic options
- quest.md template includes Party Assignments table between Anticipated Dragon and Progress Log
- SPEC-CM-001-B updated with Phase 3 animal engagement paragraph
- **README revision** — Rewrote README for accessibility and engagement: new elevator pitch and hook, consolidated Quick Start (removed duplicate Installation section), new "What a Quest Looks Like" walkthrough example, second-person voice throughout. Moved changelog to `CHANGELOG.md`, architecture details to `docs/ARCHITECTURE.md`. Reduced from 535 to ~200 lines.

## v0.3.2

- **Family & Parenting pack** — New 9-profile theme: The Elder, The Teenager, The Family Therapist, The Neighbour Kid, The Co-Parent, The Older Sibling + The Paediatrician, The Social Worker, Great Aunt Betty
- Third built-in pack added to Gandalf Phase 2 dialogue, SPEC-CM-006-A theme tables, and SPEC-CM-009-A built-in packs

## v0.3.1

- Custom profile theme selection now offers **Suggested** (Gandalf designs a set fitting the quest's setting and tone) instead of Fantasy, which is now covered by theme packs
- Retained **Neutral** (professional roles) and **Custom** (describe your own vibe) options

## v0.3.0

- **Profile Packs** — Pre-built theme templates selectable during Gandalf's Phase 2 flow. Pick a pack and all 9 profiles (6 animals + 3 NPCs) are installed instantly.
- **Fantasy pack** — Complete 9-profile D&D-inspired set: Paladin, Rogue, Sage, Bard, Artificer, Warden + Archmage, Sentinel, Ancient Wyrm
- **Hundred Acre Wood pack** — Complete 9-profile Pooh-inspired set: Pooh, Eeyore, Owl, Tigger, Rabbit, Piglet + Christopher Robin, Kanga, Heffalump
- **Unified profile format** (SPEC-CM-006-A v1.1) — All agent types now use the same frontmatter: `archetype`/`skin-name`/`theme`. Dropped explicit `depth` field (inferred from content). Relaxed body section naming. Migration guide included for v1.0 profiles.
- ADR-CM-016 documents the profile packs decision
- SPEC-CM-009-A defines the profile pack directory structure, file requirements, and contribution process
- Gandalf Phase 2 dialogue now offers "Install a theme pack" alongside vanilla and custom options
- CONTRIBUTING.md expanded with profile pack submission guidelines
- Added `.gitignore` to campaign-mode repo to properly exclude `.campaign/` state directory

## v0.2.8

- Added hero image to README — D&D concept art tavern scene featuring all Campaign Mode agents
- **Critical fix:** Plugin injection now works for all installation methods — replaced `` !`cat` `` with `` !`echo` `` + Read tool to bypass Claude Code's sandbox restriction (GitHub #9354). Affects all 12 injection points across 4 command files.
- `/campaign-setup` now begins with a Gandalf welcome greeting explaining Campaign Mode, all agent roles (NPCs, animals, Simon), and what to expect
- Simon is now offered as a mid-campaign option in `/continue-quest` and `/start-quest` for meta-analysis and reflection
- Expanded "The Supervisor (Simon)" section in README to clarify the Gandalf/Simon distinction and Simon's three campaign touchpoints
- ADR-CM-015 documents the plugin injection sandbox fix
- Updated SPEC-CM-007-C (v1.2), SPEC-CM-007-D (v1.1), SPEC-CM-008-A (v1.1) with new injection syntax
- See [ROADMAP-CM-003](docs/5_roadmap/ROADMAP-CM-003-v0.2.8.md) for full details

## v0.2.7

- Gandalf SKILL.md now has mechanical Phase 3 progress tracking instructions (Read/Write tool steps) matching the detail level of Phase 1/2 — fixes Gandalf not updating `quest.md` during campaign execution
- Animal agents (Bear, Cat, Owl, Puppy, Rabbit, Wolf) now receive campaign extensions when invoked through quest commands — enabling quest-aware advice, progress tracking, and phase transition awareness
- New `extensions/animal-campaign-context.md` defines campaign behaviour extensions for animal agents, injected into `/continue-quest`, `/start-quest`, and `/council` via dynamic context injection
- Six Animals SKILL.md files gain a generic "Context Extensions" stub, priming animals to respect supplementary instructions from any orchestration context
- ADR-CM-014 and SPEC-CM-008-A document the animal campaign extensions approach and cross-project dependency
- See [ROADMAP-CM-002](docs/5_roadmap/ROADMAP-CM-002-Animal-Campaign-Extensions.md) for full details

## v0.2.6

- CLAUDE.md campaign conventions now injected into all command invocation paths (`/start-quest`, `/continue-quest`, `/council`) via dynamic context injection
- NPC SKILL.md files now include a condensed "Campaign Conventions" section covering cross-cutting rules (identity, lifecycle, elicitation, debrief) for direct skill invocations
- Corrected SPEC-CM-007-B: plugin CLAUDE.md is NOT auto-loaded by the plugin infrastructure
- ADR-CM-013 and SPEC-CM-007-D document the hybrid injection + condensed subset approach
- See [ROADMAP-CM-001](docs/5_roadmap/ROADMAP-CM-001-Guidelines-Parity.md) for full details

## v0.2.5

- Claude Desktop installation instructions in Quick Start and Installation sections
- `start-quest` and `continue-quest` now invoke animal agents via the Skill tool instead of attempting to read skill files from the filesystem — animal skills belong to the Six Animals plugin, not Campaign Mode

## v0.2.4

- Plugin commands now work in Claude Desktop via dynamic context injection (`` !`command` `` syntax with `${CLAUDE_PLUGIN_ROOT}`)
- Commands inject skill definitions at invocation time instead of referencing file paths at runtime
- ADR-CM-012 and SPEC-CM-007-C document the approach

## v0.2

- `/council` command — multi-perspective project diagnostic from all six animal agents with Simon synthesis, persistent report in `.campaign/council-report.md`
- `/campaign-setup` now offers structured next steps (start quest, convene council, just exploring) instead of slash command references
- `/continue-quest` detects council reports and offers reconvene option in both no-quest and mid-campaign paths
- Quick Start guide in README

## v0.1

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

## Future

- Simon's campaign-mode extensions (GM responsibilities, expanded debrief)
- Alternative cultural and thematic mappings
- Multi-quest campaign arcs
- Extended NPC roster

See [docs/north-star.md](docs/north-star.md) for the full vision and open questions.
