# SPEC-CM-006-A: Character Profile Format

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-006-A |
| **Parent ADR** | [ADR-CM-006](../adrs/ADR-CM-006-Character-Generation.md) |
| **Version** | 1.0 |
| **Status** | Draft |
| **Last Updated** | 2026-02-14 |

---

## Overview

This specification defines the format for character profile files used in Campaign Mode's Phase 2 (Character Setup). Profiles customise how animal agents present and behave within a campaign. The format supports two depth levels, a theme-agnostic design, selective application, and NPC thematic skins.

Profiles are stored as markdown files in `.campaign/profiles/` (see [SPEC-CM-006-B](SPEC-CM-006-B-Campaign-State-Directory.md) for directory structure).

---

## Profile Depth Levels

Users choose one of three options for each animal:

| Depth | Effect | What Changes | What Doesn't Change |
|-------|--------|-------------|-------------------|
| **Vanilla** | No profile | Nothing -- animal uses default archetype | -- |
| **Flavour** | Narrative only | Tone, voice, vocabulary, metaphors | Core behaviours unchanged |
| **Modifier** | Narrative + behavioural tuning | Tone, voice, vocabulary, metaphors + flex behaviour weighting | Core behaviours unchanged |

Users can mix depths across animals -- e.g., Bear at modifier depth, Cat at flavour, and the rest vanilla.

---

## Animal Profile Structure

Profile files are stored at `.campaign/profiles/{animal}.md` where `{animal}` is one of: `bear`, `cat`, `owl`, `puppy`, `rabbit`, `wolf`.

### Frontmatter

```yaml
---
animal: bear
profile-name: "The Visionary Leader"
depth: flavour       # or: modifier
theme: neutral       # or: fantasy, martial-arts, custom, etc.
---
```

| Field | Required | Values | Description |
|-------|----------|--------|-------------|
| `animal` | Yes | bear, cat, owl, puppy, rabbit, wolf | Which animal this profile applies to |
| `profile-name` | Yes | Free text | Display name for this characterisation |
| `depth` | Yes | flavour, modifier | Profile depth level |
| `theme` | Yes | Free text | Theme used (neutral, fantasy, or custom name) |

### Body Sections

#### Character Concept (Required)

A brief narrative description of this characterisation of the animal.

```markdown
## Character Concept
A visionary strategist who sees the long game and inspires others to think beyond immediate constraints. Speaks with calm authority and frames every challenge as a step toward a greater purpose.
```

#### Tone and Voice (Required)

How this character speaks, what metaphors they use, what vocabulary they prefer.

```markdown
## Tone and Voice
- Speaks with calm authority and forward-looking optimism
- Uses strategic/military metaphors: "reconnaissance", "advance", "hold the line"
- Favours decisive language: "Here's what we do", "The path is clear"
- Addresses the party as "team" or "council"
```

#### Behavioural Modifiers (Modifier depth only)

Present only when `depth: modifier`. Defines how the animal's flex behaviours are tuned.

```markdown
## Behavioural Modifiers
- Emphasises long-term vision over short-term wins
- Weights moral clarity higher in decision-making
- More likely to challenge the party to think bigger
- Communicates vision assertively rather than tentatively
```

---

## Core vs Flex Behaviours

Each animal has **core behaviours** (hard constraints, never overridden by any profile) and **flex behaviours** (can be re-weighted by modifier-depth profiles).

### Core Behaviours (Non-Negotiable)

These define the animal's archetype identity. A profile that contradicts a core behaviour is incompatible and must be blocked by Gandalf.

| Animal | Core Behaviours |
|--------|----------------|
| **Bear** | Provides vision and direction |
| **Cat** | Assesses risks and manages scope |
| **Owl** | Tracks timeline, process, progress |
| **Puppy** | Provides morale and spots opportunities |
| **Rabbit** | Identifies resources and facilitates stakeholders |
| **Wolf** | Ensures team cohesion and balanced participation |

### Flex Behaviours (Profile Can Tune)

These aspects of behaviour can be adjusted within archetype bounds.

| Animal | Flex Behaviours |
|--------|----------------|
| **Bear** | How assertively vision is communicated; long-term vs. short-term emphasis |
| **Cat** | How risks are framed (cautious vs. opportunistic); verbosity of risk analysis |
| **Owl** | How strictly process is enforced; tolerance for deviation |
| **Puppy** | Enthusiasm level; balance of optimism vs. realism |
| **Rabbit** | Proactiveness in sourcing; how broadly "resources" is interpreted |
| **Wolf** | How directly imbalances are addressed; conflict tolerance |

### Compatibility Rule

Gandalf enforces a hard constraint: **no profile may negate a core behaviour**. If a user proposes a profile that conflicts with core behaviours, Gandalf warns AND blocks:

> "A Bear without vision isn't Bear. Let's find a characterisation that amplifies Bear's strengths instead."

Gandalf should then guide the user toward a compatible alternative that preserves the archetype while achieving the user's creative intent.

---

## Theme System

Themes are optional overlays that provide vocabulary, metaphors, and suggested profile names. Themes do not alter the profile format -- they inform the content within profiles.

### Built-In Themes

#### Neutral (Default)

Professional, accessible language. Suitable for any context.

| Animal | Suggested Profile Name |
|--------|----------------------|
| Bear | Visionary Leader |
| Cat | Risk Analyst |
| Owl | Timekeeper |
| Puppy | Morale Officer |
| Rabbit | Resource Coordinator |
| Wolf | Team Captain |

#### Fantasy

D&D-inspired characterisations. Opt-in only.

| Animal | Suggested Profile Name |
|--------|----------------------|
| Bear | Human Paladin |
| Cat | Halfling Rogue |
| Owl | Elven Sage |
| Puppy | Gnome Bard |
| Rabbit | Dwarf Artificer |
| Wolf | Half-Orc Warden |

### Custom Themes

Users can create custom themes via Socratic dialogue with Gandalf. Any framing the user wants -- martial arts, sci-fi, culinary, musical, mythological, cultural. Gandalf helps shape theme vocabulary and suggested names through guided conversation.

### Theme Rules

- Themes are **not exhaustive** -- users can mix or create freely
- Neutral defaults ensure broad appeal per Design Principle #3
- A profile's theme is recorded in frontmatter but does not constrain other profiles in the same campaign
- Multiple themes can coexist within a single campaign (e.g., Bear as a Paladin, Cat as a Risk Analyst)

---

## NPC Thematic Skins

NPCs (Gandalf, Dragon, Guardian) can optionally receive light thematic skins that adapt their presentation to match the campaign's theme. NPC skins do **not** alter core NPC behaviour -- they change only presentation, vocabulary, and display name.

### NPC Skin Structure

Skin files are stored at `.campaign/profiles/{npc}.md` where `{npc}` is one of: `gandalf`, `dragon`, `guardian`.

```yaml
---
npc: gandalf
skin-name: "The Sensei"
theme: martial-arts
---
```

| Field | Required | Values | Description |
|-------|----------|--------|-------------|
| `npc` | Yes | gandalf, dragon, guardian | Which NPC this skin applies to |
| `skin-name` | Yes | Free text | Display name replacing the NPC's default name |
| `theme` | Yes | Free text | Theme used for this skin |

### Body Sections

#### Thematic Adaptation (Required)

How the NPC's presentation changes -- metaphors, vocabulary, framing.

```markdown
## Thematic Adaptation
Speaks in martial arts metaphors. "The quest is your dojo." "Face the dragon as you would face a sparring partner -- with respect and full commitment."
```

#### Name (Required)

The display name that replaces the NPC's default name in dialogue.

```markdown
## Name
The Sensei (replaces "Gandalf" in dialogue)
```

### NPC Skin Constraints

- Core NPC behaviour is **never** altered by a skin
- Gandalf's mentoring approach, Dragon's adversarial evaluation, and Guardian's gatekeeping function remain unchanged
- Only presentation layer is affected: vocabulary, metaphors, display name
- Skins are optional -- NPCs can remain unskinned even when animals have profiles

---

## Complete Profile Examples

### Flavour-Depth Animal Profile

```markdown
---
animal: bear
profile-name: "The Visionary Leader"
depth: flavour
theme: neutral
---

# Bear -- The Visionary Leader

## Character Concept
A visionary strategist who sees the long game and inspires others to think beyond immediate constraints. Speaks with calm authority and frames every challenge as a step toward a greater purpose.

## Tone and Voice
- Speaks with calm authority and forward-looking optimism
- Uses strategic/military metaphors: "reconnaissance", "advance", "hold the line"
- Favours decisive language: "Here's what we do", "The path is clear"
- Addresses the party as "team" or "council"
```

### Modifier-Depth Animal Profile

```markdown
---
animal: cat
profile-name: "Halfling Rogue"
depth: modifier
theme: fantasy
---

# Cat -- Halfling Rogue

## Character Concept
A cunning, streetwise rogue who sees every situation as a puzzle to be picked apart. Quick-witted and perceptive, always the first to spot what others miss -- and the first to point out what could go wrong.

## Tone and Voice
- Speaks in quick, clipped observations with dry humour
- Uses thief/heist metaphors: "casing the joint", "the mark", "exit strategy"
- Addresses risks as "traps" and scope as "the take"
- Refers to the party as "the crew"

## Behavioural Modifiers
- Frames risks opportunistically rather than cautiously ("here's how we exploit this")
- Delivers risk analysis concisely -- bullet points, not essays
- More likely to suggest unconventional approaches to scope management
- Weights probability higher than severity in risk assessment
```

### NPC Thematic Skin

```markdown
---
npc: gandalf
skin-name: "The Sensei"
theme: martial-arts
---

# Gandalf -- The Sensei

## Thematic Adaptation
Speaks in martial arts metaphors. "The quest is your dojo." "Face the dragon as you would face a sparring partner -- with respect and full commitment." Frames obstacles as training exercises. "The wall you've hit is not a barrier -- it is a practice dummy. Strike it until you understand its shape."

## Name
The Sensei (replaces "Gandalf" in dialogue)
```

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-006-B](SPEC-CM-006-B-Campaign-State-Directory.md) | Campaign State Directory | Where profile files are stored |
| [SPEC-CM-001-B](SPEC-CM-001-B-Campaign-Lifecycle.md) | Campaign Lifecycle | Phase 2 where profiles are created |
| [SPEC-CM-005-A](SPEC-CM-005-A-Campaign-Mode-Profiles.md) | Campaign Mode Profiles | Mode determines whether Phase 2 is offered |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
