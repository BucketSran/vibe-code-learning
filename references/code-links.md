# Code References by Output Surface

Use when emitting code links in chat or saved notes. A citation identifies evidence at a version; a navigation link opens a convenient local file. Keep those roles explicit when their targets differ.

## Choose the destination before the scheme

| Output | Link behavior |
| --- | --- |
| Codex chat | Follow the host's native file-link contract. Where supported, use `[module.py:91](/absolute/repo/module.py:91)`; paths with spaces need the host's angle-bracket form. Do not replace host-native links with editor or `file://` URIs. |
| Obsidian or another Markdown note | Use the user's explicit current choice, then an applicable saved choice. For a confirmed VS Code preference, a link such as `[module.py:91](vscode://file/absolute/repo/module.py:91)` can provide file-and-line navigation. Other editors require a verified supported scheme, not a guessed substitution. |
| No note editor preference | Use a verified permanent source link when available. Otherwise a correctly encoded `file:///` link can provide file-level navigation; retain the symbol and verified line in the text, and do not claim that the URI jumps to the line. |

An installed editor proves availability, not preference. Ask about the editor only if it materially affects a requested navigation feature and no suitable fallback exists. Do not require an installation or persist a tool-detection guess. Save a preference only from an actual user choice, with its source and scope; “this note only” does not change the default.

VS Code's documented file/line URI syntax is described in its [command-line documentation](https://code.visualstudio.com/docs/configure/command-line#_opening-vs-code-with-urls). Check the selected editor's own documentation when another scheme is needed.

Link directly to the cited file, not its parent folder. Use short repo-relative labels to disambiguate duplicate basenames; reserve root-directory links for project orientation. Encode URI path components correctly, including spaces, non-ASCII characters, `#` and `?`; retain scheme delimiters and documented line syntax. For a saved note, use note-relative attachment links where appropriate. A structurally valid link is not proof that an external application opened it; report launch behavior as tested only when observed.

## Preserve the reference version

Before saving, verify path, symbol, and lines against the same source identity used in the explanation:

- **Committed code:** inspect the recorded commit, including the base side for deleted code and each revision's path for renames. Prefer a verified commit permalink. New working-tree lines do not replace these historical line numbers.
- **Captured snapshot:** cite the preserved file with its snapshot identity/hash. Verify the snapshot, not a later copy.
- **Live working tree:** re-read the actual file near save time. Update only the live navigation link if lines moved; retain the symbol and label the checkout as live. If evidence depends on mutable contents, preserve a scoped snapshot or report that the earlier state is no longer verifiable.

If the referenced historical file is absent locally, use its permanent source link or a clearly labeled local snapshot. Do not make a clickable dead path or present the renamed head file as the old implementation. Without an available navigation target, keep the precise repository/revision/path/symbol citation and state the limitation.
