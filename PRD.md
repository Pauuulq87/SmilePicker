# SmilePicker 產品需求文件 (PRD)

> **版本**: 1.0
> **建立日期**: 2026-01-22
> **目標**: 打造 Chrome Web Store 上最優雅的符號快速輸入側邊面板插件

---

## 目錄

1. [產品願景與目標](#1-產品願景與目標)
2. [規劃功能](#2-規劃功能)
3. [功能規劃（三階段）](#3-功能規劃三階段)
4. [技術架構設計](#4-技術架構設計)
5. [UI/UX 設計規範](#5-uiux-設計規範)
6. [Chrome Web Store 上架準備](#6-chrome-web-store-上架準備)
7. [開發時程建議](#7-開發時程建議)

---

## 1. 產品願景與目標

### 1.1 產品定位

**SmilePicker** 定位為 Chrome 瀏覽器上最優雅、最高效的符號快速輸入側邊面板插件。

**核心價值主張**：
- 🎯 **即時存取**: 快捷鍵一觸即達，側邊滑出不打斷工作流程
- 🎨 **精緻體驗**: 現代化 UI 設計，視覺愉悅
- ⚡ **極致效率**: 智慧搜尋、鍵盤導航、一鍵複製
- 🔄 **無縫同步**: Chrome 帳號同步收藏與設定

### 1.2 目標用戶

| 用戶類型 | 描述 | 核心需求 |
|---------|------|---------|
| **文字工作者** | 作家、編輯、記者 | 快速插入標點、引號、特殊符號 |
| **開發者** | 軟體工程師、技術作家 | 插入程式碼符號、箭頭、數學符號 |
| **設計師** | UI/UX 設計師 | 快速取用設計標注符號 |
| **學生/研究者** | 撰寫論文、報告 | 數學符號、希臘字母、單位符號 |
| **社群經理** | 管理社群媒體 | 表情符號、裝飾符號 |

### 1.3 成功指標

**Phase 1 完成後**:
- Chrome Web Store 評分 ≥ 4.5 星
- 週活躍用戶 (WAU) ≥ 1,000

**Phase 2 完成後**:
- Chrome Web Store 評分 ≥ 4.7 星
- WAU ≥ 5,000
- 付費轉換率 ≥ 5%（若採用 Freemium 模式）

**Phase 3 完成後**:
- 獲得 Chrome Web Store 精選推薦
- WAU ≥ 20,000
- 成為品類前 10 名

---

## 2. 規劃功能

### 2.1 核心功能清單

| 功能 | 優先級 | 說明 |
|-----|--------|-----|
| Side Panel 側邊面板 | P0 | Chrome Side Panel API 實現 |
| 快捷鍵開啟 | P0 | chrome.commands API（預設 Alt+S） |
| 一鍵複製符號 | P0 | Clipboard API 操作 |
| 最近使用追蹤 | P0 | 最多 10 個，chrome.storage.local 儲存 |
| 搜尋功能 | P0 | 支援名稱、符號、關鍵字 |
| 分類展開/收合 | P0 | 動畫過渡 |
| 符號收藏功能 | P1 | chrome.storage.sync 同步 |
| 設定頁面 | P1 | Options Page 完整偏好設定 |
| 主題切換 | P1 | 淺色/深色/跟隨系統 |
| 自訂符號 | P2 | 使用者自行新增符號分類 |

### 2.2 Chrome Extension 技術對照

| macOS 原功能 | Chrome Extension 對應 |
|-------------|----------------------|
| NSStatusItem 選單列圖示 | Extension Action Icon |
| Popover 面板 | Side Panel API |
| 全域快捷鍵 ⌘⇧S | chrome.commands（Alt+S） |
| NSPasteboard | Clipboard API |
| UserDefaults | chrome.storage.local |
| iCloud 同步 | chrome.storage.sync |
| KeyboardShortcuts 套件 | chrome.commands 可自訂 |
| SwiftUI | React + TypeScript |

### 2.3 專案結構規劃

```
smilepicker-extension/
├── package.json
├── vite.config.ts
├── tailwind.config.js
├── tsconfig.json
├── manifest.json                    # Chrome Extension Manifest V3
│
├── src/
│   ├── sidepanel/                   # Side Panel 主介面
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
│   ├── options/                     # 設定頁面
│   │   ├── index.html
│   │   ├── index.tsx
│   │   └── Options.tsx
│   │
│   ├── background/                  # Service Worker
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
│       └── globals.css              # Tailwind 入口
│
├── public/
│   └── icons/
│       ├── icon-16.png
│       ├── icon-32.png
│       ├── icon-48.png
│       └── icon-128.png
│
└── dist/                            # 打包輸出
```

---

## 3. 功能規劃（三階段）

### 3.1 Phase 1: MVP 核心版

> **目標**: 實現核心功能，達到 Chrome Web Store 上架標準
> **優先順序**: P0（必須完成）

#### 3.1.1 Manifest V3 配置

```json
{
  "manifest_version": 3,
  "name": "SmilePicker - 符號快選",
  "version": "1.0.0",
  "description": "Chrome 側邊面板符號快速輸入工具，一鍵複製特殊符號",

  "permissions": [
    "sidePanel",
    "storage",
    "clipboardWrite"
  ],

  "action": {
    "default_icon": {
      "16": "icons/icon-16.png",
      "32": "icons/icon-32.png",
      "48": "icons/icon-48.png",
      "128": "icons/icon-128.png"
    },
    "default_title": "開啟 SmilePicker"
  },

  "side_panel": {
    "default_path": "sidepanel/index.html"
  },

  "options_page": "options/index.html",

  "background": {
    "service_worker": "background/service-worker.js",
    "type": "module"
  },

  "commands": {
    "_execute_action": {
      "suggested_key": {
        "default": "Alt+S",
        "mac": "Alt+S"
      },
      "description": "開啟符號面板"
    }
  },

  "icons": {
    "16": "icons/icon-16.png",
    "32": "icons/icon-32.png",
    "48": "icons/icon-48.png",
    "128": "icons/icon-128.png"
  }
}
```

#### 3.1.2 Service Worker 設定

```typescript
// background/service-worker.ts

// 點擊圖示時開啟 Side Panel
chrome.action.onClicked.addListener(async (tab) => {
  if (tab.id) {
    await chrome.sidePanel.open({ tabId: tab.id });
  }
});

// 設定 Side Panel 行為
chrome.sidePanel.setPanelBehavior({ openPanelOnActionClick: true });

// 監聽安裝事件，初始化預設資料
chrome.runtime.onInstalled.addListener(async (details) => {
  if (details.reason === 'install') {
    // 初始化預設符號和設定
    await chrome.storage.local.set({
      recentSymbols: [],
      settings: {
        showCopyFeedback: true,
        maxRecentSymbols: 10,
        theme: 'system'
      }
    });
  }
});
```

#### 3.1.3 主要 React 元件

**App.tsx - 主應用程式**
```tsx
import { useState, useEffect } from 'react';
import { SearchBar } from './components/SearchBar';
import { SymbolGrid } from './components/SymbolGrid';
import { CategorySection } from './components/CategorySection';
import { useSymbols } from '../shared/hooks/useSymbols';
import { useStorage } from '../shared/hooks/useStorage';

export function App() {
  const [searchText, setSearchText] = useState('');
  const { categories, recentSymbols, addToRecent } = useSymbols();
  const { settings } = useStorage();

  const filteredCategories = categories.map(cat => ({
    ...cat,
    symbols: cat.symbols.filter(s =>
      s.name.toLowerCase().includes(searchText.toLowerCase()) ||
      s.symbol.includes(searchText) ||
      s.keywords?.some(k => k.toLowerCase().includes(searchText.toLowerCase()))
    )
  })).filter(cat => cat.symbols.length > 0);

  const handleCopy = async (symbol: string) => {
    await navigator.clipboard.writeText(symbol);
    await addToRecent(symbol);
  };

  return (
    <div className="h-screen flex flex-col bg-white dark:bg-gray-900">
      {/* 搜尋列 */}
      <div className="p-3 border-b border-gray-200 dark:border-gray-700">
        <SearchBar
          value={searchText}
          onChange={setSearchText}
          placeholder="搜尋符號..."
        />
      </div>

      {/* 符號列表 */}
      <div className="flex-1 overflow-y-auto p-3 space-y-4">
        {/* 最近使用 */}
        {recentSymbols.length > 0 && !searchText && (
          <CategorySection
            title="最近使用"
            icon="🕐"
            symbols={recentSymbols}
            onCopy={handleCopy}
            defaultExpanded
          />
        )}

        {/* 分類符號 */}
        {filteredCategories.map(category => (
          <CategorySection
            key={category.id}
            title={category.name}
            icon={category.icon}
            symbols={category.symbols}
            onCopy={handleCopy}
          />
        ))}
      </div>
    </div>
  );
}
```

**SymbolButton.tsx - 符號按鈕元件**
```tsx
import { useState } from 'react';
import { clsx } from 'clsx';

interface SymbolButtonProps {
  symbol: string;
  name: string;
  onCopy: (symbol: string) => void;
}

export function SymbolButton({ symbol, name, onCopy }: SymbolButtonProps) {
  const [copied, setCopied] = useState(false);
  const [isHovered, setIsHovered] = useState(false);

  const handleClick = async () => {
    await onCopy(symbol);
    setCopied(true);
    setTimeout(() => setCopied(false), 1000);
  };

  return (
    <button
      onClick={handleClick}
      onMouseEnter={() => setIsHovered(true)}
      onMouseLeave={() => setIsHovered(false)}
      title={name}
      className={clsx(
        'w-10 h-10 rounded-lg text-xl',
        'flex items-center justify-center',
        'transition-all duration-150',
        'border border-transparent',
        isHovered && 'scale-105 shadow-md bg-blue-50 dark:bg-blue-900/30 border-blue-200 dark:border-blue-700',
        copied && 'bg-green-100 dark:bg-green-900/30 border-green-300',
        !isHovered && !copied && 'bg-gray-50 dark:bg-gray-800 hover:bg-gray-100 dark:hover:bg-gray-700'
      )}
    >
      {copied ? '✓' : symbol}
    </button>
  );
}
```

#### 3.1.4 資料結構定義

```typescript
// shared/types/symbol.ts

export interface SymbolItem {
  symbol: string;
  name: string;
  keywords?: string[];
}

export interface SymbolCategory {
  id: string;
  name: string;
  icon: string;
  symbols: SymbolItem[];
}

export interface AppSettings {
  showCopyFeedback: boolean;
  maxRecentSymbols: number;
  theme: 'light' | 'dark' | 'system';
  symbolSize: 'small' | 'medium' | 'large';
}

export interface StorageData {
  recentSymbols: string[];
  favorites: string[];
  settings: AppSettings;
  customSymbols?: SymbolCategory[];
}
```

#### 3.1.5 預設符號資料

```json
// shared/data/defaultSymbols.json
{
  "categories": [
    {
      "id": "arrows",
      "name": "箭頭符號",
      "icon": "→",
      "symbols": [
        { "symbol": "→", "name": "右箭頭", "keywords": ["arrow", "right"] },
        { "symbol": "←", "name": "左箭頭", "keywords": ["arrow", "left"] },
        { "symbol": "↑", "name": "上箭頭", "keywords": ["arrow", "up"] },
        { "symbol": "↓", "name": "下箭頭", "keywords": ["arrow", "down"] },
        { "symbol": "↔", "name": "雙向箭頭", "keywords": ["arrow", "both"] },
        { "symbol": "⇒", "name": "雙線右箭頭", "keywords": ["arrow", "implies"] },
        { "symbol": "⇐", "name": "雙線左箭頭", "keywords": ["arrow"] },
        { "symbol": "⇔", "name": "雙向雙線箭頭", "keywords": ["arrow", "equivalent"] }
      ]
    },
    {
      "id": "math",
      "name": "數學符號",
      "icon": "∑",
      "symbols": [
        { "symbol": "±", "name": "正負號", "keywords": ["plus", "minus"] },
        { "symbol": "×", "name": "乘號", "keywords": ["multiply", "times"] },
        { "symbol": "÷", "name": "除號", "keywords": ["divide"] },
        { "symbol": "≠", "name": "不等於", "keywords": ["not equal"] },
        { "symbol": "≈", "name": "約等於", "keywords": ["approximately"] },
        { "symbol": "≤", "name": "小於等於", "keywords": ["less equal"] },
        { "symbol": "≥", "name": "大於等於", "keywords": ["greater equal"] },
        { "symbol": "∞", "name": "無限大", "keywords": ["infinity"] }
      ]
    },
    {
      "id": "punctuation",
      "name": "標點符號",
      "icon": "「」",
      "symbols": [
        { "symbol": "「", "name": "左引號", "keywords": ["quote"] },
        { "symbol": "」", "name": "右引號", "keywords": ["quote"] },
        { "symbol": "『", "name": "雙左引號", "keywords": ["quote"] },
        { "symbol": "』", "name": "雙右引號", "keywords": ["quote"] },
        { "symbol": "【", "name": "左方括號", "keywords": ["bracket"] },
        { "symbol": "】", "name": "右方括號", "keywords": ["bracket"] },
        { "symbol": "…", "name": "省略號", "keywords": ["ellipsis"] },
        { "symbol": "—", "name": "破折號", "keywords": ["dash"] }
      ]
    },
    {
      "id": "keyboard",
      "name": "鍵盤符號",
      "icon": "⌘",
      "symbols": [
        { "symbol": "⌘", "name": "Command", "keywords": ["cmd", "command"] },
        { "symbol": "⌥", "name": "Option", "keywords": ["alt", "option"] },
        { "symbol": "⇧", "name": "Shift", "keywords": ["shift"] },
        { "symbol": "⌃", "name": "Control", "keywords": ["ctrl", "control"] },
        { "symbol": "⎋", "name": "Escape", "keywords": ["esc", "escape"] },
        { "symbol": "⏎", "name": "Return", "keywords": ["enter", "return"] },
        { "symbol": "⌫", "name": "Delete", "keywords": ["backspace", "delete"] },
        { "symbol": "⇥", "name": "Tab", "keywords": ["tab"] }
      ]
    },
    {
      "id": "currency",
      "name": "貨幣符號",
      "icon": "💰",
      "symbols": [
        { "symbol": "¥", "name": "日圓/人民幣", "keywords": ["yen", "yuan"] },
        { "symbol": "€", "name": "歐元", "keywords": ["euro"] },
        { "symbol": "£", "name": "英鎊", "keywords": ["pound"] },
        { "symbol": "₩", "name": "韓圓", "keywords": ["won"] },
        { "symbol": "₿", "name": "比特幣", "keywords": ["bitcoin"] },
        { "symbol": "¢", "name": "美分", "keywords": ["cent"] }
      ]
    },
    {
      "id": "decorative",
      "name": "裝飾符號",
      "icon": "★",
      "symbols": [
        { "symbol": "★", "name": "實心星", "keywords": ["star"] },
        { "symbol": "☆", "name": "空心星", "keywords": ["star"] },
        { "symbol": "♥", "name": "愛心", "keywords": ["heart", "love"] },
        { "symbol": "♦", "name": "方塊", "keywords": ["diamond"] },
        { "symbol": "♣", "name": "梅花", "keywords": ["club"] },
        { "symbol": "♠", "name": "黑桃", "keywords": ["spade"] },
        { "symbol": "●", "name": "實心圓", "keywords": ["circle", "bullet"] },
        { "symbol": "○", "name": "空心圓", "keywords": ["circle"] }
      ]
    }
  ]
}
```

---

### 3.2 Phase 2: 完整版

> **目標**: 功能完整、跨裝置同步、專業使用者滿意
> **優先順序**: P1（重要功能）

#### 3.2.1 收藏功能

**useFavorites.ts**
```typescript
import { useState, useEffect } from 'react';

export function useFavorites() {
  const [favorites, setFavorites] = useState<string[]>([]);

  useEffect(() => {
    // 從 chrome.storage.sync 載入（跨裝置同步）
    chrome.storage.sync.get(['favorites'], (result) => {
      setFavorites(result.favorites || []);
    });

    // 監聽變更
    const listener = (changes: { [key: string]: chrome.storage.StorageChange }) => {
      if (changes.favorites) {
        setFavorites(changes.favorites.newValue || []);
      }
    };
    chrome.storage.onChanged.addListener(listener);
    return () => chrome.storage.onChanged.removeListener(listener);
  }, []);

  const toggleFavorite = async (symbol: string) => {
    const newFavorites = favorites.includes(symbol)
      ? favorites.filter(s => s !== symbol)
      : [...favorites, symbol];

    await chrome.storage.sync.set({ favorites: newFavorites });
    setFavorites(newFavorites);
  };

  const isFavorite = (symbol: string) => favorites.includes(symbol);

  return { favorites, toggleFavorite, isFavorite };
}
```

#### 3.2.2 進階搜尋

```typescript
// shared/utils/search.ts

// 拼音首字母搜尋支援
const pinyinMap: Record<string, string> = {
  '箭頭': 'jt',
  '符號': 'fh',
  '數學': 'sx',
  '標點': 'bd',
  // ... 更多映射
};

export function searchSymbols(
  categories: SymbolCategory[],
  query: string
): SymbolCategory[] {
  if (!query.trim()) return categories;

  const lowerQuery = query.toLowerCase();

  return categories
    .map(cat => ({
      ...cat,
      symbols: cat.symbols.filter(s => {
        // 符號本身匹配
        if (s.symbol.includes(query)) return true;

        // 名稱匹配
        if (s.name.toLowerCase().includes(lowerQuery)) return true;

        // 關鍵字匹配
        if (s.keywords?.some(k => k.toLowerCase().includes(lowerQuery))) return true;

        // 拼音匹配
        const pinyin = pinyinMap[s.name];
        if (pinyin && pinyin.includes(lowerQuery)) return true;

        return false;
      })
    }))
    .filter(cat => cat.symbols.length > 0);
}
```

#### 3.2.3 主題系統

```typescript
// shared/hooks/useTheme.ts

type Theme = 'light' | 'dark' | 'system';

export function useTheme() {
  const [theme, setTheme] = useState<Theme>('system');

  useEffect(() => {
    chrome.storage.local.get(['settings'], (result) => {
      setTheme(result.settings?.theme || 'system');
    });
  }, []);

  useEffect(() => {
    const root = document.documentElement;

    if (theme === 'system') {
      const isDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
      root.classList.toggle('dark', isDark);
    } else {
      root.classList.toggle('dark', theme === 'dark');
    }
  }, [theme]);

  const updateTheme = async (newTheme: Theme) => {
    const result = await chrome.storage.local.get(['settings']);
    await chrome.storage.local.set({
      settings: { ...result.settings, theme: newTheme }
    });
    setTheme(newTheme);
  };

  return { theme, setTheme: updateTheme };
}
```

#### 3.2.4 設定頁面

```tsx
// options/Options.tsx

import { useState, useEffect } from 'react';
import { useTheme } from '../shared/hooks/useTheme';

export function Options() {
  const { theme, setTheme } = useTheme();
  const [settings, setSettings] = useState({
    showCopyFeedback: true,
    maxRecentSymbols: 10,
    symbolSize: 'medium' as const
  });

  useEffect(() => {
    chrome.storage.local.get(['settings'], (result) => {
      if (result.settings) {
        setSettings(s => ({ ...s, ...result.settings }));
      }
    });
  }, []);

  const updateSetting = async <K extends keyof typeof settings>(
    key: K,
    value: typeof settings[K]
  ) => {
    const newSettings = { ...settings, [key]: value };
    setSettings(newSettings);
    await chrome.storage.local.set({ settings: newSettings });
  };

  return (
    <div className="max-w-xl mx-auto p-6 space-y-6">
      <h1 className="text-2xl font-bold">SmilePicker 設定</h1>

      {/* 外觀設定 */}
      <section className="space-y-4">
        <h2 className="text-lg font-semibold">外觀</h2>

        <div className="flex items-center justify-between">
          <label>主題</label>
          <select
            value={theme}
            onChange={(e) => setTheme(e.target.value as any)}
            className="px-3 py-2 border rounded-lg"
          >
            <option value="system">跟隨系統</option>
            <option value="light">淺色</option>
            <option value="dark">深色</option>
          </select>
        </div>

        <div className="flex items-center justify-between">
          <label>符號大小</label>
          <select
            value={settings.symbolSize}
            onChange={(e) => updateSetting('symbolSize', e.target.value as any)}
            className="px-3 py-2 border rounded-lg"
          >
            <option value="small">小</option>
            <option value="medium">中</option>
            <option value="large">大</option>
          </select>
        </div>
      </section>

      {/* 行為設定 */}
      <section className="space-y-4">
        <h2 className="text-lg font-semibold">行為</h2>

        <div className="flex items-center justify-between">
          <label>顯示複製提示</label>
          <input
            type="checkbox"
            checked={settings.showCopyFeedback}
            onChange={(e) => updateSetting('showCopyFeedback', e.target.checked)}
            className="w-5 h-5"
          />
        </div>

        <div className="flex items-center justify-between">
          <label>最近使用數量</label>
          <input
            type="number"
            min={3}
            max={20}
            value={settings.maxRecentSymbols}
            onChange={(e) => updateSetting('maxRecentSymbols', parseInt(e.target.value))}
            className="w-20 px-3 py-2 border rounded-lg"
          />
        </div>
      </section>

      {/* 快捷鍵說明 */}
      <section className="space-y-4">
        <h2 className="text-lg font-semibold">快捷鍵</h2>
        <p className="text-gray-600">
          預設快捷鍵：<kbd className="px-2 py-1 bg-gray-100 rounded">Alt + S</kbd>
        </p>
        <p className="text-sm text-gray-500">
          可在 Chrome 設定 → 擴充功能 → 鍵盤快捷鍵 中自訂
        </p>
      </section>

      {/* 關於 */}
      <section className="space-y-2 pt-4 border-t">
        <h2 className="text-lg font-semibold">關於</h2>
        <p className="text-gray-600">SmilePicker v1.0.0</p>
        <p className="text-sm text-gray-500">
          快速存取數千個特殊符號的 Chrome 側邊面板插件
        </p>
      </section>
    </div>
  );
}
```

#### 3.2.5 Onboarding 流程

首次安裝時顯示歡迎頁面：

```typescript
// background/service-worker.ts 新增

chrome.runtime.onInstalled.addListener(async (details) => {
  if (details.reason === 'install') {
    // 開啟歡迎頁面
    await chrome.tabs.create({
      url: chrome.runtime.getURL('onboarding/index.html')
    });
  }
});
```

---

### 3.3 Phase 3: 精選版

> **目標**: 超越預期、獲得 Chrome Web Store 精選推薦
> **優先順序**: P2（差異化功能）

#### 3.3.1 Glassmorphism UI

```css
/* 毛玻璃效果 */
.glass-panel {
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
}

.dark .glass-panel {
  background: rgba(30, 30, 30, 0.8);
  border: 1px solid rgba(255, 255, 255, 0.1);
}
```

#### 3.3.2 鍵盤導航

```tsx
// 完整鍵盤導航支援
function useKeyboardNavigation(symbols: string[], onSelect: (s: string) => void) {
  const [focusIndex, setFocusIndex] = useState(-1);
  const columns = 7;

  useEffect(() => {
    const handleKeyDown = (e: KeyboardEvent) => {
      switch (e.key) {
        case 'ArrowRight':
          setFocusIndex(i => Math.min(i + 1, symbols.length - 1));
          break;
        case 'ArrowLeft':
          setFocusIndex(i => Math.max(i - 1, 0));
          break;
        case 'ArrowDown':
          setFocusIndex(i => Math.min(i + columns, symbols.length - 1));
          break;
        case 'ArrowUp':
          setFocusIndex(i => Math.max(i - columns, 0));
          break;
        case 'Enter':
        case ' ':
          if (focusIndex >= 0) {
            onSelect(symbols[focusIndex]);
          }
          break;
        case 'Escape':
          setFocusIndex(-1);
          break;
      }
    };

    window.addEventListener('keydown', handleKeyDown);
    return () => window.removeEventListener('keydown', handleKeyDown);
  }, [symbols, focusIndex, onSelect]);

  return { focusIndex, setFocusIndex };
}
```

#### 3.3.3 右鍵選單整合

```typescript
// 在網頁中選取文字時，右鍵選單加入「插入符號」選項
chrome.contextMenus.create({
  id: 'insert-symbol',
  title: '插入符號',
  contexts: ['editable']
});

chrome.contextMenus.onClicked.addListener(async (info, tab) => {
  if (info.menuItemId === 'insert-symbol' && tab?.id) {
    await chrome.sidePanel.open({ tabId: tab.id });
  }
});
```

#### 3.3.4 Content Script 直接插入

```typescript
// content/inject-symbol.ts
// 直接將符號插入到當前游標位置

chrome.runtime.onMessage.addListener((message, sender, sendResponse) => {
  if (message.type === 'INSERT_SYMBOL') {
    const activeElement = document.activeElement as HTMLInputElement | HTMLTextAreaElement;

    if (activeElement && (activeElement.tagName === 'INPUT' || activeElement.tagName === 'TEXTAREA')) {
      const start = activeElement.selectionStart || 0;
      const end = activeElement.selectionEnd || 0;
      const value = activeElement.value;

      activeElement.value = value.substring(0, start) + message.symbol + value.substring(end);
      activeElement.selectionStart = activeElement.selectionEnd = start + message.symbol.length;

      // 觸發 input 事件
      activeElement.dispatchEvent(new Event('input', { bubbles: true }));
    }

    sendResponse({ success: true });
  }
});
```

---

## 4. 技術架構設計

### 4.1 技術堆疊

| 層級 | 技術選擇 |
|-----|---------|
| 語言 | TypeScript 5.x |
| 框架 | React 18 |
| 樣式 | Tailwind CSS 3.x |
| 打包 | Vite + CRXJS |
| 狀態管理 | React Hooks + Context |
| 儲存 | chrome.storage API |
| Manifest | V3 |

### 4.2 專案初始化指令

```bash
# 使用 Vite Chrome Extension 模板
npm create vite@latest smilepicker-extension -- --template react-ts

cd smilepicker-extension

# 安裝依賴
npm install @crxjs/vite-plugin tailwindcss postcss autoprefixer clsx

# 初始化 Tailwind
npx tailwindcss init -p
```

### 4.3 Vite 配置

```typescript
// vite.config.ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import { crx } from '@crxjs/vite-plugin';
import manifest from './manifest.json';

export default defineConfig({
  plugins: [
    react(),
    crx({ manifest })
  ],
  build: {
    rollupOptions: {
      input: {
        sidepanel: 'src/sidepanel/index.html',
        options: 'src/options/index.html',
        onboarding: 'src/onboarding/index.html'
      }
    }
  }
});
```

### 4.4 資料流架構

```
┌─────────────────────────────────────────────────────────────┐
│                      Side Panel UI                          │
│                    (React Components)                       │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│                     React Hooks                             │
│  useSymbols / useFavorites / useStorage / useTheme          │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│                   Chrome Storage API                        │
├──────────────────────┬──────────────────────────────────────┤
│  chrome.storage.local │  chrome.storage.sync                │
│  - 最近使用            │  - 收藏符號                         │
│  - 本地設定            │  - 同步設定                         │
│  - 快取資料            │                                    │
└──────────────────────┴──────────────────────────────────────┘
```

---

## 5. UI/UX 設計規範

### 5.1 Side Panel 尺寸

| 屬性 | 數值 |
|-----|------|
| 預設寬度 | 320px（Chrome 控制） |
| 最小寬度 | 240px |
| 最大寬度 | 500px |
| 高度 | 100vh（隨視窗高度） |

### 5.2 設計系統

#### 色彩系統（Tailwind）

```javascript
// tailwind.config.js
module.exports = {
  darkMode: 'class',
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8'
        }
      }
    }
  }
}
```

#### 字型系統

| 用途 | Tailwind 類別 |
|-----|--------------|
| 標題 | `text-base font-semibold` |
| 分類標題 | `text-sm font-medium` |
| 符號 | `text-xl` |
| 標籤 | `text-xs` |

#### 間距系統

| 名稱 | Tailwind | 數值 |
|-----|----------|------|
| xs | `p-1` | 4px |
| sm | `p-2` | 8px |
| md | `p-3` | 12px |
| lg | `p-4` | 16px |
| xl | `p-6` | 24px |

### 5.3 動畫規範

```css
/* Tailwind 動畫擴展 */
@layer utilities {
  .animate-scale-in {
    animation: scale-in 0.15s ease-out;
  }

  .animate-fade-in {
    animation: fade-in 0.2s ease-out;
  }
}

@keyframes scale-in {
  from {
    transform: scale(0.95);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

@keyframes fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}
```

### 5.4 響應式設計

Side Panel 寬度由使用者拖曳調整，需確保：
- 最小 240px 時仍可正常使用
- 符號網格自動調整欄數
- 搜尋框寬度 100%

```tsx
// 自適應網格
<div className="grid grid-cols-[repeat(auto-fill,minmax(40px,1fr))] gap-2">
  {symbols.map(s => <SymbolButton key={s.symbol} {...s} />)}
</div>
```

---

## 6. Chrome Web Store 上架準備

### 6.1 必要資產

#### 圖示尺寸

| 尺寸 | 用途 |
|-----|------|
| 16x16 | 工具列（小） |
| 32x32 | 工具列（標準） |
| 48x48 | 擴充功能管理頁面 |
| 128x128 | Chrome Web Store |

#### 商店截圖

| 尺寸 | 數量 | 內容建議 |
|-----|------|---------|
| 1280x800 或 640x400 | 5 張 | 主功能展示 |

**截圖清單**：
1. Side Panel 全貌（含最近使用、分類）
2. 搜尋功能展示
3. 收藏功能
4. 設定頁面
5. 深色模式

#### 宣傳圖片

| 尺寸 | 用途 |
|-----|------|
| 440x280 | 小型宣傳磚 |
| 1400x560 | 大型宣傳橫幅（可選） |

### 6.2 商店文案

#### 擴充功能名稱
```
SmilePicker - 符號快選
```

#### 簡短描述（132 字元內）
```
Chrome 側邊面板符號快速輸入工具。快捷鍵一觸即達，智慧搜尋、收藏同步、深色模式。
```

#### 詳細描述
```
SmilePicker 是 Chrome 上最優雅的符號快速輸入側邊面板插件。

■ 即時存取
• 側邊面板設計，不遮擋網頁內容
• 快捷鍵 Alt+S 一觸即達（可自訂）
• 一鍵複製，高效工作

■ 智慧搜尋
• 輸入名稱、關鍵字或符號本身
• 支援中英文搜尋
• 搜尋結果即時顯示

■ 個人化
• 符號收藏功能
• Chrome 帳號同步
• 淺色/深色主題切換

■ 豐富符號庫
• 箭頭符號：→ ← ↑ ↓ ⇒
• 數學符號：± × ÷ ≠ ∞
• 標點符號：「」『』【】
• 鍵盤符號：⌘ ⌥ ⇧ ⌃
• 貨幣符號：¥ € £ ₿
• 裝飾符號：★ ♥ ● ○

立即安裝 SmilePicker，讓符號輸入成為愉悅的體驗！
```

### 6.3 權限說明

在上架審核時需說明各權限用途：

| 權限 | 用途說明 |
|-----|---------|
| `sidePanel` | 顯示側邊面板介面 |
| `storage` | 儲存使用者設定、收藏和最近使用記錄 |
| `clipboardWrite` | 將符號複製到剪貼簿 |

### 6.4 隱私政策要點

```
SmilePicker 隱私政策

資料收集：
- 本擴充功能不收集任何個人識別資訊
- 使用記錄僅儲存於本機（chrome.storage.local）
- 收藏符號透過 Chrome 帳號同步（chrome.storage.sync），由 Google 管理
- 無任何第三方分析或追蹤工具

資料使用：
- 所有資料僅用於提供擴充功能服務
- 不會與任何第三方分享資料
```

---

## 7. 開發時程建議

### 7.1 里程碑概覽

```
Phase 1: MVP 核心版
├── 專案初始化（Vite + React + Tailwind）
├── Manifest V3 配置
├── Side Panel 基礎 UI
├── 符號資料與搜尋
├── 複製功能
├── 最近使用追蹤
└── 基礎樣式（淺色/深色）

Phase 2: 完整版
├── 收藏功能 + 同步
├── 設定頁面
├── 進階搜尋
├── Onboarding 流程
└── 完整主題系統

Phase 3: 精選版
├── Glassmorphism UI
├── 鍵盤導航
├── 右鍵選單整合
├── Content Script 直接插入
└── 效能優化
```

### 7.2 開發指令

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
```

---

## 附錄：實用程式碼片段

### A. Clipboard API 封裝

```typescript
// shared/utils/clipboard.ts

export async function copyToClipboard(text: string): Promise<boolean> {
  try {
    await navigator.clipboard.writeText(text);
    return true;
  } catch (err) {
    // Fallback for older browsers
    const textarea = document.createElement('textarea');
    textarea.value = text;
    textarea.style.position = 'fixed';
    textarea.style.opacity = '0';
    document.body.appendChild(textarea);
    textarea.select();

    try {
      document.execCommand('copy');
      return true;
    } catch {
      return false;
    } finally {
      document.body.removeChild(textarea);
    }
  }
}
```

### B. Storage Hook

```typescript
// shared/hooks/useStorage.ts

import { useState, useEffect } from 'react';

export function useStorage<T>(key: string, defaultValue: T) {
  const [value, setValue] = useState<T>(defaultValue);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    chrome.storage.local.get([key], (result) => {
      if (result[key] !== undefined) {
        setValue(result[key]);
      }
      setLoading(false);
    });

    const listener = (changes: { [key: string]: chrome.storage.StorageChange }) => {
      if (changes[key]) {
        setValue(changes[key].newValue);
      }
    };

    chrome.storage.onChanged.addListener(listener);
    return () => chrome.storage.onChanged.removeListener(listener);
  }, [key]);

  const setStorageValue = async (newValue: T) => {
    await chrome.storage.local.set({ [key]: newValue });
    setValue(newValue);
  };

  return { value, setValue: setStorageValue, loading };
}
```

### C. 符號 Unicode 資訊顯示

```typescript
// 取得符號的 Unicode 編碼
export function getUnicodeInfo(symbol: string): string {
  return [...symbol]
    .map(char => `U+${char.codePointAt(0)?.toString(16).toUpperCase().padStart(4, '0')}`)
    .join(' ');
}

// "→".getUnicodeInfo() → "U+2192"
```

---

## 結語

本 PRD 規劃了 SmilePicker 從 MVP 到 Chrome Web Store 精選推薦的完整發展路徑。透過三個階段的迭代開發，逐步提升產品品質與功能深度。

**核心原則**：
1. **使用者體驗優先** - 側邊面板不遮擋網頁，操作流暢
2. **漸進式開發** - 每個 Phase 都是可發布的穩定版本
3. **原生體驗** - 遵循 Chrome Extension 設計規範

**下一步行動**：
1. 確認 Phase 1 功能範圍與優先順序
2. 建立專案結構
3. 開始 Manifest V3 配置與基礎 UI 開發
