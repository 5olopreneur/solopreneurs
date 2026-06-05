# デプロイ

Cloudflare Pages にデプロイします。

## 方法1: Git連携（推奨）

Cloudflare ダッシュボードで本リポジトリと連携し、Push時に自動デプロイされるよう設定してください。

## 方法2: 手動アップロード

```bash
npm run build
```

ビルド成功後、Cloudflare ダッシュボードから `dist/` ディレクトリをドラッグ＆ドロップでアップロードしてください。

## 注意

- `wrangler.toml` は存在しないため、`wrangler pages deploy` コマンドはそのままでは使えません
- デプロイ前に必ずビルドが成功することを確認してください
