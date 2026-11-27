# Installing and calling the toolowner CLI (for agents)

For Claude Code, Codex, Cue and other coding agents. Read `SKILL.md` for when to use each command.

## Requirements

| Need | Value |
| --- | --- |
| Node.js | 22.18 or newer |
| Dependencies | None at run time |
| Network | None. The CLI imports no network module and makes no request |
| Processes | None. It starts no shell or child process; `toolowner repl` splits words itself and runs only toolowner commands |
| Credentials | None. It reads no sign-in session, API key, Supabase URL or token |
| Disk | Only `--out` files and the undo folder (`<root>/.toolowner/undo` by default) |
| Passphrases | `capsule pack` reads one from the environment variable named by `--passphrase-env`, or asks on the terminal with hidden input. It is never printed, logged, written to a receipt or accepted as a flag value |

## Install

From GitHub Releases, tag [`cli-v1.1.0`](https://github.com/derex0721/Toolowner/releases/tag/cli-v1.1.0) (plain JavaScript, no dependencies):

```sh
npm install -g https://github.com/derex0721/Toolowner/releases/download/cli-v1.1.0/toolowner-1.1.0.tgz
toolowner --version   # 1.1.0
```

Without installing: check the archive against `SHA256SUMS.txt`, unpack it and run it with Node (on Windows use the `.zip` and `node toolowner-cli-v1.1.0\bin\toolowner.js`):

```sh
base=https://github.com/derex0721/Toolowner/releases/download/cli-v1.1.0
curl -LO $base/toolowner-cli-v1.1.0.tar.gz && curl -LO $base/SHA256SUMS.txt
grep toolowner-cli-v1.1.0.tar.gz SHA256SUMS.txt | shasum -a 256 -c   # → OK
tar -xzf toolowner-cli-v1.1.0.tar.gz
node toolowner-cli-v1.1.0/bin/toolowner.js --usage
```

npm: not published yet. Until `toolowner` is on the npm registry, install from the release above.

This repository holds the documentation only; the CLI is attached to the release with its own `LICENSE` (free to install and run unmodified), together with `MANIFEST.txt` (the SHA-256 of every file inside the package) and the package's `TEST.md` (how it is tested). The Toolowner app and its source code are not included (see [LICENSE](LICENSE)).

## Calling convention

- Add `--output-format json` to every call. Success: `{"ok": true, "command", "dryRun", "result", "receipt"?, "wouldWrite"?}`. Failure: `{"ok": false, "exitCode", "error": {"type", "message"}}`.
- Input: `--in <file>` (inside `--root`), `--text <text>`, or standard input.
- Output file: `--out <file>` (inside `--root`). Each write first copies what was there into the undo folder and returns `receipt.id`.
- Preview: `--dry-run` reports `wouldWrite` and writes nothing (no file, no backup, no receipt).
- Discover: `toolowner --usage --output-format json` (command tree), `toolowner --schema` (all commands), `toolowner guard scan --schema` (one).
- No arguments: `toolowner` alone prints the usage on standard error and exits `2`. The interactive prompt starts only with `toolowner repl`.

### Capsules

```sh
# The person sets the variable in their own shell; the agent only passes its name.
toolowner capsule pack --in plan.txt --out plan.html --passphrase-env CAPSULE_PW --output-format json
# → {"ok":true,"command":"capsule pack","result":{"alg":"AES-256-GCM","kdf":"PBKDF2-SHA256","iterations":600000,"passphraseSource":"env","inputChars":22,"bytes":3864,"sha256":"…"},"receipt":{…}}
toolowner capsule inspect --in plan.html --output-format json
# → {"ok":true,"command":"capsule inspect","result":{"valid":true,"templateIntact":true,"title":"Encrypted Capsule","iterations":600000,"plaintextBytes":22,…}}
```

`capsule inspect` compares the file with the page Way Core builds from the same payload; any other script, element or remote resource makes it `capsule_modified`. It reads the file as text only.

### REPL

`toolowner repl [--root <dir>] [--state-dir <dir>] [--output-format json]` reads one line at a time: `note …`, `card build …`, `guard scan …`, `capsule pack|inspect …`, `undo …` (a leading `toolowner` is optional), plus `help`, `json on|off`, `receipts` and `exit` / `quit` / Ctrl-D. Lines are split into words with `'…'`, `"…"` and `\` only; `$VAR`, `*`, `|`, `;` and `` `…` `` are plain characters, and any other first word is refused. Lines can also be piped in (`printf 'note toc --in a.md\nexit\n' | toolowner repl`); with piped input `capsule pack` needs `--passphrase-env`.

```sh
toolowner note split --in note.md --out sections.json --output-format json
# → {"ok":true,"command":"note split","result":{"count":4,...},"receipt":{"id":"r-20261125093000-1a2b3c4d","target":"sections.json","existed":false,...}}
toolowner note join --in sections.json --out note.md --output-format json
toolowner undo --receipt r-20261125093000-1a2b3c4d --output-format json
```

## Exit codes

| Code | Meaning | Examples (`error.type`) |
| --- | --- | --- |
| 0 | Success | |
| 1 | The command ran and failed | `not_math`, `not_a_capsule`, `capsule_modified`, `seal_failed`, `receipt_not_found`, `changed_since_write`, `already_undone`, `backup_damaged` |
| 2 | Bad arguments or a safety check refused it | `unknown_command`, `unknown_flag`, `missing_input`, `bad_json`, `card_invalid`, `missing_passphrase`, `weak_passphrase`, `empty_input`, `path_traversal`, `path_outside_root`, `symlink_refused`, `bad_receipt` |

## Troubleshooting

| Symptom | Cause | Fix |
| --- | --- | --- |
| `path_traversal` | A path contains `..` | Give a path inside the root, or set `--root` to the folder that holds it |
| `path_outside_root` | An absolute path, or a folder link, leads outside `--root` | Set `--root` to the right folder |
| `symlink_refused` | `--out` (or the file being undone) is a symbolic link | Write to the real file |
| `missing_input` | No `--in`, `--text` or piped input | Pass one of them |
| `card_invalid` | Fewer than 3 or more than 8 links, no name, or a link that is not http/https | Fix the rows listed in the message |
| `missing_passphrase` | `capsule pack` without `--passphrase-env` and without a terminal, or the named variable is not set | Ask the person to set the variable, or to run the command in their terminal |
| `weak_passphrase` | Fewer than 8 characters | Use a longer passphrase |
| `capsule_modified` | The capsule's page was edited after it was built | Do not open it; ask for the original file |
| `changed_since_write` | The file was edited after the write | Check it; `--force` undoes anyway |
| `toolowner: command not found` | The CLI is not installed or not on `PATH` | Run the `npm install -g` line above, then open a new shell |
| `guard scan` finds nothing in a key | The shape is not one Toolowner recognises | Treat the text as sensitive anyway; the scan lowers risk, it does not prove absence |
