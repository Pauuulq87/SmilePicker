<div align="center">
  <h1><img src="https://api.iconify.design/lucide/smile.svg?color=%23ff6b6b" width="28" height="28" /> SmilePicker</h1>
  <p><strong>Chrome 側邊面板符號快速輸入工具</strong></p>
  <p>快捷鍵一觸即達，智慧搜尋、收藏同步、深色模式，讓符號、箭頭、標點快速輸入變得優雅。</p>
</div>

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License" />
  <img src="https://img.shields.io/badge/Chrome-Extension-blue.svg" alt="Chrome Extension" />
  <img src="https://img.shields.io/badge/Manifest-V3-orange.svg" alt="Manifest V3" />
</p>

<p align="center">
  <a href="README.md">English</a> • <strong>繁體中文</strong> • <a href="README_zh-CN.md">简体中文</a>
</p>

---

### <img src="https://api.iconify.design/lucide/triangle-alert.svg?color=%23ff6b6b" width="18" height="18" /> 痛點

輸入特殊符號（→ ⌘ ± × ÷ ≠ ∞ ★ ♥）需要記複雜的快捷鍵或在字元對應表裡翻找。切換流程中斷你的專注力。

### <img src="https://api.iconify.design/lucide/sparkles.svg?color=%23ff6b6b" width="18" height="18" /> 解決方案

SmilePicker 常駐在你的 Chrome 側邊面板 — 一個按鍵就到：

- **即時存取** — `Alt+S` 開啟側邊面板，不用切換分頁
- **智慧搜尋** — 用名稱、關鍵字或外觀找符號
- **一鍵複製** — 點擊複製，貼到任何地方
- **收藏同步** — Chrome 帳號同步收藏和設定
- **最近使用** — 快速存取最近 10 個符號
- **深色模式** — 淺色/深色/跟隨系統主題

### <img src="https://api.iconify.design/lucide/package.svg?color=%23ff6b6b" width="18" height="18" /> 符號分類

- **箭頭符號**：→ ← ↑ ↓ ⇒ ⇐ ⇑ ⇓
- **數學符號**：± × ÷ ≠ ∞ √ ∑ ∏
- **標點符號**：「」『』【】《》
- **鍵盤符號**：⌘ ⌥ ⇧ ⌃ ↵ ⌫
- **貨幣符號**：¥ € £ ₿ ₹ ₽
- **裝飾符號**：★ ☆ ♥ ♦ ● ○ ■ □

### <img src="https://api.iconify.design/lucide/download.svg?color=%23ff6b6b" width="18" height="18" /> 安裝

#### 從 Chrome Web Store（即將推出）
1. 前往 Chrome Web Store
2. 點擊「加到 Chrome」
3. 釘選側邊面板

#### 開發者模式（當前）
1. Clone 此 repo：
   ```bash
   git clone https://github.com/Pauuulq87/SmilePicker.git
   cd SmilePicker
   ```

2. 安裝依賴並建置：
   ```bash
   npm install
   npm run build
   ```

3. 載入到 Chrome：
   - 開啟 `chrome://extensions/`
   - 啟用「開發人員模式」
   - 點擊「載入未封裝項目」
   - 選擇 `dist/` 資料夾

### <img src="https://api.iconify.design/lucide/rocket.svg?color=%23ff6b6b" width="18" height="18" /> 使用方式

**開啟側邊面板**
- 按 `Alt+S`（Windows/Linux）或在 `chrome://extensions/shortcuts` 自訂
- 點擊擴充功能圖示 → 「開啟側邊面板」

**複製符號**
1. 搜尋或瀏覽分類
2. 點擊符號複製
3. 用 `Ctrl+V` 貼到任何地方

**收藏符號**
- 點擊星號圖示加入收藏
- 從頂部區塊存取收藏

**鍵盤導航**
- `Tab` / `Shift+Tab` 切換
- `Enter` 複製選中的符號
- `Esc` 關閉搜尋

### <img src="https://api.iconify.design/lucide/wrench.svg?color=%23ff6b6b" width="18" height="18" /> 開發

```bash
# 安裝依賴
npm install

# 開發模式（熱重載）
npm run dev

# 正式版建置
npm run build

# 類型檢查
npm run type-check
```

**技術棧**
- TypeScript + React 18
- Tailwind CSS
- Vite + CRXJS
- Chrome Extension Manifest V3

---

<div align="center">
  <p><strong>MIT License</strong> - 專為文字工作者、開發者和高效用戶打造。</p>
  <p><em>謝謝 GitHub 開發者把智慧與經驗分享出來，才有今天的我。</em></p>
</div>
