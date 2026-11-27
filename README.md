<div align="center">

<a href="https://toolowner.pages.dev">
  <img src="https://toolowner.pages.dev/icons/icon-192.png" width="96" height="96" alt="Toolowner">
</a>

<h1>Toolowner</h1>

<p><b>Less AI. Better System.</b><br>
A local-first personal capability layer: tools, notes and chat in one private workspace,<br>with outside AI only for the gaps it truly needs to fill.</p>

<p>
  <b>English</b> · <a href="README.zh-TW.md">繁體中文</a>
</p>

<p>
  <a href="https://toolowner.pages.dev"><img alt="Website" src="https://img.shields.io/badge/website-toolowner.pages.dev-1B1E1C?style=flat-square"></a>
  <a href="https://toolownert1.pages.dev"><img alt="Try the web app" src="https://img.shields.io/badge/web%20app-try%20it-2E6A4E?style=flat-square"></a>
  <a href="LICENSE"><img alt="License: proprietary" src="https://img.shields.io/badge/license-proprietary-675E56?style=flat-square"></a>
  <a href="SECURITY.md"><img alt="End-to-end encrypted sync" src="https://img.shields.io/badge/sync-AES--256--GCM%20E2EE-4A33B3?style=flat-square"></a>
  <a href="https://buymeacoffee.com/derexlee"><img alt="Buy me a coffee" src="https://img.shields.io/badge/support-buy%20me%20a%20coffee-FFDD00?style=flat-square&logo=buymeacoffee&logoColor=1B1E1C"></a>
</p>

<p>
  <a href="https://toolowner.pages.dev"><b>Website →</b></a>
  &nbsp;&nbsp;·&nbsp;&nbsp;
  <a href="https://toolownert1.pages.dev"><b>Open the web app: sign in or use an invite link →</b></a>
</p>

</div>

---

> [!IMPORTANT]
> **Toolowner is closed-source, proprietary software.** This repository does **not** contain the product's source code.
> It exists for the product overview, the [changelog](CHANGELOG.md), the [security policy](SECURITY.md) and community issue reports.
> See [LICENSE](LICENSE).

## Why Toolowner

Most AI tools send everything to a server and bill you per request. Toolowner does the opposite: whatever your device can work out with fixed rules, it does locally, for free, and offline. Outside AI is used only when you set it up yourself, and every call waits for your approval.

| | A typical cloud AI tool | Toolowner local tools |
| --- | --- | --- |
| **Your content** | Uploaded to their server | Stays on this device |
| **Each run** | A network request, billed by tokens | 0 requests · 0 tokens |
| **Result** | Can differ for the same text | Fixed rules: same input, same output |
| **Offline** | Stops working | Opens from scratch after one visit |

## What it does

**01 · Local first, sign in to begin.** Activate your account with a friend’s invite link, or simply sign in, then collect early-bird points and choose whether to turn on end-to-end encrypted sync. Tools run in your browser, and what you make stays on this device by default. If the device can do it, AI is not asked.

**02 · My Note that adds up, and covers up.** Write `1200 + 350*2 =` in a note and the answer is offered; `=SUM(ABOVE)` adds up the lines above. A line starting with `!!` stays covered until tapped, and covers itself again after 5 seconds. Two ways to read: **Page** (the whole note) or **Sections** (a long note split at its headings into numbered cards, read and written one section at a time, like an e-book). The note stays one Markdown text either way. Tags fold to one line. Chapters, a calendar reminder (.ics) for a to-do and related older notes are there too. All on the device, 0 tokens.

**03 · End-to-end encrypted sync, LAN direct transfer.** Sync (Beta) is optional: content is sealed with AES-256-GCM on your device before it is uploaded, and the server only ever holds ciphertext. Two devices on the same network can send a file straight across over WebRTC with no server in between (Beta).

**04 · Studio: static mini-apps and a personal link card.** Pin a page you made as a static mini-app that runs nothing when opened. Fill in a name and 3–8 links and save one `.html` link card with no code in it, to host wherever you like.

### New in late November 2026

- **My Note: ranked search and imports.** Search ranks notes by BM25 relevance and keeps dates and codes (`2026-11-27`, `A-102`) whole. Exports from Obsidian, Notion and Evernote import, parsed on your device.
- **Traditional ↔ Simplified, and garbled files rescued.** The Aa panel converts the note or the selection from a fixed table on your device (0 tokens, one undo step), leaving code, web addresses and `{{…}}` alone. Old Big5 / GBK files are read with the right encoding, using only the browser's own TextDecoder.
- **Find AI on your computer, and request limits.** Settings › AI asks only the loopback addresses the app already allows (11434, 8080, 20128), and only when you press the button. Outside AI with your own key can have a daily / monthly request limit that stops before the approval card.
- **Intel: clusters, OPML and feed health.** The same event from several feeds is one card, the first-hand source on top. OPML import reads only `<outline>` tags, refuses any DOCTYPE / ENTITY and keeps http / https addresses only; past the 10-subscription limit you tick which to keep. Export writes a standard, fully escaped `.opml`. A feed that keeps failing rests with exponential backoff (15 minutes, doubling, up to 24 hours), shows a quiet status tag and has a Retry now button, without slowing the healthy feeds.
- **#4 element picker and "Add to a note section".** A block tapped in the visual editor is saved to My Note as clean Markdown, read from its HTML string (no page script runs). An intel item can be appended to an existing note as a new `## title` section at its end; the note's earlier text is kept exactly.
- **Declarative JSON plugins.** In Settings › Plugins, add or import a JSON manifest: snippets (your own `/` commands that insert fixed Markdown) or text rules (fixed words or guarded regular expressions, applied to the selection or the whole note, undone in one step). Plugins are data only: a closed list of fields, 16 KB, up to 30 snippets or 50 rules, any script field refused, risky patterns (nested quantifiers, back-references, look-around) refused before saving, and every run ended after 1 second.
- **My Note: Page and Sections.** Switch a long note to Sections and it becomes numbered cards (title, a one-line summary, line count); open one, write in it, and step Previous · Next. Nothing about the saved note changes: sync, encryption and `.md` export see the same text.
- **Reversible placeholders before outside AI.** Keys and tokens, `!!` shield lines, e-mails, paths on your computer and (when masking is on) phone numbers become `{{SECRET_1}}`, `{{EMAIL_1}}`, `{{PATH_1}}`, `{{PHONE_1}}` on the approval card and in the request. The answer is put back on your device, and the table of originals is cleared in memory right after. Actions are graded Tier 0 / 1 / 2 every time; anything that sends, deletes or calls a provider waits for you.
- **Backup routes that rest.** With your own API key and backups set up, a route that answers 429, a server error or nothing in time rests for a while, and the next call starts with one that is not resting. It only reorders the routes you approved.
- **Version history for the AI context.** What you attach to a chat keeps up to 20 versions on this device: compare any of them with what is on screen, and restore one (what you had is kept as a version first). It is never synced, and it is encrypted with your master password when you have set one.
- **Guard log.** Settings › Privacy lists the last 50 outside-AI calls as counts only (route, how many items were masked, tier, check result), never their content.
- **Companion CLI for agents (v1 spec).** `toolowner note split / join / eval`, `toolowner card build`, `toolowner guard scan` and `toolowner undo`: the app's own My Note, link-card and masking functions on the command line, offline, with `--dry-run`, `--schema`, JSON output and an undo receipt for every file it writes. See [SKILL.md](SKILL.md) and [INSTALL_FOR_AGENTS.md](INSTALL_FOR_AGENTS.md).

More: PDF and Excel merging, image and video compression, ZIP packing, JSON formatting, Chinese conversion, OCR, personal-data masking and link cleaning, slash commands, reusable recipes, and your own AI provider (OpenAI, Anthropic, Google Gemini, OpenRouter or a model on your own machine). The full list, each with its boundary, is on the [features page](https://toolowner.pages.dev/features).

## Privacy and security at a glance

- **Kept on this device by default.** Notes, to-dos and whatever the tools process stay in your browser on this device. Local tools send nothing and keep working offline.
- **End-to-end encrypted when you sync.** AES-256-GCM with a fresh 96-bit IV per record, a random 256-bit Vault Key, PBKDF2-HMAC-SHA-256 at 600,000 iterations for the sync passphrase, and a recovery key shown once. Encryption happens only on your device, with the browser's built-in WebCrypto.
- **Placeholders, not secrets, go out.** Before an approved outside-AI call, keys, shield lines, e-mails and local paths are replaced with numbered placeholders and restored only on your device. Detection is rule-based: a secret in a shape it does not know is not found.
- **No ads, no tracking.** No third-party analytics or tracking scripts. Content goes to an outside AI only when you set one up yourself (BYO API) and approve the call.
- **Stated plainly:** with sync on, the server can see your sign-in identity and plan, opaque collection labels, padded record sizes, record and device ids, and sync timestamps; never the content or the device names.

Details, known limits and how to check all of this yourself with your browser's Network panel: **[SECURITY.md](SECURITY.md)** and the [security & privacy whitepaper](https://toolowner.pages.dev/security).

## Report a problem or suggest a feature

- 🐞 **Bug:** [open a bug report](../../issues/new?template=bug_report.yml)
- 💡 **Idea:** [suggest a feature](../../issues/new?template=feature_request.yml)
- 🔒 **Security issue:** please do **not** open a public issue. Follow [SECURITY.md](SECURITY.md).

> [!WARNING]
> Never paste a recovery key, a sync passphrase, an API key or the content of private notes into an issue. Issues are public.

## Support Toolowner

Toolowner is built independently. If it saves you time, you can support its development:

<a href="https://buymeacoffee.com/derexlee"><img alt="Buy me a coffee" src="https://img.shields.io/badge/Buy%20me%20a%20coffee-derexlee-FFDD00?style=for-the-badge&logo=buymeacoffee&logoColor=1B1E1C"></a>

More ways to support (OEN, ECPay) are coming.

## License

Copyright © 2026 Toolowner. All rights reserved. Toolowner is proprietary software; nothing in this repository grants a licence to the product or its source code. See [LICENSE](LICENSE).
