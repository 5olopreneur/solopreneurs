# Data Management Skill

## 概要

ソロプレナーデータは `src/data/solopreneurs.json` で管理されています。

## データ構造

```typescript
interface Solopreneur {
  id: string;                    // URLスラッグ（例: pieter-levels）
  name: string;                  // 表示名
  country: string;               // 国名
  countryCode: string;           // 国旗絵文字（例: 🇳🇱）
  products: string[];            // プロダクト一覧
  techStack: {
    frontend: string[];          // フロントエンド技術
    backend: string[];           // バックエンド技術
    database: string[];          // データベース
    hosting: string[];           // ホスティング
    libraries: string[];         // 主要ライブラリ
    ai: string[];                // AI/ML層
  };
  devEnvironment: {
    codeCompletion: string;      // コード補完ツール
    aiAssistant: string;         // AIアシスタント
    uiGeneration: string;        // UI生成ツール
  };
  sources: Array<{
    type: 'blog' | 'github' | 'podcast' | 'sns';
    url: string;
    title: string;
  }>;
  confidence: 'high' | 'medium' | 'low';
  xAccount: string;              // Xアカウント（@なし）
}
```

## データ更新時の注意

1. **JSONの整合性**: 配列のカンマ、閉じ括弧に注意
2. **推測ラベル**: 確信度が `medium` または `low` の場合、UI上で「推測」と表示
3. **情報源**: 各属性の根拠となるURLを `sources` に記載
4. **免責**: 推測情報には必ず「⚠️ 推測」ラベルを付与

## 追加・削除の手順

### ソロプレナーを追加

1. `solopreneurs.json` に新しいオブジェクトを追加
2. `src/pages/[id].astro` の `getStaticPaths` に `id` を追加（Astroの静的生成に必要）
3. 画像が必要な場合は `public/` に配置

### ソロプレナーを削除

1. `solopreneurs.json` から該当オブジェクトを削除
2. `getStaticPaths` から該当 `id` を削除
