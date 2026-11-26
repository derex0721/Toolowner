# Installing and calling the toolowner CLI (for agents)

For Claude Code, Codex, Cue and other coding agents. Read `SKILL.md` for when to use each command.

## Requirements

| Need | Value |
| --- | --- |
| Node.js | 22.18 or newer |
| Dependencies | None at run time |
| Network | None. The CLI imports no network module and makes no request |
| Credentials | None. It reads no sign-in session, API key, Supabase URL or token |
| Disk | Only `--out` files and the undo folder (`<root>/.toolowner/undo` by default) |

## Install

From GitHub Releases, tag [`cli-v1.0.0`](https://github.com/derex0721/Toolowner/releases/tag/cli-v1.0.0) (plain JavaScript, no dependencies):

```sh
npm install -g https://github.com/derex0721/Toolowner/releases/download/cli-v1.0.0/toolowner-1.0.0.tgz
toolowner --version   # 1.0.0
```

Without installing: check the archive against `SHA256SUMS.txt`, unpack it and run it with Node (on Windows use the `.zip` and `node toolowner-cli-v1.0.0\bin\toolowner.js`):

```sh
base=https://github.com/derex0721/Toolowner/releases/download/cli-v1.0.0
curl -LO $base/toolowner-cli-v1.0.0.tar.gz && curl -LO $base/SHA256SUMS.txt
grep toolowner-cli-v1.0.0.tar.gz SHA256SUMS.txt | shasum -a 256 -c   # → OK
tar -xzf toolowner-cli-v1.0.0.tar.gz
node toolowner-cli-v1.0.0/bin/toolowner.js --usage
```

npm: not published yet. Until `toolowner` is on the npm registry, install from the release above.

This repository holds the documentation only; the CLI is attached to the release with its own `LICENSE` (free to install and run unmodified). The Toolowner app and its source code are not included (see [LICENSE](LICENSE)).

## Calling convention

- Add `--output-format json` to every call. Success: `{"ok": true, "command", "dryRun", "result", "receipt"?, "wouldWrite"?}`. Failure: `{"ok": false, "exitCode", "error": {"type", "message"}}`.
- Input: `--in <file>` (inside `--root`), `--text <text>`, or standard input.
- Output file: `--out <file>` (inside `--root`). Each write first copies what was there into the undo folder and returns `receipt.id`.
- Preview: `--dry-run` reports `wouldWrite` and writes nothing (no file, no backup, no receipt).
- Discover: `toolowner --usage --output-format json` (command tree), `toolowner --schema` (all commands), `toolowner guard scan --schema` (one).

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
| 1 | The command ran and failed | `not_math`, `receipt_not_found`, `changed_since_write`, `already_undone`, `backup_damaged` |
| 2 | Bad arguments or a safety check refused it | `unknown_command`, `unknown_flag`, `missing_input`, `bad_json`, `card_invalid`, `path_traversal`, `path_outside_root`, `symlink_refused`, `bad_receipt` |

## Troubleshooting

| Symptom | Cause | Fix |
| --- | --- | --- |
| `path_traversal` | A path contains `..` | Give a path inside the root, or set `--root` to the folder that holds it |
| `path_outside_root` | An absolute path, or a folder link, leads outside `--root` | Set `--root` to the right folder |
| `symlink_refused` | `--out` (or the file being undone) is a symbolic link | Write to the real file |
| `missing_input` | No `--in`, `--text` or piped input | Pass one of them |
| `card_invalid` | Fewer than 3 or more than 8 links, no name, or a link that is not http/https | Fix the rows listed in the message |
| `changed_since_write` | The file was edited after the write | Check it; `--force` undoes anyway |
| `toolowner: command not found` | The CLI is not installed or not on `PATH` | Run the `npm install -g` line above, then open a new shell |
| `guard scan` finds nothing in a key | The shape is not one Toolowner recognises | Treat the text as sensitive anyway; the scan lowers risk, it does not prove absence |
