# Contributing to Campaign Mode

Thank you for your interest in Campaign Mode! This project welcomes contributions of all kinds — bug reports, feature ideas, character profiles, campaign experiences, and documentation improvements.

## How to Contribute

### Bug Reports

Found something that doesn't work as documented? [Open a bug report](https://github.com/cgbarlow/campaign-mode/issues/new?template=bug-report.md) with:
- What you expected to happen
- What actually happened
- Your Claude Code version and installation method

### Feature Requests

Have an idea for improving Campaign Mode? [Open a feature request](https://github.com/cgbarlow/campaign-mode/issues/new?template=feature-request.md) describing the problem you're trying to solve and your proposed approach.

### Character Profiles

Created a character profile you'd like to share? [Submit a profile](https://github.com/cgbarlow/campaign-mode/issues/new?template=profile-submission.md) following the [SPEC-CM-006-A](docs/3_specs/SPEC-CM-006-A-Character-Profile-Format.md) format. Profiles can be any theme — fantasy, sci-fi, culinary, martial arts, or anything else.

### Profile Packs

A profile pack is a complete set of 9 character profiles (6 animals + 3 NPCs) that can be installed as a group during Phase 2. To submit a new pack:

1. Fork the repository
2. Create a new directory under `profile-packs/` with your theme name (lowercase, hyphen-separated)
3. Add all 9 profile files (`bear.md`, `cat.md`, `owl.md`, `puppy.md`, `rabbit.md`, `wolf.md`, `gandalf.md`, `guardian.md`, `dragon.md`)
4. Each profile must follow [SPEC-CM-006-A v1.1](docs/3_specs/SPEC-CM-006-A-Character-Profile-Format.md) unified frontmatter format
5. Ensure the set is thematically coherent — it should feel like a unified cast
6. Open a pull request with a description of the theme and its creative intent

See [SPEC-CM-009-A](docs/3_specs/SPEC-CM-009-A-Profile-Pack-Format.md) for the full pack format specification.

### Campaign Experiences

Run a campaign and want to share what worked (or didn't)? Open an issue describing your experience. Real-world campaign feedback is invaluable for improving the quest flow, NPC behaviour, and proactive elicitation.

### Code and Documentation

1. Fork the repository
2. Create a feature branch (`git checkout -b my-contribution`)
3. Make your changes
4. Commit with a clear message describing what and why
5. Open a pull request

## Guidelines

- **Keep it focused.** One contribution per pull request.
- **Follow existing patterns.** Match the style and structure of existing files.
- **Respect the architecture.** Core behaviours are non-negotiable. Profiles tune flex behaviours only. See [CLAUDE.md](CLAUDE.md) for the full guidelines.
- **Test with a real campaign.** If your change affects NPC behaviour or quest flow, run through at least one quest lifecycle to verify.

## Licensing

By contributing to Campaign Mode, you agree that your contributions will be licensed under [CC-BY-SA-4.0](LICENSE). This is a content project — all contributions (profiles, documentation, skill definitions) fall under the same Creative Commons license.

## Questions?

Open an issue at [github.com/cgbarlow/campaign-mode/issues](https://github.com/cgbarlow/campaign-mode/issues) or start a discussion.
