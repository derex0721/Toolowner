# Changelog

**English** · [繁體中文](#更新日誌繁體中文)

What has shipped in the Toolowner web app (https://toolownert1.pages.dev), newest first. Every feature comes with its boundary; anything marked **Beta** is still being checked on real devices. The full list is on the [features page](https://toolowner.pages.dev/features).

## 27 November 2026

### New
- **Companion CLI v1.1.0** (tag `cli-v1.1.0`, built; release pending). Three local commands and a prompt, still with no dependencies, no network request and no shell or child process:
  - `toolowner note toc`: a long note's chapters (`#` to `###`, code fences skipped) as an e-book table of contents; read only.
  - `toolowner capsule pack`: seal a text file into the same offline self-decrypting `.html` capsule the app makes (PBKDF2-SHA256 600,000 + AES-256-GCM). The passphrase comes from an environment variable you name with `--passphrase-env`, or a hidden prompt; it is never printed, logged, written to a receipt or accepted as a flag. `--dry-run` and undo receipts as for every write.
  - `toolowner capsule inspect`: check that an `.html` is an intact capsule (fixed algorithms, sane sizes, the page unchanged) without decrypting it or running its script.
  - `toolowner repl`: run these commands one after another at a prompt, switch JSON output, list the session's receipts. Words are split with quotes only; nothing is expanded or run. `toolowner` with no arguments still prints the usage and exits 2.
  - Each release now also carries `MANIFEST.txt` (SHA-256 of every packed file) and `TEST.md`. See [SKILL.md](SKILL.md) and [INSTALL_FOR_AGENTS.md](INSTALL_FOR_AGENTS.md).

## 26 November 2026

### New
- **Companion CLI v1.0.0 on GitHub Releases** (tag `cli-v1.0.0`). `npm install -g https://github.com/derex0721/Toolowner/releases/download/cli-v1.0.0/toolowner-1.0.0.tgz`, or the `.tar.gz` / `.zip` checked against `SHA256SUMS.txt`. Node.js 22.18 or newer, no dependencies, no network request. It contains only the CLI and the local functions it calls (My Note sections and math, the link card, the guard scan, undo receipts); no sync, cloud, key or app code. Not on the npm registry yet. See [INSTALL_FOR_AGENTS.md](INSTALL_FOR_AGENTS.md).

## 25 November 2026

### New
- **My Note: Page and Sections (e-book) view.** A long note splits at its `##` / `###` headings and `---` rules into numbered section cards; one section opens in the same editor (math and shield lines work inside it) with Previous · All sections · Next. Page is the default and the choice is remembered on the device. The note is still one Markdown text: sync, encryption, the table of contents and `.md` export are unchanged.
- **My Note: tags fold to one line.** The first tag and "+N" with an arrow; the arrow shows every tag and the favourites to apply.
- **Backup routes rest after a failure (your own API key).** 429: at least 60 s (or Retry-After); a server error or timeout: 30 s, doubling in a row up to 5 minutes; one good answer clears it. Timeouts now move a call to the next backup too. Only the order of routes you approved changes. Settings shows who answered and which route is resting.
- **OmniRoute gateway (Web only).** A gateway on your own computer at `http://localhost:20128/v1`. It forwards to the cloud, so it is masked and approved one call at a time like any outside AI.
- **Version history for the AI context.** Up to 20 versions of what you attach to a chat, on this device only: compare any version with the screen, save one by hand, restore one (what you had is kept first). Not synced; encrypted with your master password when one is set.
- **Companion CLI for agents, v1 spec.** `toolowner note split / join / eval`, `card build`, `guard scan` and `undo`, offline, with `--usage`, `--schema`, `--dry-run`, `--output-format json`, exit codes 0 / 1 / 2 and an undo receipt for every file it writes. See [SKILL.md](SKILL.md) and [INSTALL_FOR_AGENTS.md](INSTALL_FOR_AGENTS.md).

### Security
- **Reversible placeholders before outside AI.** Keys and tokens, My Note shield lines, e-mails, paths and (with masking on) phone numbers become `{{SECRET_n}}`, `{{EMAIL_n}}`, `{{PATH_n}}`, `{{PHONE_n}}` on the approval card and in the request, fields included. The answer is restored on this device and the table is cleared from memory; it is never stored, logged or synced.
- **Risk tiers recomputed every time.** Tier 0 (read only), Tier 1 (local writes, with path checks: no `..`, absolute paths, `~`, drive letters, URL schemes or NUL), Tier 2 (sends, deletes or calls a provider: always waits for your confirmation).
- **One bounded retry.** An answer that does not match the expected shape is asked for once more at most, then shown as unverified and not applied.
- **Guard log.** The last 50 outside-AI calls in Settings › Privacy, counts only, never synced, cleared with two taps.

## November 2026

### New
- **My Note extras.** Math lines (`1200 + 350*2 =`, `=SUM(ABOVE)`), screen-shield lines (`!!` lines stay covered until tapped and cover themselves again after 5 seconds), chapters for long notes, a calendar reminder (.ics) for a to-do and related older notes. All on the device, 0 tokens, each switchable in Settings › Data.
- **LAN direct transfer (Beta).** Two devices on the same network pair with a one-time 6-digit code and QR codes and send a file over WebRTC, sealed again with AES-256-GCM and checked with SHA-256. 50 MB per file, no server in between, no STUN or TURN, so guest networks or AP isolation may block it.
- **Early-bird invites.** Share your invite link or QR code from the Account page; once a friend has set up sync, you get +30 and they get +15 early-bird points. You may choose your own invite code once.
- **Personal link card.** Template Studio makes a link-in-bio page from a name, one line and 3–8 links, in a warm-paper or deep-ink theme, saved as one static `.html` with no script in it and every input escaped.
- **Template Studio.** Code templates, skills, your own models and pinned mini-apps on one page; a visual page editor; static mini-apps that run nothing when opened.
- **More local tools.** Encrypted capsule, watermark, shadow-free scan and long screenshot; intel feeds parsed on the device.
- **Two ways back in when every old device is lost.** Take over with your recovery key (five wrong tries lock it for an hour), or clear the cloud copy and start over.
- **Your own AI provider.** OpenAI, Anthropic, Google Gemini, OpenRouter and BeatAPI (Web only), or a model on your own machine (Ollama, llama.cpp, PocketPal). Every call needs your approval.
- **Notes and to-dos.** Round to-dos with an agenda switch, links inserted with tracking removed, numbered lists, 12–48 pt and imported fonts.
- **Two-track OCR, the caged `/code` command, @ references, a to-confirm inbox.** The core app opens offline after one visit (about 3 MB).

### Security
- Sync (Beta) is end-to-end encrypted: AES-256-GCM per record, PBKDF2-HMAC-SHA-256 at 600,000 iterations for the passphrase, a recovery key shown once. See [SECURITY.md](SECURITY.md).
- The website runs under a strict Content Security Policy with no outside requests.

---

# 更新日誌（繁體中文）

Toolowner 體驗版（https://toolownert1.pages.dev）已上線的內容，由新到舊。每一項都附上邊界；標了 **Beta** 的仍在實機驗證。完整清單請見[全部功能](https://toolowner.pages.dev/features)。

## 2026 年 11 月 27 日

### 新增
- **伴侶 CLI v1.1.0**（標籤 `cli-v1.1.0`，已建置，待發布）。新增三個本機指令與互動模式，仍然零相依、不發出網路請求、不啟動 shell 或子行程：
  - `toolowner note toc`：抽取長筆記的章節目錄（`#` 到 `###`，略過程式碼區塊），E-book 大綱；只讀。
  - `toolowner capsule pack`：把文字檔封成與 App 相同的離線自解密 `.html` 膠囊（PBKDF2-SHA256 600,000 + AES-256-GCM）。密碼從 `--passphrase-env` 指定的環境變數或隱藏輸入讀取，絕不印出、記錄、寫進 receipt，也不接受以參數傳入。支援 `--dry-run` 與 undo receipt。
  - `toolowner capsule inspect`：檢查 `.html` 是否為完整的靜態膠囊（固定演算法、合理大小、頁面未被修改），不解密、不執行其中腳本。
  - `toolowner repl`：在提示字元下連續執行上述指令、切換 JSON 輸出、列出本次 session 的 receipt。只以引號切字，不展開、不執行任何東西。無參數執行 `toolowner` 仍印出用法並以結束碼 2 結束。
  - 每次發布另附 `MANIFEST.txt`（套件內每個檔案的 SHA-256）與 `TEST.md`。請見 [SKILL.md](SKILL.md) 與 [INSTALL_FOR_AGENTS.md](INSTALL_FOR_AGENTS.md)。

## 2026 年 11 月 26 日

### 新增
- **伴侶 CLI v1.0.0 上架 GitHub Releases**（標籤 `cli-v1.0.0`）。`npm install -g https://github.com/derex0721/Toolowner/releases/download/cli-v1.0.0/toolowner-1.0.0.tgz`，或下載 `.tar.gz`／`.zip` 並以 `SHA256SUMS.txt` 核對。需 Node.js 22.18 以上，零相依、不發出任何網路請求。內容只有 CLI 與它呼叫的本機函式（My Note 分塊與算式、連結名片、guard 脫敏、undo receipt），不含同步、雲端、金鑰或 App 程式碼。尚未上架 npm。請見 [INSTALL_FOR_AGENTS.md](INSTALL_FOR_AGENTS.md)。

## 2026 年 11 月 25 日

### 新增
- **My Note 整頁與分塊（電子書）模式。** 長筆記依 `##`／`###` 標題與 `---` 分隔線切成編號區塊卡片；打開一塊就在同一個編輯器裡寫（算式與防窺行照常運作），用「上一塊 · 所有區塊 · 下一塊」翻頁。預設為整頁，選擇記在本機。筆記仍是同一份 Markdown：同步、加密、目錄與 `.md` 匯出都不變。
- **My Note 標籤收合成一行。** 顯示第一個標籤與「+N」及箭頭；點箭頭展開全部標籤與可套用的常用標籤。
- **失敗後會冷卻的備用路線（自備 API 金鑰）。** 429：至少 60 秒（或依 Retry-After）；伺服器錯誤或逾時：30 秒，連續失敗加倍、最多 5 分鐘；成功一次即解除。逾時現在也會轉到下一條備用。只改變你核准過的路線順序。設定會顯示由誰回答、哪條路線冷卻中。
- **OmniRoute 閘道（僅 Web 版）。** 你自己電腦上的閘道 `http://localhost:20128/v1`。它會轉送到雲端，所以和任何外部 AI 一樣逐次遮罩、逐次核准。
- **AI 上下文的版本紀錄。** 附加到對話的內容最多保留 20 版，只在本機：任一版都能與畫面比對、手動存一版、還原此版本（會先保留目前內容）。不同步；設定主密碼後以主密碼加密。
- **給 Agent 用的伴侶 CLI，v1 規格。** `toolowner note split / join / eval`、`card build`、`guard scan` 與 `undo`，離線執行，支援 `--usage`、`--schema`、`--dry-run`、`--output-format json`，結束碼 0／1／2，每次寫檔都留下可復原的 receipt。請見 [SKILL.md](SKILL.md) 與 [INSTALL_FOR_AGENTS.md](INSTALL_FOR_AGENTS.md)。

### 安全性
- **送外部 AI 前的可逆佔位符。** 金鑰與 Token、My Note 防窺行、Email、路徑與（開啟遮罩時的）電話，在核准卡與請求中（包含欄位）都變成 `{{SECRET_n}}`、`{{EMAIL_n}}`、`{{PATH_n}}`、`{{PHONE_n}}`。回覆在本機還原，對照表隨即從記憶體清空，不儲存、不記錄、不同步。
- **每次重算的風險分級。** Tier 0（唯讀）、Tier 1（本機寫入，並檢查路徑：不得含 `..`、絕對路徑、`~`、磁碟代號、URL scheme 或 NUL）、Tier 2（會送出、刪除或呼叫服務商：一律等你確認）。
- **有上限的重試。** 回覆格式不符時最多再要一次，仍不符就標示為未通過校驗、不套用。
- **防護記錄。** 設定 › 隱私列出最近 50 次外部 AI 呼叫，只有計數，不同步，點兩下即可清除。

## 2026 年 11 月

### 新增
- **My Note 黑科技。** 算式行（`1200 + 350*2 =`、`=SUM(ABOVE)`）、防窺行（`!!` 開頭的行先遮住，點一下才顯示，5 秒後再遮回）、長筆記的章節目錄、待辦的行事曆提醒（.ics）與相關舊筆記。全在本機、0 Token，可在設定 › 資料逐項開關。
- **區域網路直傳（Beta）。** 同一網段的兩台裝置用一次性 6 碼配對與 QR Code，以 WebRTC 直接傳檔，再加一層 AES-256-GCM 並驗證 SHA-256。單檔 50 MB，不經過伺服器，也不使用 STUN／TURN，因此訪客網路或 AP 隔離時可能連不上。
- **早鳥邀請。** 在帳號頁分享邀請連結或 QR Code；好友完成同步設定後，你得 +30、好友得 +15 早鳥積分。邀請碼可以自訂一次。
- **個人連結名片。** 模板工作室用名稱、一句話與 3–8 個連結做出 Link-in-Bio 頁，提供暖白紙感與深墨極簡兩種主題，存成一個不含任何程式碼、所有輸入都經過轉義的靜態 `.html`。
- **模板工作室。** 程式碼模板、Skill、你自己的模型與釘選的微應用集中在一頁；視覺化網頁編輯器；打開時不執行任何程式的純靜態微應用。
- **更多本機工具。** 加密膠囊、浮水印、去陰影掃描與長截圖；情報訂閱在本機解析。
- **舊裝置全遺失時的兩條復原路。** 用復原金鑰接管（連續錯 5 次鎖一小時），或清除雲端副本重新開始。
- **你自己的 AI 服務商。** OpenAI、Anthropic、Google Gemini、OpenRouter 與 BeatAPI（僅 Web 版），或你自己電腦上的模型（Ollama、llama.cpp、PocketPal）。每一次呼叫都要你核准。
- **筆記與待辦。** 回合待辦與議程開關、插入連結時自動移除追蹤參數、編號清單、12–48 pt 與匯入字型。
- **雙軌 OCR、鐵籠 `/code` 指令、@ 引用、待確認收件匣。** 開過一次後，核心 App 離線也能打開（約 3 MB）。

### 安全性
- 同步（Beta）採端對端加密：每筆記錄 AES-256-GCM、同步密碼以 PBKDF2-HMAC-SHA-256 迭代 600,000 次、復原金鑰只顯示一次。詳見 [SECURITY.md](SECURITY.md)。
- 官網在嚴格的內容安全政策（CSP）下執行，不發出任何外部請求。
