# 快速入門

> **CTA 建議位置：** 空白畫面（專案、伺服器）

Zeabur 讓你幾分鐘內把服務部署上線，不需要碰 Docker、CI/CD 或任何 DevOps 設定。

還沒有帳號？[前往註冊](https://zeabur.com)，驗證完就可以開始了。

---

## 準備一台伺服器

Zeabur 目前以專用伺服器為主要運作方式。你需要至少有一台伺服器才能建立專案和部署服務。

有兩種方式：

1. **在 Zeabur 購買** — 到 [專用伺服器](https://zeabur.com/new) 頁面選方案，以優惠價格獲取伺服器資源。

  參考文件：[專用伺服器](https://zeabur.com/docs/zh-TW/dedicated-server)

2. **註冊自己的機器** — 如果你已經在 AWS、GCP、Hetzner 等伺服器供應商有機器，可以 [註冊到 Zeabur](https://zeabur.com/docs/zh-TW/dedicated-server/register) 來進行統一管理。

## 部署你的第一個服務

在專案裡點 **部署新服務**，你會看到幾種方式：

### 最快的方式：從模板部署

點 **模板**，挑一個有興趣的，點 **部署**，等待 Zeabur 幫你部署。

不確定選哪個？這幾個部署完打開就有東西看：

| 模板 | 適合場景 |
|------|----------|
| [WordPress](https://zeabur.com/zh-TW/templates/CV344X) | 架網站/部落格，打開就有東西看 |
| [Halo](https://zeabur.com/zh-TW/templates/Q6H2MA) | 中文部落格系統，開箱即用 |
| [Uptime Kuma](https://zeabur.com/zh-TW/templates/Q764RP) | 服務監控面板，部署完就有漂亮 dashboard |

詳見 [從模板部署](https://zeabur.com/docs/zh-TW/template/deploy-template)。

### 部署自己的程式碼：從 GitHub

1. **建立專案**：從專案處點 **建立專案**，選擇要部署專案的目標伺服器。一個專案可以放你的前端、後端、資料庫等所有相關 **服務**。
2. **從 GitHub 部署**：在專案頁面點 **建立服務** / **部署新服務**，在下拉選單選 **GitHub**，點 **設定 GitHub 儲存庫** 連結你的 GitHub 帳號；之後搜尋並選中想部署的 repo，Zeabur 會自動分析程式碼並選最適合的建置方式，直接點 **部署** 就好。


### 其他方式

Zeabur 同時支持多種部署方式：

- **本機專案** — 直接拖拉資料夾上傳
- **Docker 映像檔** — 從 Docker Hub 部署任何映像檔
- **Cursor** — 從 Cursor IDE 直接部署  

  …等等。

## 上線

部署完成後，可以透過 Zeabur 便捷的產生一個可訪問的 URL（像 `xxx.zeabur.app`）。設定完成後，點開就能看到你剛才架設的服務了。

想用自己的域名？到服務的 **網路** 頁面加上去，DNS 設好之後 HTTPS 會自動處理。

---

## 遇到問題？

畫面右側是 AI 對話窗口，它能讀取你的專案狀態和 Build log，直接告訴你哪裡出問題、並且自動幫你修復。

---

## 接下來

- [從模板部署](https://zeabur.com/docs/zh-TW/template/deploy-template) — 更多模板選擇和部署後設定
- [部署流程概述](https://zeabur.com/docs/zh-TW/deploy/deploy-flow) — 了解觸發、建置、回滾等完整流程
- [語言與框架指南](https://zeabur.com/docs/zh-TW/guides/nodejs) — 你的框架在 Zeabur 上怎麼跑
- [環境變數設定](https://zeabur.com/docs/zh-TW/deploy/variables) — 設定你的服務需要的變數

有問題可到 [Zeabur Forum](https://zeabur.com/forum) 聊，或加入 [Discord](https://zeabur.com/dc)。
