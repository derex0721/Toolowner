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

**02 · My Note that adds up, and covers up.** Write `1200 + 350*2 =` in a note and the answer is offered; `=SUM(ABOVE)` adds up the lines above. A line starting with `!!` stays covered until tapped, and covers itself again after 5 seconds. Chapters for long notes, a calendar reminder (.ics) for a to-do and related older notes are there too. All on the device, 0 tokens.

**03 · End-to-end encrypted sync, LAN direct transfer.** Sync (Beta) is optional: content is sealed with AES-256-GCM on your device before it is uploaded, and the server only ever holds ciphertext. Two devices on the same network can send a file straight across over WebRTC with no server in between (Beta).

**04 · Studio: static mini-apps and a personal link card.** Pin a page you made as a static mini-app that runs nothing when opened. Fill in a name and 3–8 links and save one `.html` link card with no code in it, to host wherever you like.

More: PDF and Excel merging, image and video compression, ZIP packing, JSON formatting, Chinese conversion, OCR, personal-data masking and link cleaning, slash commands, reusable recipes, and your own AI provider (OpenAI, Anthropic, Google Gemini, OpenRouter or a model on your own machine). The full list, each with its boundary, is on the [features page](https://toolowner.pages.dev/features).

## Privacy and security at a glance

- **Kept on this device by default.** Notes, to-dos and whatever the tools process stay in your browser on this device. Local tools send nothing and keep working offline.
- **End-to-end encrypted when you sync.** AES-256-GCM with a fresh 96-bit IV per record, a random 256-bit Vault Key, PBKDF2-HMAC-SHA-256 at 600,000 iterations for the sync passphrase, and a recovery key shown once. Encryption happens only on your device, with the browser's built-in WebCrypto.
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
