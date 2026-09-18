# Vibe Code Learning

A Codex skill for learning to understand, navigate, and change code while working on real projects with AI.

Start with a project map, follow one input through the execution flow, and connect each PR change to its files, functions, verified line numbers, and commit versions. Retain what the learner actually demonstrated across sessions.

Change explanations include focused actual diff hunks with before/after behavior. For missing Git history or unsynchronized copies, the skill can compare provenance-labeled snapshots and help establish scoped future checkpoints; see [diff learning](references/diff-learning.md).

The skill instructions are in English. Lessons and notes follow the user's language.

## Modes

| Mode | What happens |
| --- | --- |
| Explain | Map the relevant project structure, trace behavior, and explain the change with code references and a useful diagram. |
| Test | Ask a focused question and wait for the learner's answer without revealing the solution. |
| Feedback | Check the learner's actual reasoning, correct misconceptions, and update only supported learning evidence. |

Mermaid or simple text diagrams work without additional skills. For larger interactive diagrams, the skill can use an installed `archify` skill. The reading route draws on the whole-project-to-main-chain approach of `article-close-reading` and the module/caller perspective of `zoom-out`; neither is required.

## Install

For a new installation, clone the released version into your Codex skills directory:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
git clone --branch v0.1.7 https://github.com/BucketSran/vibe-code-learning.git \
  "${CODEX_HOME:-$HOME/.codex}/skills/vibe-code-learning"
```

This checks out the release in detached-HEAD mode. If the destination already exists, inspect it before replacing or updating anything. The entry point is [SKILL.md](SKILL.md).

## Use

In a project conversation, identify the PR, commit comparison, or local change:

> Use $vibe-code-learning to explain this PR. Start with the project flow, show the changed files and functions, adapt to my learning history, and save a review note.

> 用 $vibe-code-learning 带我理解这个 PR，先画流程，再解释代码改动，保存到 Obsidian。

To check understanding afterward:

> Use $vibe-code-learning to test my understanding of this change. Ask first, wait for my answer, and do not reveal the solution yet.

The learning check complements the project's software tests. It does not claim the learner can independently modify code just because they read an explanation or gave a correct verbal answer.

## Optional persistent memory

Without configured storage, the skill can still explain code. To remember learning across sessions, configure an existing Obsidian vault and a learner profile following [the memory reference](references/memory.md).

The default configuration lives outside this repository:

```text
$CODEX_HOME/skill-state/vibe-code-learning/config.json
```

When `CODEX_HOME` is unset, the default base is `~/.codex`. An explicitly selected configuration takes precedence. Personal profiles, chat excerpts, local paths, and learning notes belong in private user storage, not this public repository.

Memory is read and updated when the skill is used; there is no background service. Current instructions such as “do not save this session” override previous saving preferences. Existing notes establish exposure, not mastery.

The profile's active context stays small; detailed concept records and original session evidence are retrieved by topic. Explanation, navigation, and modification are tracked separately. Existing schema-version-1 configurations keep working: oversized profiles can gain a short active section without deleting their older records or rewriting the learner's words.

Code links follow their destination: host-native links in chat, and the user's chosen editor or a suitable source/file link in notes. Installed software does not silently become a stored preference. Historical citations keep their original revision even when the live checkout moves.

To practice a concept, ask for a small coding exercise. The skill waits for your attempt and checks the actual edit; optional practice does not interrupt an otherwise requested implementation. Later relevant sessions can revisit an unresolved gap with a fresh example.

## Versions, updates, and rollback

[CHANGELOG.md](CHANGELOG.md) records released changes. Each published version has an annotated Git tag and a [GitHub Release](https://github.com/BucketSran/vibe-code-learning/releases). Existing release tags should remain fixed.

First inspect local changes:

```bash
git -C "${CODEX_HOME:-$HOME/.codex}/skills/vibe-code-learning" status --short
```

Preserve any local edits before switching versions. To return to the first public release:

```bash
git -C "${CODEX_HOME:-$HOME/.codex}/skills/vibe-code-learning" fetch origin --tags
git -C "${CODEX_HOME:-$HOME/.codex}/skills/vibe-code-learning" switch --detach v0.1.1
```

To follow the latest published repository work again:

```bash
git -C "${CODEX_HOME:-$HOME/.codex}/skills/vibe-code-learning" switch main
git -C "${CODEX_HOME:-$HOME/.codex}/skills/vibe-code-learning" pull --ff-only
```

Switching skill versions does not roll back the learner's external notes or profile. If a future version changes the memory format, its release notes must describe compatibility and any migration.

## Maintaining a release

1. Make a focused change and record its behavior and reason in the changelog.
2. Update `metadata.version` in `SKILL.md` for a new release. Keep it consistent with the changelog and `vX.Y.Z` tag; document-only commits can remain unreleased.
3. Validate the skill format and links, then run the scenarios affected by the change. [Validation notes](docs/validation.md) describe the initial trials and their limits.
4. Commit the change, create a new annotated tag, and publish a release for that tag. Do not overwrite an older release tag or rewrite published history to undo a change; create a new fix or use `git revert`.

Personal memory stays outside versioned skill files. There is no need to rerun unrelated scenarios for a documentation-only change.

Design references and adaptation choices are recorded in [design notes](docs/design-notes.md).
