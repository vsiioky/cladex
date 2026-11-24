# Cladex

[English](README.md) | [Русский](README.ru.md) | [Deutsch](README.de.md) | [Français](README.fr.md) | [Español](README.es.md) | [Italiano](README.it.md) | [简体中文](README.zh-Hans.md) | **繁體中文** | [日本語](README.ja.md) | [한국어](README.ko.md)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/cladex)

Cladex 是一個遙控器，用 Even G2 眼鏡查看並控制在你自己的電腦上工作的 AI 代理程式。

- 你在每台執行 AI 代理程式的電腦上安裝一個程式。它是有自己視窗的 Mac app。
- 眼鏡（透過手機上的 Even app）會顯示你的代理程式、它們的工作階段和提問，你可以用觸控或語音來回答。
- 一切都從手機直接送到你自己的電腦，使用各台電腦自己的網址。沒有 Cladex 伺服器，也沒有 Cladex 帳號。
- 支援 Claude Code、Codex、Hermes 和 OpenClaw。
- 這個儲存庫只有安裝檔和說明。原始碼不公開。

## 讓你的 AI 代理程式來安裝

如果你在這台電腦上使用的 AI 代理程式可以使用終端機（Claude Code、Codex、Hermes、OpenClaw 或其他），可以讓它來完成安裝。把下面這段文字複製給代理程式：

```
Install Cladex on this computer. Read https://raw.githubusercontent.com/vsiioky/cladex/main/AGENT-INSTALL.md and follow it step by step. Stop and ask me where it says so. Answer me in Traditional Chinese.
```

代理程式會從這個儲存庫下載 Cladex，完成設定，並自行把你的代理程式和手機連起來。遇到只有你才能繼續的地方，它會停下來詢問：登入 Tailscale、把電腦的網址開放到網際網路（動手之前會先問你）、Hermes 和 OpenClaw（需要你同意）、語音金鑰（你在隱藏輸入的提示裡自己輸入，絕不會寫進聊天）、Claude app 裡的調度器，以及手機上的連結碼。它從不使用管理員權限。

請先閱讀 [AGENT-INSTALL.md](AGENT-INSTALL.md)：它很短，代理程式正是照著它來做。對於無法連上網際網路的代理程式，可以直接把這個檔案交給它，而不是給它網址。

## 你需要準備什麼

- 搭載 Apple 晶片（M1 或更新）的 Mac，系統為 macOS 15 或更新。Linux 和 Windows 是沒有視窗的預覽版（見「安裝」）；搭載 Intel 晶片的 Mac 目前還沒有安裝檔。
- 一個個人使用的免費 Tailscale 帳號（tailscale.com/download/mac）。它為電腦提供網際網路上的網址。手機上不需要安裝 Tailscale。
- 電腦上至少有一個已登入的 AI 代理程式：Claude Code（claude.com/download）、Codex（developers.openai.com/codex/app）、Hermes（hermes-agent.nousresearch.com/docs/getting-started/installation）或 OpenClaw（docs.openclaw.ai/install）。Claude Code 需要付費的 claude.ai 方案。
- Even G2 眼鏡，以及手機上的 Even app。

## 安裝

請選擇你的電腦。每種電腦有各自的指令和執行方式。

### 搭載 Apple 晶片的 Mac（M1 或更新）

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

執行方式：

1. 按 Cmd+空白鍵，輸入「終端機」（Terminal），然後按 Enter。會打開一個有文字輸入列的視窗。
2. 複製上面的指令，貼到這個視窗裡（Cmd+V），然後按 Enter。
3. 等它說明做了什麼。這個腳本從不索取你的密碼。

接下來你會看到：Cladex 的視窗會打開，一步一步帶你完成第一次設定（見下面一節）。

腳本做了什麼：下載磁碟映像檔，檢查它的檢查碼、簽章以及 Apple 的公證，把 Cladex.app 複製到「應用程式」，關閉映像檔，然後打開 Cladex。檢查全部通過之前，它不會更動任何東西。如果 /Applications 無法寫入，它會改用你家目錄裡的 Applications 檔案夾，並告訴你。如果 Cladex 正在執行，它會請你先結束它。選項：`--no-open`、`--dir <folder>`、`--help`（寫在指令後面：`| sh -s -- --no-open`）。

手動安裝：打開 https://github.com/vsiioky/cladex/releases，下載 cladex-arm64.dmg，打開它，把 Cladex 拖到「應用程式」，然後從那裡打開。同一頁面上的 SHA256SUMS 可用來核對檢查碼（`shasum -a 256 cladex-arm64.dmg`）。

狀態：已在真實的 Mac 上，用該版本已簽署並經過公證的磁碟映像檔驗證。

### 搭載 Intel 晶片的 Mac

目前還沒有安裝檔。執行同一個指令，它會用一句話說明這一點，並且不做任何更動就停止。請留意發行頁面上的消息。

### Linux（x64 和 arm64），預覽版

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

執行方式：

1. 打開終端機（大多數桌面環境中按 Ctrl+Alt+T，或在程式選單裡找「終端機」）。
2. 複製上面的指令，貼上（Ctrl+Shift+V），然後按 Enter。
3. 回答同一視窗裡出現的問題。你回答之前不會有任何更動。

接下來你會看到：沒有視窗。腳本把 Cladex 放在 ~/.g2-claude 底下，把 `cladex` 指令加入你的路徑，並啟動 `cladex setup`，它會在終端機裡提問。結束後，依序執行這些指令：`cladex gateway init`，然後 `cladex gateway publish`，再 `cladex pair`（它會印出電腦的網址和一組連結碼）。如果只想安裝，在 `| sh -s --` 後面加上 `--no-setup`。它需要 curl、tar、gzip 和 xz（套件 xz-utils），從不使用 sudo，並會自己下載 Node.js 22 並檢查其檢查碼。

狀態：預覽版。已在 Debian 容器（arm64）裡測試：安裝、`cladex --version` 和 `cladex setup --print`。尚未在真實的 Linux 電腦、真實的服務（systemd）、Tailscale 或代理程式上測試。

### Windows 10 和 11，預覽版

```powershell
irm https://github.com/vsiioky/cladex/releases/latest/download/install.ps1 | iex
```

執行方式：

1. 打開「開始」選單，輸入 PowerShell，然後按 Enter（是一般視窗，不要選「以系統管理員身分執行」）。
2. 複製上面的指令，貼上（按滑鼠右鍵即可貼上），然後按 Enter。
3. 回答同一視窗裡出現的問題。你回答之前不會有任何更動。

接下來你會看到：不會出現 Cladex 的視窗。腳本把 Cladex 放在你的使用者檔案夾底下（.g2-claude），把它的指令檔案夾加入你使用者的路徑，並啟動 `cladex setup`，它會在 PowerShell 裡提問。結束後執行：`cladex gateway init`，然後 `cladex gateway publish`，再 `cladex pair`。如果只想安裝，在執行那一行之前先設定 `$env:CLADEX_NO_SETUP = '1'`。不使用系統管理員權限。

狀態：預覽版。腳本只經過人工閱讀和靜態測試：還沒有在真實的 Windows 電腦上執行過，而且在撰寫它的那台機器上，PowerShell 也沒有解析過它。

## 第一次設定

在 Mac 上，Cladex 的視窗會指出每一步；在 Linux 和 Windows 上，由終端機裡的 `cladex setup` 和 `cladex status` 指出。簡要如下：

1. 打開 Cladex。閱讀安裝計畫，回答它的那一個問題。你回答之前不會有任何更動。
2. 安裝 Tailscale（tailscale.com/download/mac），打開並登入。如果電腦的名稱裡有你自己的名字，請替電腦改名。
3. 在瀏覽器裡打開 Tailscale 的頁面：開啟 MagicDNS 和「Enable HTTPS」（console.tailscale.com/admin/dns），並把 Funnel 加入政策（console.tailscale.com/admin/acls）。
4. 在 Cladex 裡按「發布網址」，並抄下電腦的網址。它的形式類似 name.tailnet.ts.net，最多可能需要 10 分鐘才會出現在網際網路上。
5. 安裝上面清單中的一個 AI 代理程式並登入。Cladex 不會安裝其他程式，按「重新檢查」後會自己找到代理程式。對於 Claude Code，視窗裡還會出現一次性的調度器步驟。
6. 語音是選用的，需要你自己的 ElevenLabs（elevenlabs.io/app/settings/api-keys）或 OpenAI（platform.openai.com/api-keys）金鑰。把它貼到 Cladex 的設定裡。

## 眼鏡用的 app

眼鏡上的 Cladex app 在 Even 的測試版管道中。在 Even 把它列入 app 目錄之前，需要受邀才能使用，邀請會寄到你 Even 帳號的電子郵件信箱。要申請邀請，請在這個儲存庫（https://github.com/vsiioky/cladex/issues）裡建立一個 issue，標題寫「Beta invitation」。請不要在 issue 裡寫你的電子郵件：issue 是公開的，回覆中會說明如何私下傳送電子郵件。收到邀請後，在手機上的 Even app 裡安裝測試版。

## 連結手機

1. 在電腦上的 Cladex 裡按「連結手機」：會出現電腦的網址和一組 8 位數連結碼。
2. 在手機上 Even app 裡的 Cladex app 中輸入網址和連結碼，然後輸入電腦上顯示的 3 位數。
3. 戴上眼鏡。如果顯示「沒有電腦」，點一下眼鏡的畫面：清單會重新檢查。

## 更新

再次執行你那台電腦的安裝指令：在 Mac 上必須先結束正在執行的 Cladex，舊版本會被取代。在 Linux 和 Windows 上，`cladex update` 會自己完成同樣的事：下載最新發行版，核對檢查碼，放到正在執行的副本旁邊並重新啟動服務；如果新版本沒有回應，服務會自己退回上一個版本。你的設定和你的手機都會保留。

Cladex 每天向 GitHub 詢問一次是否有更新的發行版（GitHub 只看得到你在網際網路上的位址和 Cladex 的版本，其他都看不到），有的話 `cladex status` 會告訴你。`cladex update check off` 關閉這項檢查，`cladex update check on` 重新開啟。檢查關閉期間，安全問題與錯誤的修正不會送達，也不會有任何東西告訴你有新版本，而眼鏡上透過 Even 自動更新的應用程式，可能無法再辨識電腦上的舊版本。只有你用 `cladex update auto on` 允許之後，Cladex 才會自己安裝新版本；`cladex update auto off` 可以再次禁止。`cladex update status` 會顯示以上全部。

## 移除

在 Cladex 裡打開設定，找到「移除」群組，按「從這台電腦移除 Cladex...」。或者在終端機裡執行 `cladex uninstall`：它會移除 Cladex 安裝的所有東西（服務、掛鉤、設定、金鑰、記錄）。然後把 Cladex.app 移到垃圾桶。Tailscale 和你的 AI 代理程式都會保留。

## 隱私

- 沒有 Cladex 伺服器，也沒有帳號。開發者不會從 app 或程式收到任何資料。
- 沒有分析，沒有廣告，沒有追蹤。
- 你的語音只送到你自己的電腦，再由電腦用你自己的金鑰送給語音服務。

全文：[PRIVACY.md](PRIVACY.md)（英文）。使用條款：[TERMS.md](TERMS.md)（英文）。

## 關於

Cladex 的原始碼不公開。Cladex 是獨立專案，與 Anthropic、OpenAI、Nous Research、OpenClaw、Even Realities 或 Tailscale 沒有關聯，也未獲得它們的認可。產品名稱屬於各自的擁有者。問題與回報：請到這個儲存庫的 Issues。

## 支持 Cladex

Cladex 是免費的，而且會一直免費。如果它對你有幫助，你可以支持它的開發：ko-fi.com/cladex。
