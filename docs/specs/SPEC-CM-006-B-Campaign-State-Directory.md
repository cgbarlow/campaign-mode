# SPEC-CM-006-B: Campaign State Directory

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-006-B |
| **Parent ADR** | [ADR-CM-006](../adrs/ADR-CM-006-Character-Generation.md) |
| **Version** | 1.0 |
| **Status** | Draft |
| **Last Updated** | 2026-02-14 |

---

## Overview

This specification defines the `.campaign/` directory structure used to store campaign state. In v1, the directory stores character profile files only. Full state management (quest progress, checkpoint status, etc.) is deferred -- this specification establishes the directory convention and export protocol.

---

## Directory Structure

```
.campaign/
├── quest.md                    # Quest definition (mode, criteria, narrative) — reserved, not yet specified
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

## Reserved Files

### `quest.md`

Reserved for future use. When implemented, `quest.md` will store the quest definition including:
- Campaign mode selection (Grow / Ship / Grow & Ship)
- Quest narrative and framing
- Success criteria
- Anticipated dragon (internal obstacle)

This file is **not** created or managed in v1. Its inclusion in the directory structure is forward-looking.

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

### In Scope (v1)

- `.campaign/profiles/` directory for character profile storage
- Profile file naming convention
- Export protocol (user-managed copy)
- Import recognition by Gandalf

### Out of Scope (Deferred)

- `quest.md` creation and management
- Checkpoint state persistence
- Campaign progress tracking
- Automated export/import tooling
- Campaign archival or history

This specification partially resolves Open Question #5 (State Management) from the north-star by establishing the directory convention. Full state management remains an open question.

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
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
