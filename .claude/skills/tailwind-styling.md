# Tailwind CSS Styling Skill

## 概要

このプロジェクトでは **Tailwind CSS 4.x** を使用しています。

## 設定方法

Astro 6 の Vite プラグイン方式で統合されています。
グローバルCSSは `src/styles/global.css` で `@import "tailwindcss"` しています。

## コーディング規約

1. **ユーティリティクラス優先**: 基本はTailwindのクラスを使用
2. **レスポンシブ**: `sm:`, `md:`, `lg:` プレフィックスを使用
3. **カスタム値**: 必要に応じて `global.css` で `@theme` や `@layer` を定義
4. **ダークモード**: 現状は未対応（必要であれば検討）

## 推奨パターン

### レイアウト

```html
<div class="container mx-auto px-4 py-8">
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
    <!-- カード -->
  </div>
</div>
```

### カード

```html
<div class="bg-white rounded-xl shadow-md p-6 hover:shadow-lg transition-shadow">
  <h2 class="text-xl font-bold text-gray-900">タイトル</h2>
  <p class="text-gray-600 mt-2">本文</p>
</div>
```

### バッジ

```html
<span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-blue-100 text-blue-800">
  ラベル
</span>
```

## 注意事項

- Tailwind CSS 4.xでは設定ファイルが不要な場合がある（CSSベースの設定）
- `postcss.config.mjs` で `@tailwindcss/postcss` を使用
