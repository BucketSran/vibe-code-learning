# Learning from Diffs and Incomplete History

Use for explaining an actual change or helping the user make versions comparable. Keep this a learning aid; do not turn every explanation into repository migration or Git training.

## Identify the comparison before choosing a command

Inspect repository root, status, and relevant history without changing them. Name the intended baseline and candidate and resolve available commit IDs. Scope inspection to the relevant files; diffs and untracked files may contain secrets or unrelated work.

| Question | Comparison |
| --- | --- |
| What changed between two exact revisions? | `git diff --no-ext-diff --no-textconv BASE HEAD -- path` |
| What does this PR introduce? | Verify the PR base/head and merge base; use the PR's actual comparison, commonly `git diff --no-ext-diff --no-textconv BASE...HEAD -- path`. Record the merge-base ID as well as base/head. |
| What is not staged? | `git diff --no-ext-diff --no-textconv -- path` (index to working tree) |
| What is staged? | `git diff --no-ext-diff --no-textconv --cached -- path` (HEAD to index) |
| What is the total tracked local change? | `git diff --no-ext-diff --no-textconv HEAD -- path` (HEAD to working tree) |
| What are the differences between two saved trees/files? | `git diff --no-ext-diff --no-textconv --no-index -- before after` |

These are command patterns: substitute verified refs and quote actual paths. Ordinary tracked diffs omit untracked files; inspect relevant candidates from `git ls-files --others --exclude-standard`, without automatically staging them. In a repository with no first commit, HEAD comparisons are unavailable; label the state instead of inventing a baseline. For no-index diff, exit 0 means equal, 1 means differences, and other exits are errors, not a failed experiment merely because changes exist.

`BASE..HEAD` compares two endpoint trees; `BASE...HEAD` compares the merge base to HEAD. Do not swap them silently. Working-tree timestamps and branch names alone are not immutable identities.

## Show a readable learning view

In Explain mode:

1. Give a small file/change map (`--stat` or `--name-status` can help), tied to the execution flow.
2. Show representative **actual** hunks for the substantive behaviors the user is learning. Explain that `-` is removed/base content, `+` is added/candidate content, and other lines are context. Explain `@@` old/new locations only if useful. Avoid mechanically pasting every changed line.
3. Immediately connect each hunk to one concrete input and its before/after outcome. Distinguish code-supported behavior from behavior observed in a run.
4. Provide a complete scoped `.patch` or native review view when useful so omitted edits remain inspectable. Keep credentials, large generated data, and unrelated work out of the teaching artifact; label any omissions or redactions.

Prefer the verified native PR diff or local review panel when available. A raw patch file is a valid fallback; do not claim a side-by-side UI was shown when only text was produced. Base/head source links and patch links serve different purposes. Snapshot line numbers refer to the preserved files, not today's moving checkout.

If an exact hunk is too noisy (for example a serialized multiline prompt), show a clearly labeled explanatory excerpt alongside the actual patch. Never present rewritten pseudocode as a verbatim diff. Whitespace-ignore or word-diff views are supplementary; inspect the unfiltered diff before claiming only formatting changed. Include added/deleted files and meaningful configuration changes, not only edited functions.

In Test mode, offer only the diff/context needed to make the question fair. Do not disclose the solved flow, explanation, or expected behavior before the learner answers.

## No Git or poorly synchronized copies

Use the least invasive route that preserves evidence:

- **Two available versions:** copy only relevant files into a fresh `before/` and `after/` evidence directory, preserving relative paths. Record each source location, collection time, available commit/dirty status, and content hashes. Use no-index diff; Git initialization is unnecessary just to read differences.
- **Local and remote diverged:** collect each side read-only into separate snapshots. Resolve what each side represents before naming it baseline/candidate. Do not `pull`, `reset`, overwrite with rsync, or merge copies merely to obtain a clean diff. Same commit IDs do not establish equal content when either checkout is dirty; compare the actual files too.
- **Only the current version exists:** explain the current code and record that the previous implementation is unavailable. A saved patch may help reconstruct a candidate baseline in an isolated copy, but label the reconstruction and its provenance; it is not independently recovered historical code. Establish a checkpoint now for future comparisons instead of fabricating an old version.

When Git management is requested, help create useful future checkpoints: a scoped ignore policy, known baseline, named change branch, selected-file commits, and a link from the lesson to the comparison. Prefer an isolated snapshot repository when the original directory is not Git-managed or is shared/frozen. If using synthetic baseline/candidate commits there, label them as archival snapshot commits, not original project history. Keep credentials, datasets, checkpoints and personal notes out; inspect selected files before adding them. Never use `git add .` merely to prepare a lesson.

A request to explain differences permits read-only Git inspection and local learning artifacts; it does not by itself request commits, checkout changes, remote publishing, or repository repair. When the user has authorized Git setup/checkpointing, perform the scoped work directly without asking again. Inspect existing/nested repositories before initializing anything; preserve unrelated edits and the user's index. If one material baseline choice is unresolved, finish independent inspection before asking about that choice.

## Preserve the learning evidence

Record the comparison type, base/head or snapshot identities, dirty/untracked inclusion, relevant patch location, and any unavailable side. For remote snapshots, hashes establish what was copied, not when a missing historical version existed. Save real user replies as learning evidence; a generated diff or explanation is only exposure, not demonstrated Git mastery.
