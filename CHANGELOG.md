# Changelog

Release versions match `metadata.version` in `SKILL.md` and the corresponding `vX.Y.Z` Git tag.

## 0.1.6 — 2026-09-17

### Changed

- Code references in learning notes now emit clickable Markdown links; in note environments a bare absolute path is not clickable.
- URI scheme is chosen by target editor: prefer `vscode://file/<path>:<line>` (opens VS Code at the cited line); `file:///` is the fallback. One-time interactive editor detection with a single install suggestion; the choice is recorded in the learner profile.
- Deep-link the cited file and line instead of a parent directory; repo-root links are reserved for project maps.

### Added

- Token-budget memory design: the profile centers on a fixed-shape concept index (one row per concept, updated in place); the agent restores context from the index only, session notes are for the human; rolling compression folds mastered-and-dormant concepts into archived one-liners; updates are targeted deltas, never full regenerations; the profile targets roughly a page (~1500 tokens).
- Save-time line-number re-verification: code moves between first inspection and the final note edit, so every emitted `path:line` is re-checked before saving; prefer symbol anchors when drift is likely.

## 0.1.2 – 0.1.3 — 2026-09-16

- Added diff-led explanations so learners can see actual removed/added code beside behavioral changes instead of navigating only to the final source.
- Added comparison guidance for PRs, staged/unstaged/untracked changes, non-Git snapshots and unsynchronized local/remote copies, including provenance and missing-baseline limits.
- Added scoped Git checkpoint assistance without implicitly changing live history, the index or remote repositories; learning records now retain diff identities and links.

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
