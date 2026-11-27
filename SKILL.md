---
name: toolowner-cli
description: Use the local toolowner CLI to split, join, outline and work out the math in My Note Markdown, build a static Studio link card (.html), mask keys, e-mails and paths in text before it is shared, and seal text into an offline encrypted .html capsule. Every file it writes can be undone with a receipt. It runs offline and never sends anything.
---

# toolowner CLI

`toolowner` is Toolowner's companion command line. It runs the same Way Core functions the app uses, on this computer only. It makes no network request, starts no shell or child process, and reads no sign-in session, API key or cloud setting.

## Install

```sh
npm install -g https://github.com/derex0721/Toolowner/releases/download/cli-v1.1.0/toolowner-1.1.0.tgz
toolowner --version   # 1.1.0
```

Node.js 22.18 or newer. Other ways (checksums, no install) are in `INSTALL_FOR_AGENTS.md`. Not on the npm registry yet.

## When to use it

| Task | Command |
| --- | --- |
| Read a long My Note text one section at a time | `toolowner note split` |
| Put edited sections back into one note | `toolowner note join` |
| Work out lines such as `12500 + 3800*3 =` or `=SUM(ABOVE)` | `toolowner note eval` |
| See a long note's chapters (e-book table of contents) | `toolowner note toc` |
| Make a personal link card page | `toolowner card build` |
| Check text for keys, tokens, e-mails or paths before sharing it | `toolowner guard scan` |
| Send text as a passphrase-protected file that opens offline in a browser | `toolowner capsule pack` |
| Check that a received capsule `.html` is intact before opening it | `toolowner capsule inspect` |
| Let a person run several commands by hand | `toolowner repl` |
| Take back a file written with `--out` | `toolowner undo --receipt <id>` |

## Rules for agents

1. Always pass `--output-format json` and read `ok`, `result`, `receipt` and `error.type`.
2. Run `--dry-run` first when a command writes with `--out`; write only after the person agrees.
3. Keep the `receipt.id` of every write. Offer `toolowner undo --receipt <id>` if the person wants it back.
4. `guard scan` returns only placeholders (`{{SECRET_1}}`, `{{EMAIL_1}}`, `{{PATH_1}}`, `{{PHONE_1}}`) and counts. Do not try to recover the originals, and do not paste keys into commands; use `--in <file>` instead of `--text` for anything sensitive.
5. `capsule pack`: never put a passphrase on the command line, in a file you write, or in your reply. Ask the person to set an environment variable themselves and pass only its name with `--passphrase-env <VAR>`, or let them run the command in their own terminal, where it asks with hidden input. There is no `--passphrase` flag. The JSON result never contains the passphrase; it reports only `passphraseSource` (`env` or `prompt`). Do not attempt to decrypt capsules.
6. `capsule inspect` exits `1` with `not_a_capsule` or `capsule_modified` when the file is not an intact capsule. Tell the person not to open such a file.
7. `toolowner repl` is for people at a terminal. Agents should call one-shot commands instead. Running `toolowner` with no arguments exits `2` (it never opens the prompt).
8. Paths must stay inside `--root` (default: the current folder). A path with `..`, outside the root, or a symbolic link is refused with exit code 2. Do not try to work around it.
9. Exit codes: `0` success, `1` the command failed, `2` bad arguments or a safety check refused it.

## Examples

```sh
toolowner note split --in notes/trip.md --output-format json
toolowner note toc --in notes/book.md --output-format json
toolowner note eval --text $'Coffee 120\nTea 80\n=SUM(ABOVE)' --output-format json
toolowner card build --name "Ada" --link "Blog|https://example.com" --link "Code|https://github.com/example" --link "Mail|https://example.com/contact" --out card.html --dry-run --output-format json
toolowner guard scan --in draft.txt --output-format json
toolowner capsule pack --in plan.txt --out plan.html --passphrase-env CAPSULE_PW --dry-run --output-format json
toolowner capsule inspect --in plan.html --output-format json
toolowner undo --receipt r-20261125093000-1a2b3c4d --output-format json
```

`toolowner --usage` prints the command tree; `toolowner <command> --schema` prints the JSON Schema of its flags.
