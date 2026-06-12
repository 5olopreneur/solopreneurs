# データ規約の正規化

`src/data/solopreneurs.json` の表記を以下の規約に統一してください。

## 正規化ルール

1. **区切り文字をカンマ（,）に統一**
   - 技術スタックやツールの列挙で `/` が使われている場合は `, ` に置き換え
   - 例: `Node.js / Express` → `Node.js, Express`
2. **`shadcn/ui` を `shadcnUi` に統一**
   - `shadcn/ui` や `shadcnUI` の表記を `shadcnUi` に置き換え
3. **`Postgres` を `PostgreSQL` に統一**
   - `Postgres` 表記を `PostgreSQL` に置き換え

## 手順

1. `src/data/solopreneurs.json` を読み込む
2. 上記ルールに該当する `value` 文字列と `devTools` 内の文字列を修正
3. `npm run build` を実行してビルドが通ることを確認
4. 変更差分を確認してからコミット

## 注意

- カンマの後にはスペースを入れて可読性を保つ
- `shadcn/ui` などのライブラリ名以外の `/`（例: URL 内）は置き換えない
