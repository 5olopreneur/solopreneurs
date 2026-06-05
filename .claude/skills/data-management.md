# Data Management Skill

## 概要

ソロプレナーデータは `src/data/solopreneurs.json` で管理されています。

## データ構造

```typescript
interface Solopreneur {
  id: string;                    // URLスラッグ（例: pieter-levels）
  name: string;                  // 表示名
  emoji: string;                 // プロフィール絵文字
  country: string;               // 国名
  countryCode: string;           // ISO 3166-1 alpha-2（大文字2文字、例: NL）
  flag: string;                  // 国旗絵文字（例: 🇳🇱）
  products: Array<{              // プロダクト一覧
    name: string;
    url: string | null;
    description: string;
  }>;
  xHandle: string;               // Xアカウント（@なし）
  xFollowers: number;            // Xフォロワー数
  techStack: {
    frontend:  { value: string; sources: Source[]; certainty: 'high' | 'medium' | 'low' };
    backend:   { value: string; sources: Source[]; certainty: 'high' | 'medium' | 'low' };
    database:  { value: string; sources: Source[]; certainty: 'high' | 'medium' | 'low' };
    hosting:   { value: string; sources: Source[]; certainty: 'high' | 'medium' | 'low' };
    libraries: { value: string; sources: Source[]; certainty: 'high' | 'medium' | 'low' };
    ai:        { value: string; sources: Source[]; certainty: 'high' | 'medium' | 'low' };
  };
  businessStrategy: Array<{
    name: string;
    description: string;
  }>;
  marketing: Array<{
    name: string;
    description: string;
  }>;
  devTools: {
    codeAI: string | null;       // コード補完・生成ツール（Cursor / GitHub Copilot 等）
    assistant: string | null;    // AIアシスタント（Claude / ChatGPT 等）
    uiGen: string | null;        // UI生成ツール（v0 / Bolt 等）
  };
}

interface Source {
  type: 'blog' | 'github' | 'podcast' | 'x';
  url: string;
  title: string;
}
```

## データ更新時の注意

1. **JSONの整合性**: 配列のカンマ、閉じ括弧に注意
2. **確信度（certainty）**: `medium` または `low` の場合、UI上で「⚠️」アイコンが表示される
3. **情報源（sources）**: 各属性の根拠となるURLを `{type, url, title}` 形式で記載
4. **ビジネス戦略・マーケティング**: サイトのフィルター機能に使用される。`name` に補足説明の括弧を含める場合は、`normalizeLabel` で正規化されるため選択肢に影響する
5. **技術スタックの value**: カンマ区切りで複数技術を記載可能。`extractTechs` によって個別に分解されフィルター選択肢になる
6. **xFollowers**: 数値（単位なし）。UI上で「万」に変換して表示される

## 追加・削除の手順

### ソロプレナーを追加

1. `solopreneurs.json` に新しいオブジェクトを追加
2. `id` は kebab-case で、他と重複しないことを確認
3. `xHandle` が存在しない場合は `null` を設定
4. `devTools` の各値は本人が明示的に言及している場合のみ入力し、不明な場合は `null`

### ソロプレナーを削除

1. `solopreneurs.json` から該当オブジェクトを削除
2. `[id].astro` は `solopreneurs.json` から動的に `getStaticPaths` を生成するため、ページ側の修正は不要
