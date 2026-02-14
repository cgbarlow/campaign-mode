# SPEC-CM-006-B: Campaign State Directory

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-006-B |
| **Parent ADR** | [ADR-CM-006](../adrs/ADR-CM-006-Character-Generation.md) |
| **Version** | 1.1 |
| **Status** | Draft |
| **Last Updated** | 2026-02-14 |

---

## Overview

This specification defines the `.campaign/` directory structure used to store campaign state. The directory stores character profile files and the quest definition file (`quest.md`) which tracks campaign mode, success criteria, current phase, and progress log. This specification establishes the directory convention, quest file format, and export protocol.

---

## Directory Structure

```
.campaign/
├── quest.md                    # Quest definition (mode, criteria, narrative, progress log)
└── profiles/                   # Character profiles
    ├── bear.md                 # Animal profile (if profiled)
    ├── cat.md                  # Animal profile (if profiled)
    ├── owl.md                  # Animal profile (if profiled)
    ├── puppy.md                # Animal profile (if profiled)
    ├── rabbit.md               # Animal profile (if profiled)
    ├── wolf.md                 # Animal profile (if profiled)
    ├── gandalf.md              # NPC skin (if themed)
    ├── dragon.md               # NPC skin (if themed)
    └── guardian.md             # NPC skin (if themed)
```

### Directory Location

The `.campaign/` directory lives at the **project root** -- the same level as `.claude/`, `skills/`, and `docs/`. It is created by Gandalf during Phase 2 when the user opts into character profiles.

### File Naming

- Animal profiles: `{animal}.md` where animal is one of `bear`, `cat`, `owl`, `puppy`, `rabbit`, `wolf`
- NPC skins: `{npc}.md` where npc is one of `gandalf`, `dragon`, `guardian`
- All filenames are lowercase, matching the frontmatter identifier

### Partial Profiles

Not all files need to exist. If the user profiles only Bear and Cat, only `bear.md` and `cat.md` appear in `profiles/`. Animals without profiles use their default archetypes. NPCs without skins use their default presentation.

---

## Profile File Format

Profile files follow the format defined in [SPEC-CM-006-A](SPEC-CM-006-A-Character-Profile-Format.md):

- YAML frontmatter with `animal`/`npc`, `profile-name`/`skin-name`, `depth`, and `theme` fields
- Markdown body with character concept, tone and voice, and optionally behavioural modifiers (animals) or thematic adaptation and name (NPCs)

---

## Quest Definition File

### `quest.md`

The quest definition file stores durable campaign state. It is the canonical source of truth for campaign mode, success criteria, quest narrative, and campaign progress. NPC agents read this file rather than relying on conversation context.

### Format

The file uses YAML frontmatter (matching the profile file pattern from [SPEC-CM-006-A](SPEC-CM-006-A-Character-Profile-Format.md)) with a markdown body:

```yaml
---
campaign-mode: Grow & Ship
phase: 3
created: 2026-02-14
---

## Quest Narrative
[Gandalf's framing of the quest — stakes, challenge, invitation]

## Success Criteria
1. [Criterion text as agreed with the user]
2. [Criterion text as agreed with the user]
3. [Criterion text as agreed with the user]

## Anticipated Dragon
[The internal obstacle or resistance the user identified]

## Progress Log
- **Phase 1 complete** — Quest defined (2026-02-14)
- **Phase 2 skipped** — Ship mode (2026-02-14)
- **Guardian checkpoint** — Conditional Approval: "API design is solid but error handling needs work" (2026-02-14)
- **Guardian checkpoint** — Approved (2026-02-14)
- **Dragon confrontation** — Dragon Slain: "All criteria met" (2026-02-14)
```

### Frontmatter Fields

| Field | Type | Description |
|-------|------|-------------|
| `campaign-mode` | String | One of `Grow`, `Ship`, or `Grow & Ship` |
| `phase` | Integer (1–6) | Current campaign phase |
| `created` | Date (ISO 8601) | Date the quest was defined |

### Body Sections

| Section | Description | Written by |
|---------|-------------|------------|
| **Quest Narrative** | Gandalf's framing of the quest | Gandalf (Phase 1) |
| **Success Criteria** | Numbered list of testable criteria | Gandalf (Phase 1) |
| **Anticipated Dragon** | The internal obstacle the user identified | Gandalf (Phase 1) |
| **Progress Log** | Append-only log of phase transitions and NPC verdicts | All NPCs |

### Who Writes What

| Agent | Action | When |
|-------|--------|------|
| **Gandalf** | Creates `quest.md` with all sections | End of Phase 1 |
| **Gandalf** | Updates `phase`, appends Phase 2 log entry | End of Phase 2 (or skip) |
| **Guardian** | Appends checkpoint result to Progress Log | After delivering verdict |
| **Dragon** | Appends confrontation result to Progress Log, updates `phase` | After delivering verdict |

### Progress Log Entry Formats

- Phase transitions: `- **Phase N complete** — [description] ([date])`
- Guardian checkpoint: `- **Guardian checkpoint** — {Approved|Blocked|Conditional Approval}: "[brief summary]" ([date])`
- Dragon confrontation: `- **Dragon confrontation** — {Dragon Slain|Dragon Prevails}: "[brief reason]" ([date])`

### Lifecycle

1. File does not exist before Phase 1
2. Gandalf creates the file at the end of Phase 1 (quest definition complete)
3. File is read by `/continue-quest` to reconstruct campaign context
4. Guardian and Dragon read the file for success criteria and campaign mode
5. Guardian and Dragon append to the Progress Log after delivering verdicts
6. File persists after campaign completion as a record of the quest

---

## Export Protocol

### User-Managed Export

Users can copy `.campaign/profiles/` to reuse profiles in future campaigns. The system does **not** manage a roster -- this is the user's responsibility.

```bash
# Save profiles for reuse
cp -r .campaign/profiles/ ~/my-saved-profiles/quest-name/

# Reuse profiles in a new campaign
cp -r ~/my-saved-profiles/quest-name/ .campaign/profiles/
```

### Export Scope

- Profiles are **per-campaign** -- they reflect the characterisations chosen for a specific quest
- Profiles are **self-contained** -- each file contains all information needed to reconstitute the characterisation
- Profiles have **no external dependencies** -- they do not reference campaign state, quest definitions, or other profiles

### Import Behaviour

When a user copies profiles into a new campaign's `.campaign/profiles/` directory:
- Gandalf should recognise existing profiles during Phase 2 and offer to use them as-is or modify them
- Existing profiles do not bypass the compatibility check -- Gandalf still validates against core behaviours
- The user retains full agency to accept, modify, or discard imported profiles

---

## Gitignore Considerations

The `.campaign/` directory contains user-generated campaign state. Projects should consider whether to track it in version control:

- **Track** if the campaign is a shared team activity and profiles should be version-controlled
- **Ignore** if the campaign is personal or experimental

This is a user decision -- Gandalf does not manage `.gitignore` entries.

---

## Scope Boundary

### In Scope

- `.campaign/profiles/` directory for character profile storage
- Profile file naming convention
- `quest.md` creation by Gandalf, read/append by Guardian and Dragon
- Campaign progress tracking via append-only Progress Log
- Export protocol (user-managed copy)
- Import recognition by Gandalf

### Out of Scope (Deferred)

- Automated export/import tooling
- Campaign archival or history
- Multi-quest campaign arcs

This specification resolves Open Question #5 (State Management) from the north-star. Campaign state is persisted in `.campaign/quest.md` and profiles in `.campaign/profiles/`.

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-006-A](SPEC-CM-006-A-Character-Profile-Format.md) | Character Profile Format | Format of files stored in this directory |
| [SPEC-CM-001-A](SPEC-CM-001-A-Skill-Architecture.md) | Skill Architecture | Parallel directory convention (.claude/ for skills, .campaign/ for state) |
| [SPEC-CM-001-B](SPEC-CM-001-B-Campaign-Lifecycle.md) | Campaign Lifecycle | Phase 2 where profiles are created and stored |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.1 | 2026-02-14 | Chris Barlow | Added quest.md format specification, progress log, NPC read/write protocol. Moved quest.md from reserved to fully specified. Resolved Open Question #5. |
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
