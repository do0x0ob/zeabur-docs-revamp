# 部署流程概述

> **CTA 建議位置：** 服務詳情「Deployments」區塊

一次 Zeabur 部署的生命週期：**觸發 → 建置 → 執行 → 網域生效**。

本文件是 reference，一問一標題，供 AI 索引和 In-app CTA 使用。操作細節請參考各篇專文。

---

## 什麼會觸發一次部署？

| 來源 | 觸發條件 |
|------|----------|
| **GitHub** | Push 到已連結的分支，自動觸發。可用[觸發路徑](https://zeabur.com/docs/zh-TW/deploy/watch-paths)限定哪些目錄變更才觸發 |
| **本機專案 / Cursor** | 上傳或從 IDE 部署時觸發一次 |
| **模板** | 從[模板市集](https://zeabur.com/templates)部署時觸發 |
| **Docker 映像檔** | 指定映像檔名稱後觸發 |
| **手動** | 在服務詳情或部署歷史中手動觸發重新部署 |

Monorepo 的情況：預設觸發路徑是 `*`（整個 repo 任何變更都觸發）。如果前後端在同一個 repo，可以把前端服務的觸發路徑設為 `/client`，後端設為 `/server`，這樣改前端不會重新部署後端。格式和 `.gitignore` 一樣，但這裡是「觸發」而不是「忽略」。

---

## 建置階段發生什麼事？

Zeabur 會自動偵測你的程式碼類型（Node.js、Python、Go 等）並選擇對應的建置方式。如果你用 Dockerfile，則按 Dockerfile 內容建置。

建置順序：Clone 原始碼 → 安裝依賴 → 執行 Build → 產生容器映像檔。

建置階段只有部分環境變數可用（Git 相關的特殊變數）。如果需要在建置時注入變數，使用 Dockerfile 的 `ARG`。

---

## 部署失敗去哪看日誌？

在服務的 **部署** 或 **Logs** 分頁：

- **建置日誌**：Docker build、npm install、pip install 等失敗會出現在這裡
- **執行日誌**：服務啟動後 crash 或 runtime error 看這裡

可以按部署版本和時間篩選。

---

## 如何回滾到上一版？

在服務的 **部署歷史** 裡，選一個之前成功的版本，點 **Rollback**。回滾後那個版本就是目前的線上版。

---

## 預設網域和自訂網域怎麼運作？

**預設網域：** 部署完成後 Zeabur 自動分配一個 `xxx.zeabur.app`，大約 30 秒內可以存取，HTTPS 自動設定。

**自訂網域：** 到服務的 **Networking** 頁面新增，然後在你的 DNS 設定裡指向 Zeabur 提供的紀錄。生效後 HTTPS 也會自動處理。

詳見 [公網存取](https://zeabur.com/docs/zh-TW/networking/public)。

---

## 環境變數在建置和執行階段有什麼差別？

- **執行階段：** 在 Variables 頁面設定的變數會注入到運行中的容器，改完後需要重啟或重新部署才生效
- **建置階段：** 只有 Git 相關特殊變數和 Dockerfile `ARG` 定義的變數在建置時可用
- **優先順序：** 目前服務定義的 > 其他服務暴露的 > 特殊變數

詳見 [環境變數設定](https://zeabur.com/docs/zh-TW/deploy/variables)。

---

## 如何只讓特定目錄的變更觸發部署？

在服務設定中找到 **監控路徑（Watch Paths）**，格式和 `.gitignore` 一樣，但代表的是「觸發」而不是「忽略」。

例如設為 `/client`，代表只有 `client` 目錄的變更會觸發這個服務的部署。

詳見 [觸發路徑](https://zeabur.com/docs/zh-TW/deploy/watch-paths)。

---

## 複製或匯出專案會重新部署嗎？

- **複製專案：** 會。複製完成後服務會在新專案中自動部署，但網域需要重新綁定
- **匯出專案：** 不會。匯出為 YAML 模板，需要在新專案中匯入後才部署。匯出不含服務內資料，資料要另外用備份/還原處理

---

## 相關文件

- [建立服務](https://zeabur.com/docs/zh-TW/deploy/create-service)
- [GitHub 整合](https://zeabur.com/docs/zh-TW/deploy/github)
- [環境變數設定](https://zeabur.com/docs/zh-TW/deploy/variables)
- [觸發路徑](https://zeabur.com/docs/zh-TW/deploy/watch-paths)
- [Dockerfile 部署](https://zeabur.com/docs/zh-TW/deploy/dockerfile)
- [從模板部署](https://zeabur.com/docs/zh-TW/template/deploy-template)

---

## 還有問題？

到 [Zeabur Forum](https://zeabur.com/forum) 討論，或加入 [Discord](https://zeabur.com/dc) 取得即時支援。
