<div align="center">
  <h1><img src="https://api.iconify.design/lucide/smile.svg?color=%23ff6b6b" width="28" height="28" /> SmilePicker</h1>
  <p><strong>Chrome 侧边面板符号快速输入工具</strong></p>
  <p>快捷键一触即达，智能搜索、收藏同步、深色模式，让符号、箭头、标点快速输入变得优雅。</p>
</div>

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License" />
  <img src="https://img.shields.io/badge/Chrome-Extension-blue.svg" alt="Chrome Extension" />
  <img src="https://img.shields.io/badge/Manifest-V3-orange.svg" alt="Manifest V3" />
</p>

<p align="center">
  <a href="README.md">English</a> • <a href="README_zh-TW.md">繁體中文</a> • <strong>简体中文</strong>
</p>

---

### <img src="https://api.iconify.design/lucide/triangle-alert.svg?color=%23ff6b6b" width="18" height="18" /> 痛点

输入特殊符号（→ ⌘ ± × ÷ ≠ ∞ ★ ♥）需要记复杂的快捷键或在字符映射表里翻找。切换流程中断你的专注力。

### <img src="https://api.iconify.design/lucide/sparkles.svg?color=%23ff6b6b" width="18" height="18" /> 解决方案

SmilePicker 常驻在你的 Chrome 侧边面板 — 一个按键就到：

- **即时访问** — `Alt+S` 打开侧边面板，不用切换标签
- **智能搜索** — 用名称、关键字或外观找符号
- **一键复制** — 点击复制，粘贴到任何地方
- **收藏同步** — Chrome 账号同步收藏和设置
- **最近使用** — 快速访问最近 10 个符号
- **深色模式** — 浅色/深色/跟随系统主题

### <img src="https://api.iconify.design/lucide/package.svg?color=%23ff6b6b" width="18" height="18" /> 符号分类

- **箭头符号**：→ ← ↑ ↓ ⇒ ⇐ ⇑ ⇓
- **数学符号**：± × ÷ ≠ ∞ √ ∑ ∏
- **标点符号**：「」『』【】《》
- **键盘符号**：⌘ ⌥ ⇧ ⌃ ↵ ⌫
- **货币符号**：¥ € £ ₿ ₹ ₽
- **装饰符号**：★ ☆ ♥ ♦ ● ○ ■ □

### <img src="https://api.iconify.design/lucide/download.svg?color=%23ff6b6b" width="18" height="18" /> 安装

#### 从 Chrome Web Store（即将推出）
1. 前往 Chrome Web Store
2. 点击「添加到 Chrome」
3. 固定侧边面板

#### 开发者模式（当前）
1. Clone 此 repo：
   ```bash
   git clone https://github.com/Pauuulq87/SmilePicker.git
   cd SmilePicker
   ```

2. 安装依赖并构建：
   ```bash
   npm install
   npm run build
   ```

3. 加载到 Chrome：
   - 打开 `chrome://extensions/`
   - 启用「开发者模式」
   - 点击「加载已解压的扩展程序」
   - 选择 `dist/` 文件夹

### <img src="https://api.iconify.design/lucide/rocket.svg?color=%23ff6b6b" width="18" height="18" /> 使用方式

**打开侧边面板**
- 按 `Alt+S`（Windows/Linux）或在 `chrome://extensions/shortcuts` 自定义
- 点击扩展图标 → 「打开侧边面板」

**复制符号**
1. 搜索或浏览分类
2. 点击符号复制
3. 用 `Ctrl+V` 粘贴到任何地方

**收藏符号**
- 点击星号图标添加收藏
- 从顶部区块访问收藏

**键盘导航**
- `Tab` / `Shift+Tab` 切换
- `Enter` 复制选中的符号
- `Esc` 关闭搜索

### <img src="https://api.iconify.design/lucide/wrench.svg?color=%23ff6b6b" width="18" height="18" /> 开发

```bash
# 安装依赖
npm install

# 开发模式（热重载）
npm run dev

# 正式版构建
npm run build

# 类型检查
npm run type-check
```

**技术栈**
- TypeScript + React 18
- Tailwind CSS
- Vite + CRXJS
- Chrome Extension Manifest V3

---

<div align="center">
  <p><strong>MIT License</strong> - 专为文字工作者、开发者和高效用户打造。</p>
  <p><em>谢谢 GitHub 开发者把智慧与经验分享出来，才有今天的我。</em></p>
</div>
