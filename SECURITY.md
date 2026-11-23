# Security policy

**English** · [繁體中文](#安全政策繁體中文)

Toolowner is closed-source, so this page states exactly what the product does with your data and how you can check it yourself, without reading the code. It summarises the [security & privacy whitepaper](https://toolowner.pages.dev/security) (Web implementation as of November 2026). If what you observe differs from this document, that is a problem we want to fix.

## Reporting a vulnerability

**Please do not open a public issue for a security problem.**

Use GitHub's private vulnerability reporting: open the **[Security](../../security)** tab of this repository and choose **Report a vulnerability**. Only the maintainer can see the report.

Please include what you found, how to reproduce it (browser, device, steps) and what an attacker could do with it. **Never include a real recovery key, sync passphrase, API key or private note content**, yours or anyone else's: use test accounts and fake values.

We will reply in the advisory, keep you updated while it is being fixed, and credit you when it is published unless you prefer not to be named. Please give us a reasonable time to fix the problem before disclosing it.

In scope: the web app at https://toolownert1.pages.dev, the website at https://toolowner.pages.dev and the sync service they use. Out of scope: reports that need an already compromised device or browser, social engineering, denial of service by volume, and missing headers with no demonstrated impact.

## What stays on your device

By default everything you create (notes, to-dos, saved skills, tool results) is kept in the browser on this device. On-device tools (compression, conversion, PDF and Excel merging, OCR, personal-data masking, Reader typesetting and so on) process content in the browser and send it nowhere.

Outside AI is used only if you set up a provider yourself (BYO API), and every call shows what will be sent and waits for your approval. Highly sensitive data is never sent.

**No ads and no tracking.** Toolowner contains no advertising and no third-party analytics or tracking scripts.

## End-to-end encrypted sync (Beta)

Sync is optional and off until you turn it on. Encryption and decryption happen only on your device, with the browser's built-in WebCrypto; there is no home-made cryptography.

| | |
| --- | --- |
| **Record encryption** | AES-256-GCM, a fresh random 96-bit IV for every record. The associated data binds the user, collection, record id and key version, so the server cannot move or replay ciphertext. |
| **Vault Key** | A random 256-bit key made on the first device. Each collection gets its own subkey via HKDF-SHA-256. |
| **Sync passphrase** | PBKDF2-HMAC-SHA-256, 600,000 iterations, a random salt of at least 16 bytes; NFKC-normalised, at least 12 characters, strength-checked at creation. |
| **Recovery key** | A random 256-bit key shown once, turned into a second lock with HKDF-SHA-256. |
| **Locking the key** | The Vault Key is wrapped with AES-GCM under both locks; only the locked copies reach the server. There is no password verifier on the server to attack. |
| **On the device** | The Vault Key is a non-exportable key object; its raw bytes exist only while unlocking. |
| **New devices** | A new device unlocks the Vault Key itself with the passphrase or recovery key, then waits for an already approved device to tap Approve. |

**What the server can see (metadata):** your sign-in identity and plan, opaque collection labels (not names), record sizes padded into buckets, one-way record ids, random device ids and sync timestamps. Device names are encrypted before upload. The server never sees the content.

**LAN direct transfer (Beta)** pairs two devices on the same network with a one-time 6-digit code and QR codes, makes a one-time key per connection with ECDH, seals the file with AES-256-GCM and checks a SHA-256 hash on arrival. It passes through no server and never touches the sync key.

## Verify it yourself with the Network panel

Open your browser's developer tools (F12, or ⌥⌘I on a Mac), go to the **Network** tab and clear the list.

1. **Local tools send nothing.** Compress a photo, pack a ZIP or format some JSON. No new request should appear (at most a GET for one of the site's own files, such as a script or dictionary, with no request payload).
2. **Search for what you typed.** Type a unique marker such as `TOOLOWNER-CHECK-7F3A` into a local tool and run it, then search the Network panel (Ctrl+F / ⌘F). Expect 0 results in any URL, header, payload or response. The only exception is a call you approved to an outside AI you set up yourself.
3. **It works offline.** Use a tool once, set the throttling menu to **Offline** and repeat. If it still completes, it cannot be sending your content anywhere.
4. **Synced content is ciphertext.** With sync on, open a sync request and look at Payload and Response: you see unreadable data, and the marker from step 2 still finds 0 results.
5. **No trackers.** Reload the page with the Network panel open and check the domains: there are no analytics, advertising or tracking hosts.

## Known limits, stated plainly

- If a sign-in session is stolen, an attacker can fetch the locked Vault Key and guess your sync passphrase offline. PBKDF2 at 600,000 iterations and a strong passphrase are the barrier, so please use a long, unique one.
- The metadata listed above is visible to the server.
- "Start over", for when every old device is lost, needs only a signed-in session, so a stolen session could delete the cloud copy of your sync data (never the notes on any device). A cancellable delay is not built yet.
- Recovery-key takeover is rate-limited: five wrong tries in a row lock it for an hour, and every try is logged.
- Key rotation is not implemented yet, and neither is pairing that hands the sync key to a new device by QR code.
- No third-party security audit report is available at this time.
- A compromised device or browser is out of scope: local data can be read in that case too.

---

# 安全政策（繁體中文）

Toolowner 不公開原始碼，所以這份文件直接說清楚產品怎麼處理你的資料，以及你不必讀程式碼、也能自己檢查的方法。內容整理自[安全與隱私白皮書](https://toolowner.pages.dev/security)（2026 年 11 月的 Web 版實作）。如果你觀察到的與這裡寫的不同，那就是我們該修的問題。

## 回報安全漏洞

**請不要為安全性問題開公開 Issue。**

請使用 GitHub 的私密漏洞回報：打開本倉庫的 **[Security](../../security)** 分頁，選擇 **Report a vulnerability**。只有維護者看得到你的回報。

請附上你發現的問題、重現方式（瀏覽器、裝置、步驟），以及攻擊者可能做到的事。**絕對不要附上真實的復原金鑰、同步密碼、API 金鑰或私人筆記內容**，不論是你的還是別人的；請用測試帳號與假資料。

我們會在該則 advisory 中回覆、在修復期間持續更新，並在公開時列名致謝（若你不希望具名也可以）。公開揭露前，請給我們合理的修復時間。

範圍：體驗版 https://toolownert1.pages.dev、官網 https://toolowner.pages.dev，以及它們使用的同步服務。不在範圍內：需要裝置或瀏覽器已遭入侵才成立的問題、社交工程、大量請求造成的阻斷服務，以及沒有實際影響的標頭缺漏。

## 留在你裝置上的資料

預設情況下，你建立的一切（筆記、待辦、已存的技能、工具結果）都只存在這台裝置的瀏覽器。本機工具（壓縮、轉檔、合併 PDF 與 Excel、OCR、個資遮罩、Reader 排版等）都在瀏覽器裡處理，不會把內容送到任何地方。

只有你自己設定外部 AI 服務商（BYO API）時才會用到外部 AI，而且每一次呼叫都會先顯示要送出的內容，等你核准；高度敏感的資料不會外送。

**沒有廣告，沒有追蹤。** Toolowner 不放廣告，也沒有任何第三方分析或追蹤程式。

## 端對端加密同步（Beta）

同步是選用的，預設關閉。加密與解密只發生在你的裝置上，由瀏覽器內建的 WebCrypto 執行，沒有自製的密碼學。

| | |
| --- | --- |
| **記錄加密** | AES-256-GCM，每筆記錄使用全新的隨機 96-bit IV。附帶資料綁定使用者、類別、記錄 ID 與金鑰版本，伺服器無法搬移或重放密文。 |
| **保險庫金鑰** | 第一台裝置產生的隨機 256-bit 金鑰；每個類別再以 HKDF-SHA-256 衍生子金鑰。 |
| **同步密碼** | PBKDF2-HMAC-SHA-256、600,000 次迭代、至少 16 bytes 的隨機鹽；先做 NFKC 正規化，建立時至少 12 個字元並檢查強度。 |
| **復原金鑰** | 只顯示一次的隨機 256-bit 金鑰，以 HKDF-SHA-256 轉成第二把鎖。 |
| **上鎖金鑰** | 保險庫金鑰以 AES-GCM 分別用兩把鎖上鎖，伺服器只收到上鎖的版本；伺服器上沒有可供攻擊的密碼驗證值。 |
| **裝置上** | 保險庫金鑰是不可匯出的金鑰物件，原始位元組只在解鎖的瞬間存在。 |
| **新裝置** | 新裝置用同步密碼或復原金鑰自己解開保險庫金鑰，再等一台已核准的裝置按下「核准」。 |

**伺服器看得到的（metadata）：**你的登入身分與方案、不透明的類別標籤（不是名稱）、補齊級距後的記錄大小、單向的記錄 ID、隨機的裝置 ID 與同步時間。裝置名稱在上傳前已加密。伺服器看不到內容。

**區域網路直傳（Beta）**：同一網段的兩台裝置用一次性 6 碼配對與 QR Code 連線，每次連線以 ECDH 產生一次性金鑰，檔案以 AES-256-GCM 加密，收到後驗證 SHA-256。不經過任何伺服器，也不會碰到同步金鑰。

## 用 Network 面板自己驗證

打開瀏覽器的開發者工具（F12，Mac 為 ⌥⌘I），切到 **Network** 分頁並清空清單。

1. **本機工具不外送。** 壓縮一張照片、打包一個 ZIP 或格式化一段 JSON。清單不應出現新的請求（最多是載入網站自己檔案的 GET，例如程式或詞庫，而且沒有 Request Payload）。
2. **搜尋你輸入的文字。** 在本機工具輸入獨一無二的標記，例如 `TOOLOWNER-CHECK-7F3A` 並執行，再在 Network 面板按 Ctrl+F／⌘F 搜尋。所有網址、標頭、內容與回應都應該是 0 筆。唯一的例外，是你核准、送往你自己設定的外部 AI 的那次呼叫。
3. **離線也能用。** 先用一次工具，再把節流選單改成 **Offline** 重做一次。離線仍能完成，就不可能把內容送出去。
4. **同步內容是密文。** 開啟同步後，點開同步請求查看 Payload 與 Response：看到的是無法閱讀的資料，用步驟 2 的標記搜尋仍是 0 筆。
5. **沒有追蹤器。** 開著 Network 面板重新整理頁面，檢查所有網域：沒有分析、廣告或追蹤服務。

## 已知限制，直接說明

- 如果登入 session 被竊，攻擊者可以取得上鎖的保險庫金鑰，離線猜測你的同步密碼。PBKDF2 600,000 次迭代加上高強度密碼是唯一的屏障，請使用夠長、不重複的密碼。
- 上面列出的 metadata 伺服器看得到。
- 所有舊裝置都遺失時的「重新開始」只需要登入的 session，因此被竊的 session 可以刪除同步資料的雲端副本（但永遠刪不到任何裝置上的筆記）。可取消的延遲刪除尚未實作。
- 復原金鑰接管有速率限制：連續錯 5 次會鎖一小時，每次嘗試都有紀錄。
- 金鑰輪替尚未實作；用 QR Code 把同步金鑰交給新裝置的配對也還沒有。
- 目前沒有第三方安全稽核報告。
- 裝置或瀏覽器本身遭入侵不在保護範圍內，這種情況下本機資料一樣會被讀取。
