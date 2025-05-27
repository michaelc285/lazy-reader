[EN English README](README.md)

# Lazy Reader 懶鬼閱讀器

Lazy Reader 懶鬼閱讀器 是一款專為中文文本設計的網頁速讀工具，透過逐字呈現的方式，幫助使用者高效閱讀。此工具基於 SvelteKit、TypeScript 和純 CSS 構建，提供乾淨、響應式的介面，適用於桌面和行動裝置，非常適合閱讀中文文章、學習材料或文學作品。

[Click me for DEMO](https://michaelc285.github.io/lazy-reader/)

## 功能特色

- **中文文本輸入**：可輸入任意長度的中文文本，無字數限制。
- **標點符號開關**：可選擇保留或移除中文標點符號（例如：。 ， ！）。
- **逐字播放**：每次顯示一個中文字符或單詞，並可自訂播放速度（100–1000 字/分鐘，預設 500）。

## 使用場景

- **閱讀練習**：透過文章或書籍提升中文閱讀速度。
- **學習輔助**：將繁重的中文學習材料拆解成可管理的片段。
- **語言學習**：專注於個別字符或詞語，以增強理解能力。

## 快速開始

### 先決條件

- Node.js (v18 或更高)
- pnpm (v8 或更高)

### 安裝步驟

Clone the repository:
```bash
   git clone git@github.com:michaelc285/lazy-reader.git
   cd lazy-reader
```

Install dependencies:
```bash
pnpm install
```

Start the development server:
```bash
pnpm dev
```

Open http://localhost:5173 in your browser to view the app.


Build for Production

Build the project:
```bash
pnpm build
```

Deploy:
```bash
pnpm run deploy
```