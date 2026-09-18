# Validation

## Initial validation: v0.1.1

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

## Diff-led learning, included in v0.1.6 — 2026-09-17

A coordinator exercised the new command paths in an isolated synthetic repository and two non-Git directories. Staged and unstaged changes produced distinct hunks; total tracked changes did not silently include an untracked file; the file was discovered separately. `git diff --no-index` produced an inspectable patch with exit status 1 for differences, without initializing Git in either snapshot directory. Source status and the Git index remained unchanged during inspection.

The official skill validator passed using an existing environment with PyYAML; the default Python lacked that dependency. Internal reference links and whitespace were checked. This was a local command-path exercise and instruction review, not an independent agent trial. Remote-copy capture, native review UI rendering, and optional Git setup were not executed; no learner profile or personal vault was used by these fixtures.

## v0.1.7 — 2026-09-18

Independent native agents used the candidate skill with natural learner requests and isolated synthetic configurations. Four trial vaults each began with a 1000-row legacy profile, two original learner-authored session notes, and a relevant concept note. The repository contained base/head commits, a renamed executor, and an intentional nine-line working-tree shift. No real learner notes, configuration, or chat history were used.

| Scenario | Observed outcome |
| --- | --- |
| Continue an explanation from legacy memory, no quiz | Added a small active section, retained all 1000 old rows and original learner text, and kept explanation, location, and modification evidence separate. Recorded the new explanation as exposure and retained unresolved gaps. |
| Save a lesson with a temporary file-link choice | Kept the sourced VS Code default, used file URIs for that note and host-native links for chat, and separated committed dispatcher line 25 from live line 34. Historical source snapshots matched their commits. |
| Offer a learner-owned zero-distance exercise | Created a scratch copy and acceptance criteria, saved pending status, and waited without supplying a solution or changing the source repository. |
| Evaluate the learner's actual incomplete edit | The supplied edit passed the three existing tests and returned the requested coordinates, but zero-distance results aliased the original state. The tutor ran focused checks, identified that gap, saved the learner's exact reasoning and feedback, kept the edit unchanged, and did not promote ability. |
| Revisit an unresolved gap with a new question, no saving | Used a new command/validation scenario, yielded without answers, and left all original vault/config files byte-identical. |

### Failure found and targeted retry

The first link and recall trials incorrectly read the full large profile while reading `memory.md` in parallel. Their later selective reads and correct artifacts did not erase that retrieval failure. The entrypoint now explicitly orders the operations: finish the reference, inspect profile size, then choose excerpts/searches; truncation is not selective retrieval.

A fresh agent repeated the no-save cold start with the final instruction. It read `memory.md` before accessing the profile, checked its 1020 lines / 155210 bytes, selected a short opening and correction excerpt, searched relevant concepts, and opened only the two linked sessions. It did not emit the whole profile. This is a qualitative behavioral observation, not an exact token benchmark or a guarantee across models.

### Artifact checks and limits

- A coordinator verified all 1000 original concept rows and both original learner-note texts remained present in each trial. Baseline, shared source files, and the no-save trial's original files retained their hashes.
- The coordinator compared 16 saved commit files in the continuation trial and 14 scoped files in the link trial against Git objects. The source's intentional working-tree change was preserved.
- Base/head example runs produced agent x=0/x=2 and unchanged direct x=1. The initial repository tests passed 2/3 checks respectively; the learner feedback correctly distinguished these existing checks from the new exercise requirements.
- Skill format, internal Markdown targets, and whitespace were checked. An independent read-only instruction review found no additional blocking contradictions.
- External application launch and Obsidian rendering were not exercised. Review scheduling over real elapsed time, other editor URI schemes, and long-term learning outcomes remain untested. Profiles were accessed selectively rather than subjected to a destructive full migration.
