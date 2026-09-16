# Changelog

Release versions match `metadata.version` in `SKILL.md` and the corresponding `vX.Y.Z` Git tag.

## Unreleased

No changes recorded yet.

## 0.1.1 — 2026-09-16

First public release, based on the locally developed and tested skill.

### Added

- Explain, Test, and Feedback modes for learning from repositories and PRs.
- Project maps, execution journeys, diagrams, and version-specific file/function/line references.
- Per-learner memory and optional Obsidian notes, with user configuration outside the skill package.
- Evidence-based learning states, preservation of original learner reasoning, and safe continuation when storage is unavailable.
- Repository documentation for installation, release history, updates, and rollback.

### Fixed during local trials

- Clarified prediction questions so that a prompt does not both tell the learner to run a command and ask them not to run it.

### Validation

- Four isolated behavioral scenarios and one targeted follow-up were completed: PR explanation, answer-free testing, feedback/memory correction, unavailable storage, and prediction wording with a no-save request.
- Skill format and internal references were checked. See [validation notes](docs/validation.md) for the scope and remaining gaps.

The earlier 0.1.0 local prototype was not published as a Git release. Repository history begins with 0.1.1; this changelog does not imply a recoverable 0.1.0 tag.
