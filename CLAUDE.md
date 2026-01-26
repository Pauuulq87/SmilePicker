# SmilePicker

## 基本資訊

- 類型：Standard（Chrome Extension）
- 語言：TypeScript + React
- 狀態：開發中
- 建立日期：2026-01-26

---

## 文件索引

專案管理文件位於 `docs/rules/`：

- @docs/rules/CURRENT.md — 當前任務狀態（AI 維護）
- @docs/rules/CONTEXT.md — 專案背景與知識庫（AI 維護）
- @docs/rules/REQUIREMENTS.md — 需求與目的（用戶填寫）
- @docs/rules/ARCHITECTURE.md — 技術架構（AI 維護）
- @docs/rules/RULES.md — 開發規則（模板）
- @docs/rules/CHANGELOG.md — 變更日誌（AI 維護）

---

## 絕對禁止事項

1. **絕不** 在根目錄建立程式檔案 → 使用 `src/` 結構
2. **絕不** 直接將輸出檔案寫入根目錄 → 使用 `output/`
3. **絕不** 建立重複檔案（如 `*_v2.py`、`*_new.js`）→ 擴充現有檔案
4. **絕不** 硬編碼敏感資訊 → 使用環境變數
5. **絕不** 提交含有密碼、API Key 的檔案 → 安全檢查會擋下

---

## 使用者專屬區域

`user/` 目錄為私人區域：

- 未授權不得讀寫
- 不得納入版控
- 不得自動化處理

---

## 外部資源

- **Chrome Extension 文件**: https://developer.chrome.com/docs/extensions/
- **Manifest V3 文件**: https://developer.chrome.com/docs/extensions/mv3/intro/
- **Side Panel API**: https://developer.chrome.com/docs/extensions/reference/api/sidePanel
- **Vite + CRXJS**: https://crxjs.dev/vite-plugin

---

## 常用命令

```bash
# 開發模式（熱重載）
npm run dev

# 建置生產版本
npm run build

# 載入擴充功能
# 1. 開啟 chrome://extensions/
# 2. 啟用「開發人員模式」
# 3. 點擊「載入未封裝項目」
# 4. 選擇 dist/ 資料夾

# 型別檢查
npm run typecheck

# Lint 檢查
npm run lint
```
