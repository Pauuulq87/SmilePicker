# 技術架構

## 技術選型

| 類別 | 選擇 | 原因 |
|-----|------|------|
| 語言 | TypeScript 5.x | 型別安全，開發體驗佳 |
| 框架 | React 18 | 元件化開發，生態系成熟 |
| 樣式 | Tailwind CSS 3.x | 快速樣式開發，支援深色模式 |
| 打包 | Vite + CRXJS | HMR 支援，Chrome Extension 友善 |
| 儲存 | chrome.storage API | 本地 + 跨裝置同步 |

## 目錄結構

```
SmilePicker/
├── CLAUDE.md                    # 專案入口
├── README.md                    # 專案說明
├── PRD.md                       # 產品需求文件
├── docs/rules/                  # 管理文件
├── src/
│   ├── sidepanel/              # Side Panel 主介面
│   │   ├── index.html
│   │   ├── index.tsx
│   │   ├── App.tsx
│   │   └── components/
│   │       ├── SearchBar.tsx
│   │       ├── SymbolGrid.tsx
│   │       ├── CategorySection.tsx
│   │       ├── SymbolButton.tsx
│   │       └── CopyFeedback.tsx
│   │
│   ├── options/                # 設定頁面
│   │   ├── index.html
│   │   ├── index.tsx
│   │   └── Options.tsx
│   │
│   ├── background/             # Service Worker
│   │   └── service-worker.ts
│   │
│   ├── shared/
│   │   ├── hooks/
│   │   │   ├── useSymbols.ts
│   │   │   ├── useStorage.ts
│   │   │   └── useFavorites.ts
│   │   ├── utils/
│   │   │   ├── clipboard.ts
│   │   │   └── storage.ts
│   │   ├── types/
│   │   │   └── symbol.ts
│   │   └── data/
│   │       └── defaultSymbols.json
│   │
│   └── styles/
│       └── globals.css         # Tailwind 入口
│
├── public/
│   └── icons/
│       ├── icon-16.png
│       ├── icon-32.png
│       ├── icon-48.png
│       └── icon-128.png
│
├── user/                       # 使用者私人區域
├── output/                     # 輸出檔案
└── dist/                       # 打包輸出
```

## 模組說明

### Side Panel (主介面)
- 負責符號瀏覽、搜尋、複製功能
- 支援分類展開收合、最近使用顯示

### Service Worker (背景服務)
- 處理擴充功能安裝初始化
- 管理快捷鍵觸發 Side Panel 開啟

### Options Page (設定頁面)
- 主題切換設定
- 符號大小、最近使用數量等偏好

### Shared (共用模組)
- Hooks：狀態管理邏輯
- Utils：剪貼簿、儲存工具函式
- Types：TypeScript 型別定義
- Data：預設符號資料

## 資料結構

```typescript
interface SymbolItem {
  symbol: string;
  name: string;
  keywords?: string[];
}

interface SymbolCategory {
  id: string;
  name: string;
  icon: string;
  symbols: SymbolItem[];
}

interface AppSettings {
  showCopyFeedback: boolean;
  maxRecentSymbols: number;
  theme: 'light' | 'dark' | 'system';
  symbolSize: 'small' | 'medium' | 'large';
}
```

## API 設計

Chrome Extension API 使用：
- `chrome.sidePanel` - Side Panel 控制
- `chrome.storage.local` - 本地儲存（最近使用、設定）
- `chrome.storage.sync` - 同步儲存（收藏）
- `chrome.commands` - 快捷鍵註冊
- `navigator.clipboard` - 剪貼簿操作
