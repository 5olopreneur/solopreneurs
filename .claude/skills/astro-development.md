# Astro Development Skill

## 概要

このプロジェクトでは **Astro 6.x** を使用した静的サイト開発を行います。

## 基本ルール

- **出力モード**: `static`（`astro.config.mjs` で `output: 'static'`）
- **サイトURL**: `https://solopreneurs.pages.dev/`
- **コンポーネント**: `.astro` ファイルを基本とする
- **スタイリング**: Tailwind CSS 4.x（Vite プラグイン方式）

## ファイル構成

```
src/
├── layouts/       # レイアウトコンポーネント
├── pages/         # ページコンポーネント（ルーティング）
├── data/          # JSONデータ
└── styles/        # グローバルCSS
public/            # 静的アセット
```

## コーディング規約

1. **フロントマター**: Astroコンポーネントは `---` で囲まれたフロントマターでサーバーサイド処理を記述
2. **クライアントJS**: `client:*` ディレクティブを使ってハイドレーションを制御
3. **スタイル**: Tailwindのユーティリティクラスを優先。カスタムCSSが必要な場合は `src/styles/global.css` に追記
4. **画像**: `public/` に配置し、絶対パス `/` で参照

## よく使うパターン

### ページ作成

```astro
---
import Layout from '../layouts/Layout.astro';
---

<Layout title="ページタイトル">
  <main class="container mx-auto px-4">
    <!-- コンテンツ -->
  </main>
</Layout>
```

### 動的ルーティング

```astro
---
import solopreneurs from '../data/solopreneurs.json';

export function getStaticPaths() {
  return solopreneurs.map((s) => ({
    params: { id: s.id },
    props: { solopreneur: s },
  }));
}
const { solopreneur } = Astro.props;
---
```

## 注意事項

- `dist/` はビルド成果物なので手動で編集しない
- `node_modules/` は編集しない
- TypeScript strictモードを遵守
