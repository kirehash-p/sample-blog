---
title: "ブログの始め方入門 #11 - 自作ブログ構築（後編）"
date: 2025-12-02
updated: 2025-12-10
tags:
  - サンプルシリーズ
  - ブログ入門
  - 自作ブログ
  - デプロイ
  - Cloudflare Pages
  - CI/CD
cover: https://images.unsplash.com/photo-1451187580459-43490279c0fa?w=800
---

# ブログの始め方入門 #11 - 自作ブログ構築（後編）

**前回**: [自作ブログ構築（前編）](/sample-blog/blog/blog-start-10-build-blog-part1.html)

---

## 後編の目標

前編で基礎を構築しました。後編では以下を完成させます：

- [x] ルーティングの設定
- [x] 記事一覧・詳細ページ
- [x] ダークモード対応
- [x] ビルドとデプロイ
- [x] CI/CDの設定

## ルーティングの設定

### React Routerのインストール

```bash
npm install react-router-dom
```

### ルーター設定

`src/App.tsx`:

```tsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import { Layout } from './components/Layout';
import { Home } from './pages/Home';
import { ArticlePage } from './pages/Article';
import { NotFound } from './pages/NotFound';

export function App() {
  return (
    <BrowserRouter>
      <Layout>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/article/:slug" element={<ArticlePage />} />
          <Route path="*" element={<NotFound />} />
        </Routes>
      </Layout>
    </BrowserRouter>
  );
}
```

## 記事一覧ページ

`src/pages/Home.tsx`:

```tsx
import { useState, useEffect } from 'react';
import { ArticleCard } from '../components/ArticleCard';
import type { ArticleIndex } from '../types';

export function Home() {
  const [articles, setArticles] = useState<ArticleIndex[]>([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function fetchArticles() {
      try {
        // 記事インデックスを取得
        const response = await fetch('/blog/index.json');
        const data = await response.json();
        
        // 日付でソート（新しい順）
        const sorted = data.sort((a: ArticleIndex, b: ArticleIndex) => 
          new Date(b.meta.date).getTime() - new Date(a.meta.date).getTime()
        );
        
        setArticles(sorted);
      } catch (error) {
        console.error('Failed to fetch articles:', error);
      } finally {
        setLoading(false);
      }
    }

    fetchArticles();
  }, []);

  if (loading) {
    return (
      <div className="flex justify-center items-center h-64">
        <div className="animate-spin rounded-full h-8 w-8 border-b-2 border-blue-500" />
      </div>
    );
  }

  return (
    <div>
      <h1 className="text-3xl font-bold mb-8 text-gray-900 dark:text-white">
        最新の記事
      </h1>
      
      <div className="grid gap-6 md:grid-cols-2">
        {articles.map(article => (
          <ArticleCard
            key={article.slug}
            slug={article.slug}
            {...article.meta}
          />
        ))}
      </div>
    </div>
  );
}
```

## 記事詳細ページ

`src/pages/Article.tsx`:

```tsx
import { useParams, Link } from 'react-router-dom';
import { useArticle } from '../hooks/useArticle';

export function ArticlePage() {
  const { slug } = useParams<{ slug: string }>();
  const { article, loading, error } = useArticle(slug!);

  if (loading) {
    return (
      <div className="flex justify-center items-center h-64">
        <div className="animate-spin rounded-full h-8 w-8 border-b-2 border-blue-500" />
      </div>
    );
  }

  if (error || !article) {
    return (
      <div className="text-center py-16">
        <h1 className="text-2xl font-bold text-gray-900 dark:text-white">
          記事が見つかりません
        </h1>
        <Link to="/" className="mt-4 text-blue-500 hover:underline">
          トップに戻る
        </Link>
      </div>
    );
  }

  const { meta, html } = article;

  return (
    <article className="max-w-3xl mx-auto">
      {/* ヘッダー */}
      <header className="mb-8">
        {meta.cover && (
          <img
            src={meta.cover}
            alt={meta.title}
            className="w-full h-64 object-cover rounded-lg mb-6"
          />
        )}
        
        <h1 className="text-4xl font-bold text-gray-900 dark:text-white">
          {meta.title}
        </h1>
        
        <div className="mt-4 flex items-center gap-4 text-gray-600 dark:text-gray-400">
          <time>{meta.date}</time>
          {meta.updated && (
            <span>更新: {meta.updated}</span>
          )}
        </div>
        
        <div className="mt-4 flex flex-wrap gap-2">
          {meta.tags.map(tag => (
            <span
              key={tag}
              className="px-3 py-1 text-sm bg-blue-100 text-blue-800 
                       dark:bg-blue-900 dark:text-blue-200 rounded-full"
            >
              {tag}
            </span>
          ))}
        </div>
      </header>

      {/* 本文 */}
      <div 
        className="prose prose-lg dark:prose-invert max-w-none"
        dangerouslySetInnerHTML={{ __html: html }}
      />

      {/* フッター */}
      <footer className="mt-16 pt-8 border-t">
        <Link 
          to="/"
          className="text-blue-500 hover:underline"
        >
          ← 記事一覧に戻る
        </Link>
      </footer>
    </article>
  );
}
```

## ダークモード対応

### テーマフックの作成

`src/hooks/useTheme.ts`:

```typescript
import { useState, useEffect } from 'react';

type Theme = 'light' | 'dark' | 'system';

export function useTheme() {
  const [theme, setTheme] = useState<Theme>(() => {
    if (typeof window === 'undefined') return 'system';
    return (localStorage.getItem('theme') as Theme) || 'system';
  });

  useEffect(() => {
    const root = document.documentElement;
    
    const applyTheme = (t: Theme) => {
      if (t === 'system') {
        const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
        root.classList.toggle('dark', prefersDark);
      } else {
        root.classList.toggle('dark', t === 'dark');
      }
    };

    applyTheme(theme);
    localStorage.setItem('theme', theme);

    // システムテーマの変更を監視
    const mediaQuery = window.matchMedia('(prefers-color-scheme: dark)');
    const handler = () => {
      if (theme === 'system') applyTheme('system');
    };
    
    mediaQuery.addEventListener('change', handler);
    return () => mediaQuery.removeEventListener('change', handler);
  }, [theme]);

  return { theme, setTheme };
}
```

### テーマ切り替えボタン

`src/components/ThemeToggle.tsx`:

```tsx
import { useTheme } from '../hooks/useTheme';

export function ThemeToggle() {
  const { theme, setTheme } = useTheme();

  const icons = {
    light: '☀️',
    dark: '🌙',
    system: '💻',
  };

  const nextTheme = {
    light: 'dark',
    dark: 'system',
    system: 'light',
  } as const;

  return (
    <button
      onClick={() => setTheme(nextTheme[theme])}
      className="p-2 rounded-lg hover:bg-gray-200 dark:hover:bg-gray-700 
                 transition-colors"
      aria-label={`現在のテーマ: ${theme}`}
    >
      <span className="text-xl">{icons[theme]}</span>
    </button>
  );
}
```

## ビルドスクリプト

### 記事インデックスの生成

`scripts/generate-index.mjs`:

```javascript
import fs from 'fs/promises';
import path from 'path';
import matter from 'gray-matter';

const BLOG_DIR = './public/blog';
const OUTPUT_FILE = './public/blog/index.json';

async function generateIndex() {
  const files = await fs.readdir(BLOG_DIR);
  const mdFiles = files.filter(f => f.endsWith('.md'));
  
  const articles = await Promise.all(
    mdFiles.map(async (filename) => {
      const filepath = path.join(BLOG_DIR, filename);
      const content = await fs.readFile(filepath, 'utf-8');
      const { data } = matter(content);
      
      return {
        slug: filename.replace('.md', ''),
        meta: data,
      };
    })
  );

  // 日付でソート
  articles.sort((a, b) => 
    new Date(b.meta.date).getTime() - new Date(a.meta.date).getTime()
  );

  await fs.writeFile(OUTPUT_FILE, JSON.stringify(articles, null, 2));
  console.log(`✅ Generated index with ${articles.length} articles`);
}

generateIndex().catch(console.error);
```

### package.jsonにスクリプト追加

```json
{
  "scripts": {
    "dev": "vite",
    "build": "node scripts/generate-index.mjs && vite build",
    "preview": "vite preview",
    "generate-index": "node scripts/generate-index.mjs"
  }
}
```

## Cloudflare Pagesへのデプロイ

### なぜCloudflare Pagesか？

| 項目 | Cloudflare Pages | Vercel | Netlify |
| --- | --- | --- | --- |
| 無料枠 | 無制限 | 100GB/月 | 100GB/月 |
| ビルド時間 | 500回/月 | 6000分/月 | 300分/月 |
| CDN | 全世界 | 全世界 | 全世界 |
| 独自ドメイン | 無料 | 無料 | 無料 |

### デプロイ手順

1. **GitHubリポジトリにプッシュ**

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/username/my-blog.git
git push -u origin main
```

2. **Cloudflare Pagesでプロジェクト作成**

- Cloudflare Dashboard → Pages → Create a project
- GitHubを連携
- リポジトリを選択

3. **ビルド設定**

| 項目 | 値 |
| --- | --- |
| Build command | `npm run build` |
| Build output directory | `dist` |
| Node.js version | 18 |

4. **デプロイ開始**

数分でデプロイが完了し、`https://your-blog.pages.dev` でアクセス可能になります。

## GitHub Actionsでの自動デプロイ

`.github/workflows/deploy.yml`:

```yaml
name: Deploy to Cloudflare Pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Build
        run: npm run build

      - name: Deploy to Cloudflare Pages
        uses: cloudflare/pages-action@v1
        with:
          apiToken: ${{ secrets.CLOUDFLARE_API_TOKEN }}
          accountId: ${{ secrets.CLOUDFLARE_ACCOUNT_ID }}
          projectName: my-blog
          directory: dist
```

### シークレットの設定

1. Cloudflare Dashboard → My Profile → API Tokens
2. 「Create Token」→「Edit Cloudflare Pages」テンプレート
3. GitHubリポジトリのSettings → Secrets → 追加

## 独自ドメインの設定

### ドメイン購入

- **Cloudflare Registrar**: 最安値、Cloudflare連携が楽
- **Google Domains**: 使いやすい（※現在はSquarespaceに移行）
- **お名前.com**: 日本語サポート

### DNS設定

```
Type: CNAME
Name: blog
Target: your-blog.pages.dev
```

Cloudflare Pagesの設定画面で「Custom domains」→ドメインを追加

## 運用のヒント

### 画像の最適化

```bash
# ImageMagickで圧縮
find ./public/blog/assets -name "*.jpg" -exec convert {} -quality 80 {} \;

# WebPに変換
find ./public/blog/assets -name "*.jpg" -exec cwebp {} -q 80 -o {}.webp \;
```

### アクセス解析の導入

```html
<!-- Cloudflare Web Analytics（無料） -->
<script 
  defer 
  src='https://static.cloudflareinsights.com/beacon.min.js' 
  data-cf-beacon='{"token": "your-token"}'
></script>
```

### OGP画像の自動生成

<details>
<summary>OGP画像生成スクリプトの例</summary>

```typescript
import { createCanvas, loadImage } from 'canvas';

async function generateOGImage(title: string, outputPath: string) {
  const canvas = createCanvas(1200, 630);
  const ctx = canvas.getContext('2d');

  // 背景
  ctx.fillStyle = '#1a1a2e';
  ctx.fillRect(0, 0, 1200, 630);

  // タイトル
  ctx.fillStyle = '#ffffff';
  ctx.font = 'bold 48px sans-serif';
  ctx.fillText(title, 80, 300, 1040);

  // ファイル出力
  const buffer = canvas.toBuffer('image/png');
  await fs.writeFile(outputPath, buffer);
}
```

</details>

## シリーズのまとめ

全12回のシリーズを完走おめでとうございます！ 🎉

### 学んだこと

| Part | 内容 |
| --- | --- |
| Part 1 (#01-#05) | 面白い記事の書き方 |
| Part 2 (#06-#09) | ブログ運営のテクニック |
| Part 3 (#10-#11) | 自作ブログの構築 |

### これからのステップ

1. **記事を書き続ける** - [継続のコツ](/sample-blog/blog/blog-start-09-consistency.html)を実践
2. **改善を続ける** - デザイン、機能、パフォーマンス
3. **コミュニティに参加** - 仲間を見つける
4. **フィードバックを受ける** - 読者の声を聞く

### 最後のメッセージ

> 「完璧を目指すより、まず公開する」

ブログは**育てるもの**です。最初は粗削りでも、少しずつ改善していけばいい。

大切なのは**始めること**、そして**続けること**。

あなたのブログの成功を心から応援しています！ 🚀

---

**シリーズトップ**: [シリーズ概要と目次](/sample-blog/blog/blog-start-00-introduction.html)

**前回**: [自作ブログ構築（前編）](/sample-blog/blog/blog-start-10-build-blog-part1.html)

