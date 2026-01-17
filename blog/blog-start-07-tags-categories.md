---
title: "ブログの始め方入門 #07 - タグとカテゴリ"
date: 2025-10-07
updated: 2025-10-14
tags:
  - サンプルシリーズ
  - ブログ入門
  - タグ
  - カテゴリ
  - 整理術
cover: https://images.unsplash.com/photo-1507925921958-8a62f3d1a50d?w=800
---

# ブログの始め方入門 #07 - タグとカテゴリ

> ⚠️ **注意**: このシリーズの内容はすべて生成AIによって作成されたサンプルコンテンツです。記載されている情報の正確性は検証されておらず、裏取りも行っていません。実際のブログ運営に活用する際は、ご自身で内容を確認してください。

**前回**: [コードブロックの活用](/sample-blog/blog/blog-start-06-code-blocks.html)

---

## 記事が増えると混乱する

ブログを続けていると、記事がどんどん増えていきます。

> 100記事を超えたあたりから、自分でも「あの記事どこだっけ？」となります

適切な**タグ**と**カテゴリ**で整理することで、読者も自分も記事を見つけやすくなります。

## タグとカテゴリの違い

### カテゴリ = 階層的な分類

本棚の「棚」のようなもの。1つの記事は**1つのカテゴリ**に属します。

```
📁 プログラミング
├── 📁 Python
├── 📁 JavaScript
└── 📁 Go

📁 ライフスタイル
├── 📁 生産性
└── 📁 健康
```

### タグ = 横断的なラベル

付箋のようなもの。1つの記事に**複数のタグ**を付けられます。

```
記事「Pythonで自動化」
├── 🏷️ Python
├── 🏷️ 自動化
├── 🏷️ 初心者向け
└── 🏷️ 業務効率化
```

### 比較表

| 特徴 | カテゴリ | タグ |
| --- | --- | --- |
| 数 | 1記事に1つ | 1記事に複数 |
| 構造 | 階層的 | フラット |
| 用途 | 大分類 | 詳細な分類 |
| 例 | 本のジャンル | 索引のキーワード |

## タグ設計の原則

### 原則1: 一貫性を保つ

同じ概念には同じタグを使います。

```
❌ 悪い例
記事A: Python, python, パイソン
記事B: JavaScript, JS, ジャバスクリプト

✅ 良い例
記事A: Python
記事B: JavaScript
```

### 原則2: 粒度を揃える

抽象度が異なるタグを混ぜないようにします。

```
❌ 悪い例
プログラミング, Python, リスト内包表記
（粒度がバラバラ）

✅ 良い例
言語レベル: Python, JavaScript, Go
機能レベル: 配列操作, 非同期処理, エラーハンドリング
```

### 原則3: 適度な数に抑える

タグが多すぎると意味がなくなります。

$$
\text{タグの価値} = \frac{\text{発見性の向上}}{\text{タグの総数}}
$$

**目安**:
- 1記事につき3〜7個
- 全体で50〜100個程度

## タグの命名規則

### 一般的なパターン

| パターン | 例 | 特徴 |
| --- | --- | --- |
| 言語名 | Python, JavaScript | 技術記事に必須 |
| レベル | 初心者向け, 上級者向け | 読者層を明示 |
| 形式 | チュートリアル, チートシート | 記事の種類 |
| トピック | 自動化, テスト, CI/CD | 具体的な内容 |

### 表記の統一

```yaml
# 推奨: 統一されたフォーマット
tags:
  - JavaScript      # 言語名は正式表記
  - TypeScript
  - 初心者向け       # 日本語は平仮名統一
  - チュートリアル   # カタカナは長音含む
```

## 実践：タグ設計の例

### 技術ブログの場合

```yaml
# 言語・技術
- JavaScript
- TypeScript
- Python
- React
- Vue
- Node.js

# レベル
- 初心者向け
- 中級者向け
- 上級者向け

# トピック
- Webフロントエンド
- バックエンド
- データベース
- DevOps
- 機械学習

# 形式
- チュートリアル
- Tips
- トラブルシューティング
- レビュー
```

### 生活系ブログの場合

```yaml
# カテゴリ的タグ
- 料理
- 旅行
- 読書
- 映画

# 詳細タグ
- レシピ
- 国内旅行
- 海外旅行
- 書評
- 映画レビュー

# メタタグ
- おすすめ
- まとめ
- 体験談
```

## Frontmatterでの設定

[書式テクニックのFrontmatterの節](/sample-blog/blog/blog-start-04-formatting.html#frontmatterでの設定)で学んだFrontmatterを使います：

```yaml
---
title: "ReactでTodoアプリを作る"
date: "2025-10-01"
tags:
  - JavaScript
  - React
  - チュートリアル
  - 初心者向け
category: プログラミング
---
```

## タグの活用方法

### 1. 関連記事の表示

同じタグを持つ記事を「関連記事」として表示します。

```
この記事を読んだ人はこちらも読んでいます：
├── [Reactの基礎を学ぶ] (タグ: React, 初心者向け)
├── [Reactのベストプラクティス] (タグ: React, 中級者向け)
└── [React vs Vue 比較] (タグ: React, Vue, 比較)
```

### 2. タグクラウド

人気のタグを視覚的に表示します：

<div style="display: flex; flex-wrap: wrap; gap: 8px;">
  <span style="font-size: 1.5em;">JavaScript</span>
  <span style="font-size: 1.2em;">Python</span>
  <span style="font-size: 1.3em;">React</span>
  <span style="font-size: 1.0em;">Vue</span>
  <span style="font-size: 1.4em;">初心者向け</span>
  <span style="font-size: 0.9em;">DevOps</span>
</div>

### 3. フィルタリング

読者が興味のあるタグで記事を絞り込めます。

<details>
<summary>タグフィルターの実装例</summary>

```typescript
interface Article {
  title: string;
  tags: string[];
}

function filterByTags(articles: Article[], selectedTags: string[]): Article[] {
  if (selectedTags.length === 0) return articles;
  
  return articles.filter(article =>
    selectedTags.every(tag => article.tags.includes(tag))
  );
}

// 使用例
const filtered = filterByTags(articles, ['React', '初心者向け']);
```

</details>

## よくある失敗

### ❌ 失敗1: タグの乱立

```yaml
# 悪い例：タグが多すぎる
tags:
  - JavaScript
  - JS
  - プログラミング
  - コーディング
  - Web
  - Webサイト
  - フロントエンド
  - frontend
  - 開発
  - 開発者向け
```

### ❌ 失敗2: 1記事だけのタグ

そのタグが付いた記事が1つしかないなら、タグの意味がありません。

```
タグ「2025年1月10日に書いた記事」 → ❌ 意味がない
タグ「Python」 → ✅ 複数記事で使える
```

### ❌ 失敗3: 曖昧なタグ

```yaml
# 悪い例
tags:
  - いろいろ
  - その他
  - メモ

# 良い例
tags:
  - 雑記
  - 日記
  - 技術メモ
```

## タグ管理のTips

### 定期的な棚卸し

3〜6ヶ月に一度、タグを見直しましょう：

- [ ] 使われていないタグを削除
- [ ] 類似タグを統合
- [ ] 新しいタグの追加を検討

### タグ一覧を作る

管理用のドキュメントを作成しておくと便利です：

```markdown
# タグ一覧

## 言語・技術
- JavaScript: JavaScriptに関する記事
- Python: Pythonに関する記事
- ...

## レベル
- 初心者向け: プログラミング経験1年未満の方向け
- 中級者向け: 基礎文法を理解している方向け
- ...
```

## チェックリスト

記事公開前に確認しましょう：

- [x] タグは3〜7個程度か
- [x] 表記は統一されているか
- [x] 既存のタグを使っているか
- [x] 新しいタグは本当に必要か
- [x] 曖昧すぎるタグはないか

## まとめ

タグとカテゴリのポイント：

| ポイント | 説明 |
| --- | --- |
| 一貫性 | 同じ概念には同じタグ |
| 粒度 | 抽象度を揃える |
| 数 | 1記事3〜7個、全体50〜100個 |
| 管理 | 定期的に棚卸しする |

適切なタグ設計は、読者の回遊率を高め、ブログ全体の価値を上げます 🏷️

次回は、検索エンジンからの流入を増やす「SEOの基本」を解説します。

---

**次回**: [SEOの基本 - 検索で見つけてもらうために](/sample-blog/blog/blog-start-08-seo-basics.html)

**前回**: [コードブロックの活用](/sample-blog/blog/blog-start-06-code-blocks.html)

