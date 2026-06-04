# Solopreneurs Pages Dev - 進捗状況

> 最終更新: 2026-06-04

---

## プロジェクト概要

ソロプレナーとして起業したい人向けに、現代のソロプレナーの技術スタック・開発環境・作ったものを一覧化・比較できる静的サイト。

- **サイト名**: Solopreneurs Pages Dev
- **公開URL**: https://solopreneurs.pages.dev/
- **GitHub**: https://github.com/5olopreneur/solopreneurs

---

## 完了済み

### 要件定義（Grill-me Method）
- [x] コアバリューの確定
- [x] 掲載対象者の選定（Pieter Levels, Arvid Kahl, Tony Dinh）
- [x] データ収集方針の決定（公開情報 + LLM推測）
- [x] プライバシー・肖像権対策の方針確定
- [x] UI/UX設計の確定（カードグリッド + 中粒度6属性）
- [x] AI関連（プロダクト技術 + 開発生産性ツール）の掲載方針確定
- [x] サイト名・ドメイン名の決定

### インフラ・基盤構築
- [x] Astro 6.4.4 プロジェクト初期化
- [x] Cloudflare アダプター（`@astrojs/cloudflare`）導入
- [x] Tailwind CSS 導入（Astro 6 Vite プラグイン方式）
- [x] `wrangler.toml` 設定
- [x] GitHub リポジトリ作成済み（`github.com/5olopreneur/solopreneurs`）
- [x] ビルドパイプライン確認（`dist/` へ静的出力）

### サイト骨格実装
- [x] 共通レイアウト（`src/layouts/Layout.astro`）
  - ヘッダー（サイト名 + スナップショット日付表示）
  - フッター（免責事項 + 訂正依頼先メールアドレス）
  - X（Twitter）ウィジェット用 JS 読み込み
- [x] トップページ（`src/pages/index.astro`）
  - カードグリッド表示（1〜3カラム、レスポンシブ）
  - クライアントサイドフィルター（フロントエンド / バックエンド / データベース）
  - 各カードに：国旗、国名、プロダクト、技術スタック（推測）、情報源アイコン、確信度インジケーター
- [x] 詳細ページ（`src/pages/[id].astro`）
  - 基本プロフィール（名前、国旗、国名、プロダクト一覧）
  - 技術スタック6属性（フロントエンド、バックエンド、データベース、ホスティング、主要ライブラリ、AI/ML層）
  - 確信度バッジ（高/中/低）の色分け表示
  - 情報源アイコン（📄🐙🎙️）表示
  - 開発環境・AI生産性ツールセクション（コード補完、AIアシスタント、UI生成）
  - X（Twitter）タイムライン埋め込み
  - 情報源一覧セクション
- [x] ダミーデータ作成（`src/data/solopreneurs.json`）
  - 3名分の基本情報 + 技術スタック + 開発ツール

---

## 未完了タスク（TODO）

### データ品質
- [x] LLM推測用プロンプトの詳細設計 (`prompts/collect.md`, `prompts/infer.md`)
- [x] 実際の公開情報からのデータ収集・推測実行（Pieter Levels分完了）
- [x] 残り2名（Arvid Kahl, Tony Dinh）の推測実行
- [x] ダミーデータを本物の推測データに差し替え
- [x] 情報源URLの具体化（各属性に対する元リンク）

### コンテンツ・法務
- [ ] ロゴ・ファビコンのデザイン作成
- [ ] Xタイムライン埋め込み用の公式アカウント選定確認
  - Pieter Levels: `@levelsio`
  - Arvid Kahl: `@arvidkahl`
  - Tony Dinh: `@tdinh_me`
- [ ] 訂正・削除依頼用メールアドレスの有効化（現状はダミー）

### デプロイ・運用
- [ ] Cloudflare への初回デプロイ（`wrangler deploy` または GitHub Actions）
- [ ] デプロイ後の動作確認（フィルター、X埋め込み、レスポンシブ）
- [ ] Astro 6 のリリース状況確認（必要に応じてバージョン固定を解除）

### 将来拡張（反響があれば）
- [ ] 対象者の増加（+3〜5名）
- [ ] 情報収集→LLM推測のワークフロー自動化
- [ ] 収益モデルの検討（現状は非営利）

---

## 技術スタック（本サイト自体）

| レイヤー | 技術 |
|---------|------|
| フレームワーク | Astro 6.4.4 |
| スタイリング | Tailwind CSS 4.x（Vite プラグイン方式）|
| ホスティング | Cloudflare Pages |
| アダプター | `@astrojs/cloudflare` |
| デプロイツール | Wrangler |

---

## ファイル構成

```
solopreneurs/
├── astro.config.mjs          # Astro + Cloudflare + Tailwind 設定
├── package.json              # 依存関係
├── wrangler.toml             # Cloudflare 設定
├── tsconfig.json             # TypeScript 設定
├── spec.md                   # 要件定義書（Grill-me Method）
├── PROGRESS.md               # 本ファイル
├── src/
│   ├── layouts/
│   │   └── Layout.astro      # 共通レイアウト
│   ├── pages/
│   │   ├── index.astro       # トップページ（カードグリッド + フィルター）
│   │   └── [id].astro        # 詳細ページ（動的ルーティング）
│   ├── data/
│   │   └── solopreneurs.json # ソロプレナーデータ（現在はダミー）
│   └── styles/
│       └── global.css        # Tailwind CSS インポート + カスタムテーマ
└── public/
    └── favicon.svg           # デフォルトファビコン（要差し替え）
```

---

## 次のステップ候補

1. **データ収集・推測実行**: LLMプロンプトを設計し、3名分の本物のデータを生成して差し替え
2. **デプロイ**: `wrangler pages deploy dist` で Cloudflare に公開し、実際の動作確認
3. **見た目の微調整**: ロゴ作成、カードデザイン調整、モバイル表示の最適化
