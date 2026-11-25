<div align="center">

<a href="https://toolowner.pages.dev">
  <img src="https://toolowner.pages.dev/icons/icon-192.png" width="96" height="96" alt="Toolowner">
</a>

<h1>Toolowner</h1>

<p><b>Less AI. Better System.</b><br>
本地優先的個人能力層：工具、筆記與對話收在同一個私人工作區，<br>外部 AI 只補真正需要它的空缺。</p>

<p>
  <a href="README.md">English</a> · <b>繁體中文</b>
</p>

<p>
  <a href="https://toolowner.pages.dev"><img alt="官網" src="https://img.shields.io/badge/%E5%AE%98%E7%B6%B2-toolowner.pages.dev-1B1E1C?style=flat-square"></a>
  <a href="https://toolownert1.pages.dev"><img alt="體驗版" src="https://img.shields.io/badge/%E9%AB%94%E9%A9%97%E7%89%88-%E7%AB%8B%E5%8D%B3%E8%A9%A6%E7%94%A8-2E6A4E?style=flat-square"></a>
  <a href="LICENSE"><img alt="授權：封閉原始碼" src="https://img.shields.io/badge/%E6%8E%88%E6%AC%8A-%E5%B0%81%E9%96%89%E5%8E%9F%E5%A7%8B%E7%A2%BC-675E56?style=flat-square"></a>
  <a href="SECURITY.md"><img alt="端對端加密同步" src="https://img.shields.io/badge/%E5%90%8C%E6%AD%A5-AES--256--GCM%20E2EE-4A33B3?style=flat-square"></a>
  <a href="https://buymeacoffee.com/derexlee"><img alt="請我喝杯咖啡" src="https://img.shields.io/badge/%E8%B4%8A%E5%8A%A9-Buy%20me%20a%20coffee-FFDD00?style=flat-square&logo=buymeacoffee&logoColor=1B1E1C"></a>
</p>

<p>
  <a href="https://toolowner.pages.dev"><b>前往官網 →</b></a>
  &nbsp;&nbsp;·&nbsp;&nbsp;
  <a href="https://toolownert1.pages.dev"><b>打開體驗版：登入或使用邀請連結 →</b></a>
</p>

</div>

---

> [!IMPORTANT]
> **Toolowner 是封閉原始碼的商業軟體（Closed-Source / Proprietary）。** 這個倉庫**不包含**產品的原始碼，
> 僅用於產品說明、[更新日誌](CHANGELOG.md)、[安全政策](SECURITY.md)與社群問題回報。
> 授權說明請見 [LICENSE](LICENSE)。

## 為什麼是 Toolowner

多數 AI 工具把所有內容送上伺服器，每一次都按請求計費。Toolowner 反過來做：能用固定規則在你的裝置上算完的事，就在本機完成，不花錢，離線也能用。外部 AI 只在你自己設定之後才會用到，而且每一次呼叫都要你核准。

| | 一般的雲端 AI 工具 | Toolowner 本機工具 |
| --- | --- | --- |
| **你的內容** | 上傳到對方的伺服器 | 留在這台裝置 |
| **每次執行** | 一次網路請求，按 Token 計費 | 0 次請求 · 0 Token |
| **結果** | 同一段文字也可能不同 | 固定規則：同樣輸入，同樣輸出 |
| **離線時** | 無法使用 | 開過一次後，離線也能從頭打開 |

## 它能做什麼

**01 · 本地優先，登入即可開始。** 用好友的邀請連結或直接登入啟用帳號，就能累積早鳥積分、選擇開啟端對端加密同步。工具在你的瀏覽器裡執行，內容預設只存在這台裝置；能在本機算的，就不問 AI。

**02 · My Note：會算，也會遮。** 在筆記寫 `1200 + 350*2 =` 就有答案，`=SUM(ABOVE)` 加總上面幾行；`!!` 開頭的防窺行先遮住，點一下才顯示，5 秒後再遮回。兩種讀法：**整頁**（整篇）或**分塊**（長筆記依標題切成編號卡片，一次讀寫一塊，像電子書）；無論哪種，筆記都還是同一份 Markdown。標籤收合成一行。另外還有章節目錄、待辦的行事曆提醒（.ics）與相關舊筆記。全在本機，0 Token。

**03 · 端對端加密同步，區域網路直傳。** 同步（Beta）是選用的：內容在你的裝置上用 AES-256-GCM 加密後才上傳，伺服器只拿到密文。同一個網段的兩台裝置，可以用 WebRTC 直接傳檔，不經過伺服器（Beta）。

**04 · Studio：靜態微應用與個人連結名片。** 把做好的頁面釘成純靜態微應用，打開時不執行任何程式；填好名稱與 3–8 個連結，存成一個不含程式碼的 `.html` 名片，放到你自己的空間。

其他還有：合併 PDF 與 Excel、圖片與影片壓縮、ZIP 打包、JSON 格式化、繁簡轉換、OCR、個資遮罩與連結清洗、斜線命令、可重複使用的配方，以及你自己的 AI 服務商（OpenAI、Anthropic、Google Gemini、OpenRouter，或你自己電腦上的模型）。每一項功能與它的邊界，都寫在[全部功能](https://toolowner.pages.dev/features)頁。

### 2026 年 11 月下旬新增

- **My Note 整頁與分塊。** 長筆記切到分塊，就成為編號卡片（標題、一行摘要、行數）；打開一塊直接寫，用「上一塊 · 下一塊」翻頁。存下來的筆記完全不變：同步、加密與 `.md` 匯出看到的是同一份文字。
- **送外部 AI 前的可逆佔位符。** 金鑰與 Token、`!!` 防窺行、Email、你電腦上的路徑，以及（開啟遮罩時的）電話，在核准卡與請求裡都變成 `{{SECRET_1}}`、`{{EMAIL_1}}`、`{{PATH_1}}`、`{{PHONE_1}}`。回覆在你的裝置上還原，原值對照表隨即從記憶體清空。每個動作每次都重新分為 Tier 0／1／2；會送出、刪除或呼叫服務商的，一律等你確認。
- **會冷卻的備用路線。** 自備 API 金鑰並設定備用後，回 429、伺服器錯誤或逾時的路線會先冷卻一段時間，下一次呼叫從沒有冷卻的路線開始。它只調整你核准過的路線順序。
- **AI 上下文的版本紀錄。** 附加到對話的內容在本機最多保留 20 版：任一版都能和畫面上的內容比對，也能還原（還原前會先把目前內容存成一版）。不會同步；設定主密碼後以主密碼加密。
- **防護記錄。** 設定 › 隱私列出最近 50 次外部 AI 呼叫，只有計數（路線、遮了幾項、Tier、校驗結果），沒有任何內容。
- **給 Agent 用的伴侶 CLI（v1 規格）。** `toolowner note split / join / eval`、`toolowner card build`、`toolowner guard scan` 與 `toolowner undo`：把 App 本身的 My Note、連結名片與脫敏函式帶到命令列，離線執行，支援 `--dry-run`、`--schema`、JSON 輸出，每次寫檔都有可復原的 receipt。請見 [SKILL.md](SKILL.md) 與 [INSTALL_FOR_AGENTS.md](INSTALL_FOR_AGENTS.md)。

## 隱私與安全摘要

- **資料預設留在本機。** 筆記、待辦與工具處理的內容，預設只存在這台裝置的瀏覽器。本機工具不發出請求，離線也照樣能用。
- **同步時端對端加密。** 每筆記錄使用 AES-256-GCM 與全新的 96-bit IV；保險庫金鑰是隨機 256-bit；同步密碼以 PBKDF2-HMAC-SHA-256 迭代 600,000 次；復原金鑰只顯示一次。加密只在你的裝置上、由瀏覽器內建的 WebCrypto 執行。
- **送出去的是佔位符，不是機密。** 核准外部 AI 呼叫前，金鑰、防窺行、Email 與本機路徑都換成編號佔位符，只在你的裝置上還原。偵測是規則式的：不認得格式的機密不會被找到。
- **沒有廣告，沒有追蹤。** 不放廣告，也不裝第三方分析或追蹤程式。只有你自己設定外部 AI（BYO API）並核准那次呼叫，內容才會送到你選的服務商。
- **誠實說明：** 開啟同步後，伺服器看得到你的登入身分與方案、不透明的類別標籤、補齊級距後的記錄大小、記錄與裝置的隨機 ID，以及同步時間；看不到內容與裝置名稱。

細節、已知限制，以及如何用瀏覽器的 Network 面板自己檢查：**[SECURITY.md](SECURITY.md)** 與[安全與隱私白皮書](https://toolowner.pages.dev/security)。

## 回報問題或提出建議

- 🐞 **錯誤回報：**[開一則 Bug 回報](../../issues/new?template=bug_report.yml)
- 💡 **功能建議：**[提出功能建議](../../issues/new?template=feature_request.yml)
- 🔒 **安全性問題：**請**不要**開公開 Issue，依照 [SECURITY.md](SECURITY.md) 私下回報。

> [!WARNING]
> 請勿在 Issue 貼上任何復原金鑰、同步密碼、API 金鑰或私人筆記內容。Issue 是公開的。

## 贊助 Toolowner

Toolowner 是獨立開發的產品。如果它幫你省下時間，歡迎支持後續開發：

<a href="https://buymeacoffee.com/derexlee"><img alt="請我喝杯咖啡" src="https://img.shields.io/badge/Buy%20me%20a%20coffee-derexlee-FFDD00?style=for-the-badge&logo=buymeacoffee&logoColor=1B1E1C"></a>

更多贊助方式（OEN 應援、綠界 ECPay）即將加入。

## 授權

Copyright © 2026 Toolowner. 版權所有。Toolowner 為封閉原始碼的商業軟體；本倉庫的任何內容都不授予產品或其原始碼的使用授權。詳見 [LICENSE](LICENSE)。
