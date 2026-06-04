# 技術スタック推測プロンプト

## 目的

情報収集フェーズで作成された「観察メモ」を入力として、各技術スタック属性の**最も確からしい値**を推測し、`solopreneurs.json` 形式のJSONを出力する。

## 入力

- 対象ソロプレナーの観察メモ（`collect.md` の出力）
- 対象ソロプレナーの基本情報（名前、国、プロダクト一覧、Xアカウント）

## 推論ルール

### 確信度（certainty）の判定基準

| 確信度 | 条件 |
|--------|------|
| **high** | 複数の独立した情報源（📄🐙🎙️🐦のうち2種類以上）で同一の技術が言及されている。または、GitHubの言語統計・package.jsonなどの客観的データで示されている。 |
| **medium** | 1つの情報源で明示的に言及されている。または、複数の断片的な言及から整合的に読み取れる。 |
| **low** | 推論が必要。類似プロダクトの一般的な技術選定、または1つの断片的な言及に基づく。間違いの可能性が高いことを前提とする。 |

### 各属性の推測ガイドライン

| 属性 | 推測の根拠 | 注意点 |
|------|-----------|--------|
| **frontend** | プロダクトのUI技術。React/Vue/Svelte/純正JSなど。 | SPAかMPAか、SSRの有無も考慮 |
| **backend** | サーバーサイド言語・ランタイム。Node.js/Python/Go/Ruby/PHPなど。 | Serverless（Lambda等）の場合は言語ではなくプラットフォームも記録 |
| **database** | 永続化層。PostgreSQL/MySQL/MongoDB/Firebase/Supabaseなど。 | 複数DBを使い分けている場合は主要な1〜2つを記録 |
| **hosting** | インフラ・デプロイ先。AWS/Vercel/Heroku/Cloudflare/自前サーバーなど。 | CDNやエッジ機能の有無も考慮 |
| **libraries** | 主要フレームワーク・ライブラリ。Next.js/Tailwind/Prisma/Electron/Stripeなど。 | 3〜5個程度に絞り、プロダクトの特性と最も関連深いものを優先 |
| **ai** | AI/ML層。OpenAI API/Stable Diffusion/Replicate/LangChain/Pineconeなど。 | AI関連プロダクトの場合は必須。非AIプロダクトでもChatGPT API等を使っている場合は記録 |

### 開発ツール（devTools）の推測ガイドライン

| 属性 | 推測の根拠 | 注意点 |
|------|-----------|--------|
| **codeAI** | コード補完・生成ツール。Cursor/GitHub Copilot/Windsurf/Replit Agentなど。 | 本人が明示的に言及していない場合は `null` |
| **assistant** | AIアシスタント。Claude/ChatGPT/Gemini/Perplexityなど。 | 同上。推測はしない |
| **uiGen** | UI生成・プロトタイピングツール。v0/Bolt/Tempo/Lovableなど。 | 同上。推測はしない |

## 出力形式（厳密JSON）

```json
{
  "id": "[URLスラッグ（kebab-case）]",
  "name": "[フルネーム]",
  "country": "[英語国名]",
  "countryCode": "[ISO 3166-1 alpha-2（大文字2文字）]",
  "flag": "[国旗絵文字]",
  "products": ["[プロダクト名1]", "[プロダクト名2]"],
  "xHandle": "[Xアカウント（@なし）]",
  "techStack": {
    "frontend": {
      "value": "[技術名]",
      "sources": ["blog", "github"],
      "certainty": "high"
    },
    "backend": {
      "value": "[技術名]",
      "sources": ["blog"],
      "certainty": "medium"
    },
    "database": {
      "value": "[技術名]",
      "sources": ["podcast"],
      "certainty": "medium"
    },
    "hosting": {
      "value": "[技術名]",
      "sources": ["github"],
      "certainty": "low"
    },
    "libraries": {
      "value": "[技術名1, 技術名2]",
      "sources": ["blog", "github"],
      "certainty": "medium"
    },
    "ai": {
      "value": "[技術名1, 技術名2]",
      "sources": ["blog"],
      "certainty": "high"
    }
  },
  "devTools": {
    "codeAI": "[Cursor / GitHub Copilot / null]",
    "assistant": "[Claude / ChatGPT / null]",
    "uiGen": "[v0 / Bolt / null]"
  },
  "inferenceNotes": "[推測に際しての補足説明。確信度がlowの属性の根拠、複数候補があった場合の選定理由など]"
}
```

## 禁止事項

- `null` 以外で推測で埋めない（わからない場合は確信度を `low` にしても値は入れるが、devToolsは `null` を許容）
- 情報源にない技術を「一般的だから」と勝手に追加しない
- 古い情報（「3年前は〜を使っていた」）を現在の技術スタックとして扱わない
