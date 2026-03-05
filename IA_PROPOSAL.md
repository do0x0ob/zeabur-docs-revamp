# Zeabur Docs IA 重構提案

> 依據 brief 三大目標（AI Agent Wiki、In-app CTA、降低支援成本）與內部提案架構設計。

---

## 架構總覽

**I. 入門**

- Zeabur 是什麼
- 快速入門
- 依需求開始 🆕
- 為什麼選擇 Zeabur 🆕
- 最佳實踐 🆕
- 遷移與導入
  - 從其他平台遷移（Heroku、Railway…）🆕
  - 從共享叢集遷移到專用伺服器 🆕
  - 從 AI 開發工具導入（v0、Replit、Lovable、Bolt…）
  - 從 GitHub 導入
- 常見問題 → Forum

**II. 部署與服務**

- *伺服器*
  - 專用伺服器概述
  - 註冊伺服器
  - 維護伺服器
- *專案*
  - 建立專案
  - 成員管理
  - 預算設定
  - 用量分析
  - 安全報告
  - 複製專案
  - 匯出專案
- *服務*
  - 部署流程概述 🆕
  - 建立服務
  - 環境變數
  - GitHub 整合
  - Dockerfile 部署
  - 自訂映像檔
  - 根目錄設定
  - 觸發路徑
  - 執行命令
  - 更新映像引用
- *模板*
  - 從模板部署 🆕
  - 用 YAML 建立模板
  - 一鍵部署按鈕
  - 模板目錄（外連）
- *特色服務*
  - Zeabur AI Hub（+ n8n、SillyTavern 整合）
  - Zeabur Email（概述、快速開始、API、網域、金鑰、Webhook）
  - MCP 整合
  - InsForge

**III. 基礎設施**

- 資料管理（儲存空間、設定檔、檔案管理、備份、還原）
- 網路（公網、內網、高可用性）

**IV. 開發者工具**

- API 金鑰 / 開放 API / WebSocket 指南
- 構建原理
- CLI 部署
- Chrome 插件（含從 Gemini 部署）
- Raycast 插件
- VS Code 插件

**V. 語言與框架指南**（AI-first）

- Node.js / Bun / Java / PHP / Python / Go / Deno / Rust / Swift / Dart / 靜態網頁 / .NET

**VI. 帳務與法律**

- 定價 / 方案 / 訂閱 / 贊助 / 兌換預付卡
- 濫用回報指引 / 公平使用指南 / 隱私權政策 / 服務條款

**VII. 社群**

- 論壇 / 推薦計畫 / 貢獻獎勵 / 帳號驗證 / 尋求幫助（同時在 I. 入門設入口）

---

## 分類邏輯

**為什麼這樣分？**

現有文檔按「功能模組」分類（部署、網路、管理…），但用戶查文檔的心態是「我要做什麼」，不是「這屬於哪個模組」。所以改按**查閱動機**分區：


| 用戶心態           | 對應區塊       |
| -------------- | ---------- |
| 「我剛來，想試試看」     | I. 入門      |
| 「我要部署東西」       | II. 部署與服務  |
| 「我要設定基礎設施」     | III. 基礎設施  |
| 「我要串 API 或自動化」 | IV. 開發者工具  |
| 「我卡在某個框架」      | V. 語言與框架指南 |


**為什麼部署區要按伺服器 → 專案 → 服務拆？**

Zeabur 的產品架構本身就是三層：伺服器包含專案，專案包含服務。但現有文檔把「建立專案」和「建立服務」塞在同一個 `deploy/` 裡，成員管理和預算又放在另一個 `manage/`。用戶不知道「變數」是專案層還是服務層的。按產品架構拆開，每一層的設定項自然歸位。

**AI-first vs Human-first 怎麼分？**

需要在 UI 裡點按鈕的操作（建立帳號、綁定域名、模板部署）→ Human-first，需要截圖和步驟。可以用文字描述完整的技術內容（框架設定、API 參考、錯誤排除）→ AI-first，重點是結構化和語意索引。

**語言與框架指南為什麼獨立？**

這些指南是 AI agent 最常被問到的內容（「怎麼部署 Next.js」），獨立出來讓 AI 更容易索引。內容本身品質不錯，不需要大改，但歸類要清楚。

---

## 優先改寫 / 新增評估

根據 brief 的三大目標和現有文檔缺口，以下是我認為最值得投入的：

### 🔴 最優先（影響大、目前缺口明顯）

**1. 快速入門 ✏️ 改寫**

- 原因：這是所有新用戶的第一站，目前花太多篇幅在註冊流程，魔法時刻來得太晚
- 現狀：內容還不錯但篇幅較長，需要重新抓重點
- 目標：30 秒內讓用戶體驗到「哦，東西上線了」

**2. 從模板部署 🆕 新增**

- 原因：模板是 Zeabur 最低門檻的入口，卻沒有教學
- 現狀：不存在
- 目標：最短路徑從模板到服務上線

**3. 部署流程概述 🆕 新增**

- 原因：部署知識散落在 create-service、github、watch-paths 等篇，沒有一篇完整的 reference。AI agent 回答部署問題時沒有單一可索引的來源
- 現狀：不存在
- 目標：一問一標題，結構化 reference

### 🟡 次優先（有價值但急迫性較低）

**4. 依需求開始（情境分流）🆕**

- 幫不同背景的用戶找到對的起點，降低跳出率

**5. 從共享叢集遷移到專用伺服器 🆕**

- 2026-04-01 截止日逼近，用戶需要指引（但 Blog 有了，優先級下降）

**6. AI 對話窗口引導文 🆕**

- Zeabur 的產品差異化在 AI，但用戶可能不知道 AI 能做什麼

### 🟢 可以之後再加

- 從其他平台遷移（Heroku、Railway…）
- 為什麼選擇 Zeabur
- 最佳實踐

---

## 詳細對照

狀態：✅ 保留 | 🔀 搬移 | ✏️ 改寫 | 🆕 新增 | 📛 建議改名

### I. 入門


| 新位置          | 原始路徑               | 狀態  | 改名說明                  |
| ------------ | ------------------ | --- | --------------------- |
| Zeabur 是什麼   | `index` 基本介紹       | 📛  | 「基本介紹」太模糊，改為明確的產品說明標題 |
| 快速入門         | `get-started` 快速開始 | ✏️  | 砍註冊篇幅，聚焦魔法時刻          |
| 依需求開始        | 無                  | 🆕  | 情境分流，幫用戶找到對的起點        |
| 為什麼選擇 Zeabur | 無                  | 🆕  |                       |
| 最佳實踐         | 無                  | 🆕  |                       |


#### 遷移與導入


| 新位置                      | 原始路徑                 | 狀態  | 改名說明              |
| ------------------------ | -------------------- | --- | ----------------- |
| 從其他平台遷移（Heroku、Railway…） | 無                    | 🆕  |                   |
| 從共享叢集遷移到專用伺服器            | 無                    | 🆕  |                   |
| 從 v0 導入                  | `tutorials/v0`       | 🔀  |                   |
| 從 Replit 導入              | `tutorials/replit`   | 🔀  |                   |
| 從 Lovable 導入             | `tutorials/lovable`  | 🔀  |                   |
| 從 Bolt 導入                | `tutorials/bolt`     | 🔀  |                   |
| 從 Emergent 導入            | `tutorials/emergent` | 🔀  |                   |
| 從 AI Studio 導入           | `tutorials/aistudio` | 🔀  |                   |
| 從 GitHub 導入              | `tutorials/github`   | 🔀  |                   |
| 常見問題 → Forum             | `community/help`     | 🔀  | 提升到入門區入口，社群區保留原連結 |


---

### II. 部署與服務

#### 伺服器


| 新位置     | 原始路徑                        | 狀態  | 改名說明 |
| ------- | --------------------------- | --- | ---- |
| 專用伺服器概述 | `dedicated-server.mdx`      | ✅   |      |
| 註冊伺服器   | `dedicated-server/register` | ✅   |      |
| 維護伺服器   | `dedicated-server/operate`  | ✅   |      |


#### 專案


| 新位置  | 原始路徑                     | 狀態   | 改名說明                    |
| ---- | ------------------------ | ---- | ----------------------- |
| 建立專案 | `deploy/create-project`  | 🔀   | 從 deploy/ 移入專案層         |
| 成員管理 | `manage/invite`          | 🔀📛 | 「邀請成員」→「成員管理」，更通用       |
| 預算設定 | `manage/budget`          | 🔀📛 | 「預算」→「預算設定」，動作更明確       |
| 用量分析 | `manage/metric`          | 🔀📛 | 「使用量分析」→「用量分析」，精簡       |
| 安全報告 | `manage/security-report` | 🔀   |                         |
| 複製專案 | `deploy/copy-project`    | 🔀   | 從 deploy/ 移入專案層（專案層級操作） |
| 匯出專案 | `deploy/export-project`  | 🔀   | 從 deploy/ 移入專案層         |


#### 服務


| 新位置           | 原始路徑                            | 狀態  | 改名說明                         |
| ------------- | ------------------------------- | --- | ---------------------------- |
| 部署流程概述        | 無（分散各處）                         | 🆕  | 概念先行，供 AI 索引                 |
| 建立服務          | `deploy/create-service`         | ✅   |                              |
| 環境變數          | `deploy/variables`              | 🔀  | 歸入服務層（變數是 per-service scope） |
| GitHub 整合     | `deploy/github`                 | 📛  | 「整合 GitHub」→「GitHub 整合」，名詞在前 |
| Dockerfile 部署 | `deploy/dockerfile`             | ✅   |                              |
| 自訂映像檔         | `deploy/customize-prebuilt`     | 📛  | 「自訂 Docker 映像檔」→「自訂映像檔」，精簡   |
| 根目錄設定         | `deploy/root-directory`         | 📛  | 「自訂根目錄」→「根目錄設定」，統一用「設定」      |
| 觸發路徑          | `deploy/watch-paths`            | ✅   |                              |
| 執行命令          | `deploy/command-execution`      | 🔀  | 從 deploy/ 移入服務層              |
| 更新映像引用        | `deploy/update-image-reference` | 🔀  | 從 deploy/ 移入服務層              |


#### 模板


| 新位置         | 原始路徑                             | 狀態  | 改名說明                            |
| ----------- | -------------------------------- | --- | ------------------------------- |
| 從模板部署       | `/template/deploy-template`（404） | 🆕  | 被 create-service 連結但頁面不存在       |
| 用 YAML 建立模板 | `template/template-in-code`      | 📛  | 「從 YAML 建立模板」→「用 YAML 建立模板」，口語化 |
| 一鍵部署按鈕      | `deploy/deploy-button`           | 🔀  | 模板作者功能，從服務層移入模板區                |
| 模板目錄        | marketplace（外連）                  | ✅   |                                 |


#### 特色服務


| 新位置            | 原始路徑                             | 狀態  | 改名說明        |
| -------------- | -------------------------------- | --- | ----------- |
| Zeabur AI Hub  | `ai-hub.mdx` + `ai-hub/`*        | ✅   |             |
| n8n 整合         | `ai-hub/n8n-integration`         | ✅   |             |
| SillyTavern 整合 | `ai-hub/sillytavern-integration` | ✅   |             |
| Zeabur Email   | `email/*`（6 篇）                   | ✅   |             |
| MCP 整合         | `mcp.mdx`（目前隱藏）                  | 🔀  | 加入側欄，歸入特色服務 |
| InsForge       | `integrations/insforge`          | 🔀  | 從「整合」移入特色服務 |


---

### III. 基礎設施

#### 資料管理


| 新位置   | 原始路徑                              | 狀態  | 改名說明                   |
| ----- | --------------------------------- | --- | ---------------------- |
| 儲存空間  | `data-management/volumes`         | 📛  | 「持久儲存空間（硬碟）」→「儲存空間」，精簡 |
| 設定檔編輯 | `data-management/config-edit`     | 📛  | 「編輯設定檔」→「設定檔編輯」，名詞在前   |
| 檔案管理  | `data-management/file-management` | ✅   |                        |
| 備份    | `data-management/backup`          | ✅   |                        |
| 還原    | `data-management/restore`         | ✅   |                        |


#### 網路


| 新位置  | 原始路徑                           | 狀態  | 改名說明 |
| ---- | ------------------------------ | --- | ---- |
| 公網存取 | `networking/public`            | ✅   |      |
| 內網存取 | `networking/private`           | ✅   |      |
| 高可用性 | `networking/high-availability` | ✅   |      |


---

### IV. 開發者工具


| 新位置                        | 原始路徑                                   | 狀態              | 改名說明                          |
| -------------------------- | -------------------------------------- | --------------- | ----------------------------- |
| API 金鑰                     | `developer/use-api-key`                | 📛              | 「建立和使用 API 金鑰」→「API 金鑰」，精簡    |
| 開放 API                     | `developer/public-api`                 | ✅               |                               |
| WebSocket 指南               | `developer/websocket-guide`            | ✅               |                               |
| 構建原理                       | `advanced/builds`                      | 🔀              | 從「進階」移入，「進階」區塊消滅              |
| CLI 部署                     | `deploy/deploy-in-cli`                 | 🔀              | 從 deploy/ 移入開發者工具             |
| Chrome 插件                  | `deploy/deploy-with-chrome-extension`  | 🔀              | 從 deploy/ 移入，含「從 Gemini 部署」子頁 |
| Raycast 插件                 | `deploy/deploy-with-raycast-extension` | 🔀              | 從 deploy/ 移入                  |
| VS Code 插件                 | `deploy/deploy-with-vscode-extension`  | 🔀              | 從 deploy/ 移入                  |
| 服務生命週期（Scaling、Rollbacks…） | 無                                      | 📋 內部提案有列，目前無文檔 |                               |
| 監控與日誌                      | 無                                      | 📋 內部提案有列，目前無文檔 |                               |


---

### V. 語言與框架指南（AI-first）


| 新位置     | 原始路徑            | 狀態  |
| ------- | --------------- | --- |
| Node.js | `guides/nodejs` | ✅   |
| Bun     | `guides/bun`    | ✅   |
| Java    | `guides/java`   | ✅   |
| PHP     | `guides/php`    | ✅   |
| Python  | `guides/python` | ✅   |
| Go      | `guides/go`     | ✅   |
| Deno    | `guides/deno`   | ✅   |
| Rust    | `guides/rust`   | ✅   |
| Swift   | `guides/swift`  | ✅   |
| Dart    | `guides/dart`   | ✅   |
| 靜態網頁    | `guides/static` | ✅   |
| .NET    | `guides/dotnet` | ✅   |


---

### VI. 帳務與法律


| 新位置    | 原始路徑                   | 狀態  | 改名說明             |
| ------ | ---------------------- | --- | ---------------- |
| 定價     | `billing/pricing`      | 📛  | 「價格」→「定價」，對齊業界用語 |
| 方案     | `billing/plans`        | ✅   |                  |
| 訂閱     | `billing/subscription` | ✅   |                  |
| 贊助     | `billing/sponsor`      | ✅   |                  |
| 兌換預付卡  | `billing/redeem`       | ✅   |                  |
| 濫用回報指引 | `legal/abuse-report`   | ✅   |                  |
| 公平使用指南 | `legal/fair-use`       | ✅   |                  |
| 隱私權政策  | `legal/privacy`        | ✅   |                  |
| 服務條款   | `legal/terms`          | ✅   |                  |


---

### VII. 社群


| 新位置  | 原始路徑                     | 狀態  | 改名說明              |
| ---- | ------------------------ | --- | ----------------- |
| 論壇   | `community/forum`        | ✅   |                   |
| 推薦計畫 | `community/referral`     | ✅   |                   |
| 貢獻獎勵 | `community/contribution` | ✅   |                   |
| 帳號驗證 | `community/verify`       | 📛  | 「驗證」→「帳號驗證」，避免歧義  |
| 尋求幫助 | `community/help`         | ✅   | 保留原位，同時在 I. 入門設入口 |


---

## 被拆散的原有區塊


| 原區塊                 | 去向                                |
| ------------------- | --------------------------------- |
| `deploy/`           | 拆入 II. 專案層 + 服務層 + 模板 + IV. 開發者工具 |
| `manage/`           | 拆入 II. 專案層                        |
| `tutorials/` 導入指南   | 拆入 I. 遷移與導入                       |
| `integrations/` 整合  | 拆入 II. 特色服務                       |
| `advanced/` 進階      | 拆入 IV. 開發者工具（區塊消滅）                |
| `dedicated-server/` | 提升為 II. 伺服器層                      |
| `community/help`    | 提升到 I. 常見問題入口（社群區保留）              |


