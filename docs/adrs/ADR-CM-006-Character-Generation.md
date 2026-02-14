# ADR-CM-006: Character Generation

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-006 |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Proposed |

---

## WH(Y) Decision Statement

**In the context of** Campaign Mode's Phase 2 (Character Setup) and the desire to let users customise how animal agents present and behave within a campaign,

**facing** the need for a character generation system that supports multiple depths (flavour vs. behavioural modifiers), is theme-agnostic, preserves core animal archetypes as hard constraints, and stores profiles as exportable campaign state,

**we decided for** a user-driven character generation system facilitated by Gandalf during Phase 2, with two depth levels (narrative flavour and behavioural modifiers), theme-agnostic profiles stored as markdown files in `.campaign/profiles/`, selective application to any subset of animals, and light thematic skins for NPCs,

**and neglected** auto-generated profiles (animals self-assign -- removes user agency), full D&D character sheets (too niche, violates Broad Appeal First), a separate `/character-gen` skill (Gandalf already owns Phase 2), and persistent cross-campaign rosters (over-engineering state management for v1),

**to achieve** user agency over party composition, thematic flexibility across cultures and contexts, preserved animal archetype integrity, and exportable campaign state,

**accepting that** Gandalf's SKILL.md grows more complex, the `.campaign/` directory introduces state management concerns, and theme-agnostic profiles require more abstraction than a fantasy-only system.

---

## Context

Campaign Mode's Phase 2 (Character Setup) was originally scoped as a post-v1 feature: "Character generation is post-v1 scope. In v1, this phase is a simple narrative exercise." The initiation conversation between Simon and Chris envisioned applying D&D-style character profiles to animals ("Cat becomes Human Paladin or perhaps Halfling Thief"), and the north-star listed it as a post-v1 possibility.

This ADR promotes character generation to a fully specified v1 feature. The system allows users to optionally assign character profiles to any subset of the six animal agents, choosing between narrative flavour (changes tone and vocabulary) and behavioural modifiers (tunes how animals contribute within archetype bounds). NPCs can receive light thematic skins, including name changes.

### Design Decisions

| Decision | Answer |
|----------|--------|
| **Profile depth** | User chooses: vanilla (no profile), narrative flavour, or behavioural modifiers |
| **Theme scope** | Theme-agnostic from day 1. Neutral defaults, themes opt-in. User can design custom via Socratic dialogue |
| **Who generates** | User assigns all. Gandalf provides guidance if selections conflict with Six Animals theory |
| **Persistence** | Per-campaign, exportable (user can save/reuse but system doesn't manage a roster) |
| **Partial profiles** | Selective -- user can profile any subset of animals, rest stay vanilla |
| **NPC profiles** | NPCs keep core identities but get light thematic skin including name changes |
| **Storage** | Profile files (.md) in a `.campaign/profiles/` directory |
| **Default suggestions** | Neutral language ("Visionary Leader", "Risk Analyst"), fantasy/other themes opt-in |
| **Guardrails** | Hard constraints -- core archetypes non-negotiable, Gandalf warns AND blocks incompatible profiles |
| **Implementation** | Gandalf owns Phase 2 character generation (no new skill) |

---

## Options Considered

### Option 1: User-Driven Character Generation via Gandalf (Selected)

Users assign profiles to animals during Phase 2, facilitated by Gandalf. Two depth levels (flavour and modifier), theme-agnostic, stored as markdown files in `.campaign/profiles/`.

**Pros:**
- Preserves user agency -- the user decides how each animal presents
- Theme-agnostic design supports fantasy, professional, cultural, and custom framings
- Selective application -- profile any subset, rest stay vanilla
- Hard guardrails protect core archetypes while allowing creative expression
- Gandalf already owns Phase 2, no new skill required
- Exportable profiles enable reuse without system-managed rosters

**Cons:**
- Gandalf's SKILL.md grows more complex
- `.campaign/` directory introduces state management concerns
- Theme-agnostic profiles require more abstraction than a fantasy-only system

### Option 2: Auto-Generated Profiles (Rejected)

Animals self-assign profiles based on quest context and theme.

**Why rejected:** Removes user agency. The user-as-protagonist principle requires the user to make meaningful choices. Auto-generation reduces character setup to a spectator experience.

### Option 3: Full D&D Character Sheets (Rejected)

Detailed character sheets with stats, abilities, classes, and levels.

**Why rejected:** Too niche. Violates the Broad Appeal First principle (Design Principle #3). Users who've never played D&D would find this alienating. The system must be accessible before it is deep.

### Option 4: Separate `/character-gen` Skill (Rejected)

A dedicated skill for character generation, separate from Gandalf.

**Why rejected:** Gandalf already owns Phase 2 (Character Setup). Adding a separate skill fragments the quest flow and creates coordination overhead between skills. Character generation is a natural extension of quest framing.

### Option 5: Persistent Cross-Campaign Roster (Rejected)

A managed roster of character profiles that persists across campaigns with version history and selection UI.

**Why rejected:** Over-engineers state management for v1. The simpler "exportable per-campaign files" model gives users the same capability (copy files to reuse) without system complexity. If demand emerges, a roster system can be added later.

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-006-A](../specs/SPEC-CM-006-A-Character-Profile-Format.md) | Character Profile Format | Profile file structure, depth levels, themes, core vs flex behaviours, NPC skins |
| [SPEC-CM-006-B](../specs/SPEC-CM-006-B-Campaign-State-Directory.md) | Campaign State Directory | `.campaign/` directory structure, profile storage, and export protocol |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Part Of | ADR-CM-001 | Campaign Mode Architecture | Parent initiative |
| Relates To | ADR-CM-002 | Quest Agent Decomposition | Profiles modify animal behaviour within campaigns |
| Relates To | ADR-CM-005 | Campaign Mode Selection | Mode determines whether Phase 2 is offered |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Six Animals Framework | External Project | [github.com/SimonMcCallum/six-animals](https://github.com/SimonMcCallum/six-animals) |
| REF-002 | Campaign Mode North Star | Vision Document | [docs/north-star.md](../north-star.md) |
| REF-003 | Initiation Conversation | Source Material | [docs/initiation/initial-thinking-on-campaign-mode.txt](../initiation/initial-thinking-on-campaign-mode.txt) |

---

## Governance

| Review Board | Date | Outcome | Action | Review Cadence | Next Review |
|--------------|------|---------|--------|----------------|-------------|
| -- | -- | -- | -- | Quarterly | -- |

---

## Status History

| Status | Approver | Date |
|--------|----------|------|
| Proposed | Chris Barlow | 2026-02-14 |
