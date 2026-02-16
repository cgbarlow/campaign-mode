# SPEC-CM-009-A: Profile Pack Format

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-009-A |
| **Parent ADR** | [ADR-CM-016](../2_adrs/ADR-CM-016-Profile-Packs.md) |
| **Version** | 1.0 |
| **Status** | Draft |
| **Last Updated** | 2026-02-16 |

---

## Overview

This specification defines the format for profile packs — pre-built, complete sets of character profiles that can be installed as a group during Campaign Mode's Phase 2 (Character Setup). Profile packs provide instant theme installation, removing the need for users to create 9 individual profiles from scratch.

Profile packs are stored in the Campaign Mode repository under `profile-packs/` and are selectable during Gandalf's Phase 2 flow.

---

## Directory Structure

```
profile-packs/
└── {theme-name}/
    ├── bear.md
    ├── cat.md
    ├── owl.md
    ├── puppy.md
    ├── rabbit.md
    ├── wolf.md
    ├── gandalf.md
    ├── guardian.md
    └── dragon.md
```

### Naming Conventions

- **Pack directory name** (`{theme-name}`): Lowercase, hyphen-separated. Must be descriptive and unique within the repository. Examples: `fantasy`, `hundred-acre-wood`, `martial-arts`, `sci-fi`.
- **Profile file names**: Must match the archetype name exactly: `bear.md`, `cat.md`, `owl.md`, `puppy.md`, `rabbit.md`, `wolf.md`, `gandalf.md`, `guardian.md`, `dragon.md`.

---

## Profile File Requirements

Each profile file in a pack must follow [SPEC-CM-006-A v1.1](SPEC-CM-006-A-Character-Profile-Format.md):

### Required Frontmatter

```yaml
---
archetype: bear
skin-name: "The Paladin"
theme: "Fantasy"
---
```

- `archetype` must match the file name (without `.md`)
- `skin-name` is the display name for this characterisation
- `theme` must match the pack's theme name (title case or natural form)

### Required Body Sections

- **Character Concept** (or **Thematic Adaptation**) — narrative description
- **Tone and Voice** (or **Voice and Manner**) — speech patterns, metaphors, vocabulary

### Optional Body Sections

- **Behavioural Modifiers** (or **Behavioural Tweaks**) — flex behaviour tuning (animal profiles only)
- **Name** — display name for NPC profiles (redundant with `skin-name` but acceptable)

---

## Pack Completeness

### Complete Packs (Required for v1)

All profile packs must include all 9 profiles — 6 animal agents and 3 NPC agents. This ensures that installing a pack provides a fully themed campaign experience.

| Archetype | Agent Type | Required |
|-----------|-----------|----------|
| bear | Animal | Yes |
| cat | Animal | Yes |
| owl | Animal | Yes |
| puppy | Animal | Yes |
| rabbit | Animal | Yes |
| wolf | Animal | Yes |
| gandalf | NPC | Yes |
| guardian | NPC | Yes |
| dragon | NPC | Yes |

### Coherence Requirements

A pack should feel like a cohesive themed set:

- All profiles share a consistent thematic vocabulary
- No two characters are too similar in name, tone, or personality
- Each character's distinctiveness maps to the archetype's distinctiveness
- NPC skins adapt presentation to the theme without altering core NPC roles

---

## Pack Installation

When a user selects a pack during Phase 2, Gandalf installs it by copying all profile files from `profile-packs/{theme-name}/` to `.campaign/profiles/`.

### Installation Process

1. Read all `.md` files from the selected pack directory
2. Copy each file to `.campaign/profiles/{archetype}.md`
3. Display the installed character table (archetype → skin-name mapping)
4. Offer the user the option to customise individual profiles further

### Path Resolution

Pack directories are resolved relative to the Campaign Mode plugin root. The plugin root is determined by the path resolution rules in [SPEC-CM-007-C](SPEC-CM-007-C-Plugin-Path-Resolution.md).

---

## Built-In Packs

Campaign Mode ships with the following packs:

| Pack | Directory | Description |
|------|-----------|-------------|
| **Fantasy** | `profile-packs/fantasy/` | D&D-inspired characterisations: Paladin, Rogue, Sage, Bard, Artificer, Warden + Archmage, Sentinel, Ancient Wyrm |
| **Hundred Acre Wood** | `profile-packs/hundred-acre-wood/` | Winnie-the-Pooh inspired: Pooh, Eeyore, Owl, Tigger, Rabbit, Piglet + Christopher Robin, Kanga, Heffalump |

---

## Contributing a New Pack

Community members can submit new profile packs via pull request. See [CONTRIBUTING.md](../../CONTRIBUTING.md) for the full process.

### Submission Requirements

1. **Complete set** — All 9 profiles (6 animals + 3 NPCs)
2. **SPEC-CM-006-A v1.1 compliant** — Unified frontmatter, required body sections
3. **Thematically coherent** — Pack feels like a unified set, not 9 unrelated profiles
4. **Core behaviours preserved** — No profile contradicts an animal's core behaviour or an NPC's core role
5. **Original or licensed content** — Contributions must be compatible with CC-BY-SA-4.0

### Submission Process

1. Fork the Campaign Mode repository
2. Create a new directory under `profile-packs/` with your theme name
3. Add all 9 profile files following the format above
4. Open a pull request with a description of the theme and its creative intent

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-006-A](SPEC-CM-006-A-Character-Profile-Format.md) | Character Profile Format (v1.1) | Format that all pack profiles must follow |
| [SPEC-CM-006-B](SPEC-CM-006-B-Campaign-State-Directory.md) | Campaign State Directory | Where installed profiles are stored |
| [SPEC-CM-001-B](SPEC-CM-001-B-Campaign-Lifecycle.md) | Campaign Lifecycle | Phase 2 where packs are installed |
| [SPEC-CM-007-C](SPEC-CM-007-C-Plugin-Path-Resolution.md) | Plugin Path Resolution | How pack directories are located |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-16 | Chris Barlow | Initial specification |
