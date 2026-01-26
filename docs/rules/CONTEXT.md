# 專案脈絡

## 背景

SmilePicker 是 Chrome 瀏覽器上最優雅、最高效的符號快速輸入側邊面板插件。目標是讓使用者能快速存取並複製各種特殊符號（箭頭、數學、標點、鍵盤、貨幣、裝飾符號等），透過 Chrome Side Panel API 提供不遮擋網頁的操作體驗。

## 技術棧

| 類別 | 選擇 |
|-----|------|
| 語言 | TypeScript 5.x |
| 框架 | React 18 |
| 樣式 | Tailwind CSS 3.x |
| 打包 | Vite + CRXJS |
| 狀態管理 | React Hooks + Context |
| 儲存 | chrome.storage API |
| Manifest | V3 |

## 架構總覽

Chrome Extension 架構：
- **Side Panel**：主要 UI 介面，符號瀏覽與搜尋
- **Service Worker**：背景服務，處理快捷鍵與初始化
- **Options Page**：設定頁面，主題與偏好設定
- **Storage**：chrome.storage.local（本地）+ chrome.storage.sync（同步）

---

# 知識庫

## 決策記錄

| 日期 | 決策 | 原因 |
|-----|------|------|
| 2026-01-26 | 採用 8 檔案架構 | 簡化文件管理 |
| 2026-01-26 | 使用 Side Panel API | 不遮擋網頁內容，提升使用體驗 |
| 2026-01-26 | 採用 Manifest V3 | Chrome Extension 新標準 |
| 2026-01-26 | 選擇 Vite + CRXJS | 開發效率高，支援熱重載 |

## 學到的教訓

[過程中踩過的坑、未來要注意的事]
