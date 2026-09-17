# Initial validation: v0.1.1

Date: 2026-09-16.

Four independently initialized native agents used the skill on natural-language requests in an isolated local fixture. Each scenario had a separate simulated Obsidian vault. A coordinator reviewed the outputs against source code and inspected the saved notes, links, and file hashes.

The fixture was a small Python repository with two Git commits. Before the change, an agent branch generated a tool request but returned the original observation. After the change, it dispatched the request to an executor and returned the new observation. The direct branch continued to call the same movement function. There was no remote model, live service, or physical robot.

## Observed results

| Scenario | Observed behavior |
| --- | --- |
| Explain a PR | Produced a project map, diagram, before/after explanation, exact commit and line references, and notes. Recorded exposure without claiming independent mastery. |
| Test before answering | Asked questions without showing solutions, yielded for a response, and saved a pending status. |
| Correct an existing understanding | Preserved the learner's original wording, appended a correction, repaired a stale source reference, and invalidated an unsupported mastery inference without deleting history. |
| Unavailable memory storage | Continued the explanation, reported that memory was not saved, and did not create a replacement vault or select a different user's storage. |
| Targeted follow-up after revision | Clearly framed a command as a prediction rather than an instruction to execute; honored an explicit no-save request. Vault file hashes remained unchanged. |

The initial testing prompt contained ambiguous wording: it first said to run a command, then asked the learner not to run it. The final skill explicitly distinguishes prediction exercises from run-and-observe exercises. The follow-up checked that correction.

## Evidence checks

- Running the fixture confirmed the agent result changed from x=0 to x=2, while the direct result stayed at x=1.
- Referenced source lines were checked against the corresponding commits, including the deleted old file and the moved function.
- New note links resolved. The feedback scenario updated its existing lesson rather than duplicating it, and preserved the original learner text.
- The actual user's profile was unchanged by the simulated cases. Later installation notes were operational records, not evidence of learner ability.
- The official skill-creator validator reported `Skill is valid!` for the final skill. Internal skill references were checked.

## Limits and future trials

These are bounded qualitative trials, not a statistical benchmark or proof of learning outcomes. They used a simulated repository rather than a large production PR. Mermaid source was checked semantically but not rendered for visual acceptance. The optional archify route, real conversation-history retrieval, and long-term profile maintenance were not exercised. English and Chinese instructions were not compared experimentally.

Future evaluations should keep learner data isolated, run only the scenarios affected by a change, and record actual behavior before revising the skill. Useful next cases include a larger PR with asynchronous calls, a second real lesson that resumes a saved question, and a rendered diagram review.

## Unreleased: diff-led learning — 2026-09-17

A coordinator exercised the new command paths in an isolated synthetic repository and two non-Git directories. Staged and unstaged changes produced distinct hunks; total tracked changes did not silently include an untracked file; the file was discovered separately. `git diff --no-index` produced an inspectable patch with exit status 1 for differences, without initializing Git in either snapshot directory. Source status and the Git index remained unchanged during inspection.

The official skill validator passed using an existing environment with PyYAML; the default Python lacked that dependency. Internal reference links and whitespace were checked. This was a local command-path exercise and instruction review, not an independent agent trial. Remote-copy capture, native review UI rendering, and optional Git setup were not executed; no learner profile or personal vault was used by these fixtures.
