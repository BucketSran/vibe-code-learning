# Maintaining Vibe Code Learning

This repository is also an installed skill. `SKILL.md` is the runtime entry point; personal configuration and learner notes live outside the repository.

For a skill behavior change, record the concrete change and reason under `Unreleased` in `CHANGELOG.md`, and exercise the affected learning scenario. Documentation-only edits need link and diff checks rather than a full behavioral trial.

When publishing a release, choose a new version, update `metadata.version` in `SKILL.md`, move the corresponding changelog entries into a dated release section, and keep the annotated tag `vX.Y.Z` and GitHub Release consistent. Check the packaged files and internal links. Preserve old tags so users can restore them; undo published mistakes with a new commit or release rather than rewriting history.

Before staging files, confirm that no personal configuration, vault contents, learner profiles, chat transcripts, machine-specific paths, or credentials are included. Validation summaries may describe synthetic cases without copying private artifacts.

Use the currently selected model and available native tools. A new release does not require a fixed number of agents or test cases; choose checks for the changed behavior and report untested paths honestly.
