# Changelog

**English** · [繁體中文](#更新日誌繁體中文)

What has shipped in the Toolowner web app (https://toolownert1.pages.dev), newest first. Every feature comes with its boundary; anything marked **Beta** is still being checked on real devices. The full list is on the [features page](https://toolowner.pages.dev/features).

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
