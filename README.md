# Solopreneurs Pages Dev

現代の代表的ソロプレナーの技術スタック・開発環境・作ったものを一覧化・比較できる静的サイト。

- **公開URL**: https://solopreneurs.pages.dev/
- **GitHub**: https://github.com/5olopreneur/solopreneurs

## 技術スタック

- [Astro](https://astro.build/) 6.x
- [Tailwind CSS](https://tailwindcss.com/) 4.x
- Cloudflare Pages

## データ規約

`solopreneurs.json` に技術スタックなどを記述する際は、以下を統一してください。

- **区切り文字はカンマ（,）のみ**: 複数技術を列挙する際は `/` ではなく `,` を使用
- **`shadcn/ui` は `shadcnUi` と表記**: `shadcnUI` なども `shadcnUi` に統一
- **`Postgres` は `PostgreSQL` と表記**: 正式名称で統一

## 開発コマンド

| Command           | Action                                      |
| :---------------- | :------------------------------------------ |
| `npm install`     | 依存パッケージのインストール                |
| `npm run dev`     | ローカル開発サーバーを起動 (`localhost:4321`) |
| `npm run build`   | 静的サイトを `./dist/` にビルド             |
| `npm run preview` | ビルド結果をローカルでプレビュー            |
