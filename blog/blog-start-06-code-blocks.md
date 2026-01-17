---
title: "ブログの始め方入門 #06 - コードブロックの活用"
date: 2025-09-23
updated: 2025-09-30
tags:
  - サンプルシリーズ
  - ブログ入門
  - コードブロック
  - 技術記事
cover: https://images.unsplash.com/photo-1461749280684-dccba630e2f6?w=800
---

# ブログの始め方入門 #06 - コードブロックの活用

**前回**: [画像の活用法](/sample-blog/blog/blog-start-05-images.html)

---

## 技術ブログの核心 = コードブロック

技術ブログにおいて、**コードブロック**は最も重要な要素です。

読者が求めているのは「コピーして動くコード」。適切なコードブロックの使い方をマスターしましょう。

## 基本的な書き方

### インラインコード

文中で `const x = 1` のように短いコードを示すときに使います。

```markdown
変数 `count` を `0` で初期化します。
```

結果: 変数 `count` を `0` で初期化します。

### コードブロック（フェンスドコード）

````markdown
```言語名
コードの内容
```
````

**言語名を指定する**ことで、シンタックスハイライトが有効になります。

## 言語別のサンプル

### JavaScript / TypeScript

```javascript
// 配列の操作
const numbers = [1, 2, 3, 4, 5];

const doubled = numbers.map(n => n * 2);
const filtered = numbers.filter(n => n > 2);
const sum = numbers.reduce((acc, n) => acc + n, 0);

console.log({ doubled, filtered, sum });
```

```typescript
interface User {
  id: string;
  name: string;
  email: string;
  createdAt: Date;
}

const createUser = (name: string, email: string): User => ({
  id: crypto.randomUUID(),
  name,
  email,
  createdAt: new Date(),
});
```

### Python

```python
from dataclasses import dataclass
from datetime import datetime
from typing import List

@dataclass
class Article:
    title: str
    content: str
    tags: List[str]
    created_at: datetime = datetime.now()

    def word_count(self) -> int:
        return len(self.content.split())

# 使用例
article = Article(
    title="ブログの始め方",
    content="これはサンプル記事です。コードブロックの説明をしています。",
    tags=["入門", "ブログ"]
)
print(f"文字数: {article.word_count()}")
```

### Bash / Shell

```bash
#!/bin/bash

# ブログのセットアップスクリプト
echo "Setting up blog environment..."

# 依存関係のインストール
npm install

# 開発サーバーの起動
npm run dev &

# ビルド
npm run build

echo "Setup complete! 🎉"
```

### SQL

```sql
-- 記事の取得クエリ
SELECT 
    a.id,
    a.title,
    a.content,
    u.name AS author_name,
    COUNT(c.id) AS comment_count
FROM articles a
JOIN users u ON a.author_id = u.id
LEFT JOIN comments c ON a.id = c.article_id
WHERE a.published = TRUE
GROUP BY a.id, u.name
ORDER BY a.created_at DESC
LIMIT 10;
```

### JSON

```json
{
  "name": "my-blog",
  "version": "1.0.0",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  }
}
```

### CSS

```css
/* 記事カードのスタイル */
.article-card {
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  padding: 1.5rem;
  transition: transform 0.2s ease;
}

.article-card:hover {
  transform: translateY(-4px);
}

.article-card__title {
  font-size: 1.25rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}
```

### HTML

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Blog</title>
</head>
<body>
  <header>
    <h1>Welcome to My Blog</h1>
  </header>
  <main>
    <article>
      <h2>記事タイトル</h2>
      <p>記事の内容...</p>
    </article>
  </main>
</body>
</html>
```

## コードブロックの使い分け

### いつインラインを使うか

| シーン | 使うべき記法 |
| --- | --- |
| 変数名やファイル名に言及 | インライン `code` |
| コマンド1つを紹介 | インライン `npm install` |
| 複数行のコード | コードブロック |
| 実行可能なスニペット | コードブロック |

### diff表示

変更箇所を示すときに便利です：

```diff
- const oldValue = "before";
+ const newValue = "after";

  function unchanged() {
    // この行は変更なし
  }
```

## コードブロックのベストプラクティス

### 1. 動くコードを書く

> コピー&ペーストして動かないコードは、読者の信頼を失います

```javascript
// ❌ 悪い例：動作に必要な情報が不足
const result = fetchData();

// ✅ 良い例：自己完結している
const fetchData = async () => {
  const response = await fetch('https://api.example.com/data');
  return response.json();
};

const result = await fetchData();
console.log(result);
```

### 2. コメントを適切に入れる

```python
# 入力データの前処理
def preprocess(data):
    # 欠損値を平均で埋める
    data = data.fillna(data.mean())
    
    # 外れ値を除去（3σルール）
    mean = data.mean()
    std = data.std()
    data = data[(data - mean).abs() <= 3 * std]
    
    return data
```

### 3. 長すぎるコードは分割する

1つのコードブロックは**30行以内**を目安にしましょう。

<details>
<summary>長いコードを折りたたむ例</summary>

```typescript
// 完全なAPIクライアントの実装
interface ApiClientConfig {
  baseUrl: string;
  timeout?: number;
  headers?: Record<string, string>;
}

class ApiClient {
  private baseUrl: string;
  private timeout: number;
  private headers: Record<string, string>;

  constructor(config: ApiClientConfig) {
    this.baseUrl = config.baseUrl;
    this.timeout = config.timeout ?? 30000;
    this.headers = {
      'Content-Type': 'application/json',
      ...config.headers,
    };
  }

  async get<T>(path: string): Promise<T> {
    const response = await fetch(`${this.baseUrl}${path}`, {
      method: 'GET',
      headers: this.headers,
    });
    return response.json();
  }

  async post<T>(path: string, body: unknown): Promise<T> {
    const response = await fetch(`${this.baseUrl}${path}`, {
      method: 'POST',
      headers: this.headers,
      body: JSON.stringify(body),
    });
    return response.json();
  }
}
```

</details>

### 4. エラーハンドリングを含める

```javascript
// ✅ エラーハンドリングを含めた例
async function fetchUserData(userId) {
  try {
    const response = await fetch(`/api/users/${userId}`);
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    return await response.json();
  } catch (error) {
    console.error('Failed to fetch user:', error);
    throw error;
  }
}
```

## 数式とコードの組み合わせ

技術的な説明では、数式とコードを組み合わせると効果的です。

### 例：二分探索

二分探索の計算量は $O(\log n)$ です。

$$
T(n) = T\left(\frac{n}{2}\right) + O(1)
$$

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1
```

## よくある失敗

### ❌ 失敗1: 言語指定なし

````markdown
```
const x = 1;  // ハイライトされない
```
````

### ❌ 失敗2: インデントの乱れ

```javascript
// 悪い例
function bad(){
let x=1;
    if(x){
  console.log(x);
    }
}
```

```javascript
// 良い例
function good() {
  let x = 1;
  if (x) {
    console.log(x);
  }
}
```

### ❌ 失敗3: 古いコードをそのまま

ライブラリのバージョンや非推奨のAPIに注意しましょう。

```javascript
// ❌ 古い書き方
var self = this;
$.ajax({
  url: '/api/data',
  success: function(data) {
    self.setState({ data: data });
  }
});

// ✅ モダンな書き方
const response = await fetch('/api/data');
const data = await response.json();
setData(data);
```

## チェックリスト

公開前に確認しましょう：

- [x] 言語名を指定しているか
- [x] コピーして動作するか
- [x] 適切なコメントがあるか
- [x] インデントは揃っているか
- [x] 長すぎないか（30行以内）

## まとめ

コードブロック活用のポイント：

| ポイント | 説明 |
| --- | --- |
| 言語を指定 | シンタックスハイライトのため |
| 動くコードを書く | 読者の信頼を得る |
| コメントを入れる | 意図を伝える |
| 短く保つ | 30行以内を目安に |

次回は、記事の整理に欠かせない「タグとカテゴリ」について解説します 🏷️

---

**次回**: [タグとカテゴリ - 記事の整理術](/sample-blog/blog/blog-start-07-tags-categories.html)

**前回**: [画像の活用法](/sample-blog/blog/blog-start-05-images.html)

