<div align="center">
  <h1><img src="https://api.iconify.design/lucide/smile.svg?color=%23ff6b6b" width="28" height="28" /> SmilePicker</h1>
  <p><strong>Chrome side panel symbol picker for power users</strong></p>
  <p>Quick access to symbols, arrows, punctuation, and special characters with keyboard shortcuts, smart search, and sync across devices.</p>
</div>

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License" />
  <img src="https://img.shields.io/badge/Chrome-Extension-blue.svg" alt="Chrome Extension" />
  <img src="https://img.shields.io/badge/Manifest-V3-orange.svg" alt="Manifest V3" />
</p>

<p align="center">
  <strong>English</strong> • <a href="README_zh-TW.md">繁體中文</a> • <a href="README_zh-CN.md">简体中文</a>
</p>

---

### <img src="https://api.iconify.design/lucide/triangle-alert.svg?color=%23ff6b6b" width="18" height="18" /> The Problem

Typing special symbols (→ ⌘ ± × ÷ ≠ ∞ ★ ♥) requires memorizing complex keyboard shortcuts or hunting through character maps. Context switching breaks your flow.

### <img src="https://api.iconify.design/lucide/sparkles.svg?color=%23ff6b6b" width="18" height="18" /> The Solution

SmilePicker lives in your Chrome side panel — one keystroke away:

- **Instant Access** — `Alt+S` opens the side panel without switching tabs
- **Smart Search** — Find symbols by name, keyword, or appearance
- **One-Click Copy** — Click to copy, paste anywhere
- **Sync Favorites** — Chrome account sync for favorites and settings
- **Recent History** — Quick access to your last 10 symbols
- **Dark Mode** — Light/dark/system themes

### <img src="https://api.iconify.design/lucide/package.svg?color=%23ff6b6b" width="18" height="18" /> Symbol Categories

- **Arrows**: → ← ↑ ↓ ⇒ ⇐ ⇑ ⇓
- **Math**: ± × ÷ ≠ ∞ √ ∑ ∏
- **Punctuation**: 「」『』【】《》
- **Keyboard**: ⌘ ⌥ ⇧ ⌃ ↵ ⌫
- **Currency**: ¥ € £ ₿ ₹ ₽
- **Decorative**: ★ ☆ ♥ ♦ ● ○ ■ □

### <img src="https://api.iconify.design/lucide/download.svg?color=%23ff6b6b" width="18" height="18" /> Installation

#### From Chrome Web Store (Coming Soon)
1. Visit Chrome Web Store
2. Click "Add to Chrome"
3. Pin the side panel

#### Developer Mode (Current)
1. Clone this repo:
   ```bash
   git clone https://github.com/Pauuulq87/SmilePicker.git
   cd SmilePicker
   ```

2. Install dependencies and build:
   ```bash
   npm install
   npm run build
   ```

3. Load in Chrome:
   - Open `chrome://extensions/`
   - Enable "Developer mode"
   - Click "Load unpacked"
   - Select the `dist/` folder

### <img src="https://api.iconify.design/lucide/rocket.svg?color=%23ff6b6b" width="18" height="18" /> Usage

**Open Side Panel**
- Press `Alt+S` (Windows/Linux) or customize in `chrome://extensions/shortcuts`
- Click the extension icon → "Open side panel"

**Copy Symbols**
1. Search or browse categories
2. Click a symbol to copy
3. Paste anywhere with `Ctrl+V`

**Favorite Symbols**
- Click the star icon to add to favorites
- Access favorites from the top section

**Keyboard Navigation**
- `Tab` / `Shift+Tab` to navigate
- `Enter` to copy selected symbol
- `Esc` to close search

### <img src="https://api.iconify.design/lucide/wrench.svg?color=%23ff6b6b" width="18" height="18" /> Development

```bash
# Install dependencies
npm install

# Dev mode (hot reload)
npm run dev

# Build for production
npm run build

# Type check
npm run type-check
```

**Tech Stack**
- TypeScript + React 18
- Tailwind CSS
- Vite + CRXJS
- Chrome Extension Manifest V3

---

<div align="center">
  <p><strong>MIT License</strong> - Made with care for writers, developers, and power users.</p>
  <p><em>Thanks to all GitHub developers who share their wisdom and experience — you made this possible.</em></p>
</div>
