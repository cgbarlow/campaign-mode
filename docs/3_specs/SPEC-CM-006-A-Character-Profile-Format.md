# SPEC-CM-006-A: Character Profile Format

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-006-A |
| **Parent ADR** | [ADR-CM-006](../2_adrs/ADR-CM-006-Character-Generation.md) |
| **Version** | 1.1 |
| **Status** | Draft |
| **Last Updated** | 2026-02-16 |

---

## Overview

This specification defines the format for character profile files used in Campaign Mode's Phase 2 (Character Setup). Profiles customise how animal and NPC agents present and behave within a campaign. The format uses a unified frontmatter structure for all agent types, supports two depth levels, a theme-agnostic design, selective application, and NPC thematic skins.

Profiles are stored as markdown files in `.campaign/profiles/` (see [SPEC-CM-006-B](SPEC-CM-006-B-Campaign-State-Directory.md) for directory structure). Profile packs (pre-built theme sets) are stored in `profile-packs/{theme-name}/` (see [SPEC-CM-009-A](SPEC-CM-009-A-Profile-Pack-Format.md) for pack format).

---

## Profile Depth Levels

Users choose one of three options for each animal:

| Depth | Effect | What Changes | What Doesn't Change |
|-------|--------|-------------|-------------------|
| **Vanilla** | No profile | Nothing -- animal uses default archetype | -- |
| **Flavour** | Narrative only | Tone, voice, vocabulary, metaphors | Core behaviours unchanged |
| **Modifier** | Narrative + behavioural tuning | Tone, voice, vocabulary, metaphors + flex behaviour weighting | Core behaviours unchanged |

Users can mix depths across animals -- e.g., Bear at modifier depth, Cat at flavour, and the rest vanilla.

Depth is inferred from content: profiles containing a behavioural modifiers section are modifier depth; those without are flavour depth. No explicit `depth` field is required in frontmatter.

---

## Unified Profile Structure

All agent profiles -- animal agents (bear, cat, owl, puppy, rabbit, wolf) and NPC agents (gandalf, dragon, guardian) -- use the same frontmatter format and file structure.

Profile files are stored at `.campaign/profiles/{archetype}.md` where `{archetype}` is one of: `bear`, `cat`, `owl`, `puppy`, `rabbit`, `wolf`, `gandalf`, `dragon`, `guardian`.

### Frontmatter

```yaml
---
archetype: bear
skin-name: "The Paladin"
theme: "Fantasy"
---
```

| Field | Required | Values | Description |
|-------|----------|--------|-------------|
| `archetype` | Yes | bear, cat, owl, puppy, rabbit, wolf, gandalf, dragon, guardian | Which agent this profile applies to |
| `skin-name` | Yes | Free text | Display name for this characterisation |
| `theme` | Yes | Free text | Theme this profile belongs to (e.g., "Fantasy", "Hundred Acre Wood", "Neutral") |

### Body Sections

#### Character Concept (Required)

A brief narrative description of this characterisation of the agent. For NPC agents, this describes how the NPC's presentation adapts to the theme.

```markdown
## Character Concept
A steadfast holy warrior who sees the quest as a sacred charge. The Paladin frames every challenge as a test of conviction and every decision as an oath to be honoured.
```

Accepted section names: `Character Concept`, `Thematic Adaptation`.

#### Tone and Voice (Required)

How this character speaks, what metaphors they use, what vocabulary they prefer.

```markdown
## Tone and Voice
- Speaks with solemn conviction and measured authority
- Uses chivalric and martial metaphors: "hold the line", "this is our sworn path"
- Addresses the party as "companions" or "the order"
```

Accepted section names: `Tone and Voice`, `Voice and Manner`.

#### Behavioural Modifiers (Optional — defines modifier depth)

Present when the profile tunes flex behaviours. The presence of this section elevates the profile from flavour depth to modifier depth.

```markdown
## Behavioural Modifiers
- Frames risks opportunistically rather than cautiously
- Delivers risk analysis concisely — bullet points, not essays
- Weights probability higher than severity in risk assessment
```

Accepted section names: `Behavioural Modifiers`, `Behavioural Tweaks`.

#### Name (Optional — NPC profiles)

For NPC profiles, specifies the display name that replaces the NPC's default name in dialogue.

```markdown
## Name
The Archmage (replaces "Gandalf" in dialogue)
```

This section is optional because `skin-name` in frontmatter serves the same purpose. If present, it must match `skin-name`.

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

### NPC Core Roles (Non-Negotiable)

NPC agents have fixed core roles that profiles cannot alter:

| NPC | Core Role |
|-----|-----------|
| **Gandalf** | Mentors without rescuing |
| **Dragon** | Evaluates adversarially but fairly |
| **Guardian** | Gates progression based on quality |

Profiles change NPC presentation only: vocabulary, metaphors, display name.

### Compatibility Rule

Gandalf enforces a hard constraint: **no profile may negate a core behaviour**. If a user proposes a profile that conflicts with core behaviours, Gandalf warns AND blocks:

> "A Bear without vision isn't Bear. Let's find a characterisation that amplifies Bear's strengths instead."

Gandalf should then guide the user toward a compatible alternative that preserves the archetype while achieving the user's creative intent.

---

## Theme System

Themes are optional overlays that provide vocabulary, metaphors, and suggested profile names. Themes do not alter the profile format -- they inform the content within profiles. Complete theme sets can be distributed as profile packs (see [SPEC-CM-009-A](SPEC-CM-009-A-Profile-Pack-Format.md)).

### Built-In Themes

#### Neutral (Default)

Professional, accessible language. Suitable for any context.

| Archetype | Suggested Skin Name |
|-----------|---------------------|
| Bear | Visionary Leader |
| Cat | Risk Analyst |
| Owl | Timekeeper |
| Puppy | Morale Officer |
| Rabbit | Resource Coordinator |
| Wolf | Team Captain |

#### Fantasy

D&D-inspired characterisations. Available as a profile pack in `profile-packs/fantasy/`.

| Archetype | Suggested Skin Name |
|-----------|---------------------|
| Bear | The Paladin |
| Cat | The Rogue |
| Owl | The Sage |
| Puppy | The Bard |
| Rabbit | The Artificer |
| Wolf | The Warden |
| Gandalf | The Archmage |
| Dragon | The Ancient Wyrm |
| Guardian | The Sentinel |

#### Hundred Acre Wood

Winnie-the-Pooh inspired characterisations. Available as a profile pack in `profile-packs/hundred-acre-wood/`.

| Archetype | Suggested Skin Name |
|-----------|---------------------|
| Bear | Pooh |
| Cat | Eeyore |
| Owl | Owl |
| Puppy | Tigger |
| Rabbit | Rabbit |
| Wolf | Piglet |
| Gandalf | Christopher Robin |
| Dragon | Heffalump |
| Guardian | Kanga |

### Custom Themes

Users can create custom themes via Socratic dialogue with Gandalf. Any framing the user wants -- martial arts, sci-fi, culinary, musical, mythological, cultural. Gandalf helps shape theme vocabulary and suggested names through guided conversation.

### Theme Rules

- Themes are **not exhaustive** -- users can mix or create freely
- Neutral defaults ensure broad appeal per Design Principle #3
- A profile's theme is recorded in frontmatter but does not constrain other profiles in the same campaign
- Multiple themes can coexist within a single campaign (e.g., Bear as a Paladin, Cat as a Risk Analyst)

---

## Complete Profile Examples

### Flavour-Depth Animal Profile

```markdown
---
archetype: bear
skin-name: "The Paladin"
theme: "Fantasy"
---

# Bear — The Paladin

## Character Concept

A steadfast holy warrior who sees the quest as a sacred charge. The Paladin frames every challenge as a test of conviction and every decision as an oath to be honoured. Where Bear provides vision and direction, the Paladin wraps that vision in the language of duty, honour, and unwavering purpose.

## Tone and Voice

- Speaks with solemn conviction and measured authority
- Uses chivalric and martial metaphors: "hold the line", "this is our sworn path", "we do not retreat from what is right"
- Frames goals as oaths: "We have pledged to deliver this. An oath broken is a quest failed."
- Addresses the party as "companions" or "the order"
- Delivers hard truths with compassion: "The path ahead is steep, but I would not lead you somewhere I would not walk myself"
```

### Modifier-Depth Animal Profile

```markdown
---
archetype: cat
skin-name: "The Rogue"
theme: "Fantasy"
---

# Cat — The Rogue

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

### NPC Profile

```markdown
---
archetype: gandalf
skin-name: "The Archmage"
theme: "Fantasy"
---

# Gandalf — The Archmage

## Character Concept

An ancient archmage who has guided countless adventuring parties through perilous quests. Speaks in the language of high fantasy — spells, prophecies, and ancient wisdom. Where Gandalf mentors without rescuing, the Archmage frames that mentorship as the passing of arcane knowledge from master to apprentice.

## Tone and Voice

- Speaks with gravitas and mystical authority
- Uses magical metaphors: "the threads of fate", "your spell is not yet complete", "the arcane path reveals itself to those who walk it"
- Frames the quest as a prophecy being fulfilled
- Addresses the party as "adventurers" or "seekers"
```

---

## Migration from v1.0

Profiles using the v1.0 format remain readable. When encountered, agents should interpret them as follows:

| v1.0 Field | v1.1 Equivalent | Notes |
|------------|-----------------|-------|
| `animal` | `archetype` | Same values for animal agents |
| `npc` | `archetype` | Same values for NPC agents |
| `profile-name` | `skin-name` | Identical semantics |
| `depth` | *(inferred)* | Presence of Behavioural Modifiers section = modifier; absence = flavour |

New profiles should use v1.1 format exclusively.

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-006-B](SPEC-CM-006-B-Campaign-State-Directory.md) | Campaign State Directory | Where profile files are stored |
| [SPEC-CM-001-B](SPEC-CM-001-B-Campaign-Lifecycle.md) | Campaign Lifecycle | Phase 2 where profiles are created |
| [SPEC-CM-005-A](SPEC-CM-005-A-Campaign-Mode-Profiles.md) | Campaign Mode Profiles | Mode determines whether Phase 2 is offered |
| [SPEC-CM-009-A](SPEC-CM-009-A-Profile-Pack-Format.md) | Profile Pack Format | How complete theme sets are packaged |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
| 1.1 | 2026-02-16 | Chris Barlow | Unified frontmatter (`archetype`/`skin-name`/`theme`) for all agent types. Dropped explicit `depth` field (inferred from content). Relaxed body section naming. Added NPC profiles to examples. Added migration guide from v1.0. Added Hundred Acre Wood theme. Added profile pack cross-references. |
