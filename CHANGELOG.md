# Changelog

Release versions match `metadata.version` in `SKILL.md` and the corresponding `vX.Y.Z` Git tag.

## 0.1.7 — 2026-09-18

### Fixed

- Replaced the growing always-read concept index with bounded active context and topic-specific retrieval. Large legacy profiles can keep their original text while adding a small active section.
- Preserved full evidence, unresolved gaps, and independent ability dimensions during archival; age no longer implies mastery or gap removal.
- Selected code links by output surface and actual user preference instead of treating an installed editor as a chosen editor. Kept historical citations separate from live navigation when lines drift.
- Updated the default installation example to the new release; retained the first-release rollback example.

### Added

- Lightweight gap classification and relevant-session revisits, recording actual assistance and evidence without mandatory quizzes or background reminders.
- Optional small coding exercises in an isolated or explicitly selected practice location, with modification ability grounded in the user's edit and executed checks.
- Dedicated code-link reference and compatibility guidance for existing schema-version-1 memory.

### Validation

- Exercised legacy-memory continuation, versioned links with a temporary editor override, optional coding practice and feedback, and a fresh-context recall question with no note writes.
- Initial trials exposed a dependency error: reading the memory reference and the full legacy profile in parallel. Clarified the entrypoint ordering, then verified selective cold-start retrieval in a fresh agent trial.
- Verified preservation of 1000 legacy concept rows and original learner notes, source snapshot bytes, unchanged source/config state where required, and package format/internal links. See [validation notes](docs/validation.md).

### Compatibility

- No configuration schema change or forced note migration. Existing profile paths and learner-authored records remain valid; optional active sections provide selective access to large legacy profiles.
- Skill rollback does not undo external note updates. No real learner memory was migrated during release validation.

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
