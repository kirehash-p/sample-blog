---
title: "ブログの始め方入門 #10 - 自作ブログ構築（前編）"
date: 2025-11-18
updated: 2025-11-25
tags:
  - サンプルシリーズ
  - ブログ入門
  - 自作ブログ
  - 技術選定
  - React
  - Vite
cover: https://images.unsplash.com/photo-1555066931-4365d14bab8c?w=800
---

# ブログの始め方入門 #10 - 自作ブログ構築（前編）

**前回**: [継続のコツ](/sample-blog/blog/blog-start-09-consistency.html)

---

## いよいよ自作ブログに挑戦！

ここまでで「面白い記事の書き方」と「ブログ運営のテクニック」を学びました。

最後のPart 3では、**自分だけのブログを構築**する方法を解説します。

> ⚠️ **注意**: この記事は技術的な内容を含みます。HTML/CSS/JavaScriptの基礎知識があることを前提としています。

## なぜ自作ブログなのか

### 既存サービスとの比較

| 項目 | 既存サービス | 自作ブログ |
| --- | --- | --- |
| 難易度 | ★☆☆☆☆ | ★★★★☆ |
| カスタマイズ | 制限あり | 無制限 |
| コスト | 無料〜月額1000円 | サーバー代のみ |
| 所有権 | サービスに依存 | 完全に自分のもの |
| 学習効果 | 低い | 高い |

### 自作ブログのメリット

1. **完全なカスタマイズ**: デザインも機能も思いのまま
2. **技術力の証明**: ポートフォリオとして最適
3. **サービス終了リスクなし**: 自分が続ける限り存続
4. **学習効果**: Web技術を実践的に学べる

## 技術選定

### アーキテクチャの選択肢

```
┌────────────────────────────────────────┐
│           ブログのアーキテクチャ          │
├────────────────────────────────────────┤
│                                        │
│  ① SSG (Static Site Generation)        │
│     ├── Astro                          │
│     ├── Next.js (静的エクスポート)       │
│     └── Gatsby                         │
│                                        │
│  ② SPA (Single Page Application)       │
│     ├── React + Vite                   │
│     └── Vue + Vite                     │
│                                        │
│  ③ SSR (Server Side Rendering)         │
│     ├── Next.js                        │
│     └── Nuxt.js                        │
│                                        │
└────────────────────────────────────────┘
```

### おすすめ: SSG（静的サイト生成）

ブログには**SSG**が最適です。理由：

- ⚡ 高速（HTMLが事前生成される）
- 💰 安価（CDNだけで運用可能）
- 🔒 セキュア（サーバーレス）
- 📈 SEOに強い

### このシリーズで使用する技術

| 役割 | 技術 | 理由 |
| --- | --- | --- |
| フレームワーク | React | 最も広く使われている |
| ビルドツール | Vite | 高速、設定簡単 |
| スタイリング | Tailwind CSS | ユーティリティファースト |
| Markdown処理 | unified/remark | 柔軟性が高い |
| ホスティング | Cloudflare Pages | 無料、高速 |

## プロジェクトのセットアップ

### 必要な環境

- **Node.js**: 18.x 以上
- **npm** または **pnpm**
- **Git**

```bash
# バージョン確認
node --version  # v18.x.x 以上
npm --version   # 8.x.x 以上
```

### プロジェクト作成

```bash
# Vite + React + TypeScriptでプロジェクト作成
npm create vite@latest my-blog -- --template react-ts

# ディレクトリに移動
cd my-blog

# 依存関係をインストール
npm install
```

### 追加パッケージのインストール

```bash
# Tailwind CSS
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

# Markdown処理
npm install unified remark-parse remark-rehype rehype-stringify
npm install remark-gfm remark-math rehype-katex
npm install gray-matter

# 型定義
npm install -D @types/node
```

### Tailwind CSSの設定

`tailwind.config.js`:

```javascript
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      typography: {
        DEFAULT: {
          css: {
            maxWidth: '75ch',
          },
        },
      },
    },
  },
  plugins: [
    require('@tailwindcss/typography'),
  ],
}
```

`src/index.css`:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

/* カスタムスタイル */
@layer base {
  html {
    scroll-behavior: smooth;
  }
}
```

## プロジェクト構造

```
my-blog/
├── public/
│   └── blog/           # Markdown記事
│       ├── hello-world.md
│       └── assets/     # 画像など
├── src/
│   ├── components/     # Reactコンポーネント
│   │   ├── ArticleCard.tsx
│   │   ├── ArticleList.tsx
│   │   └── Layout.tsx
│   ├── hooks/          # カスタムフック
│   │   └── useArticle.ts
│   ├── pages/          # ページコンポーネント
│   │   ├── Home.tsx
│   │   └── Article.tsx
│   ├── utils/          # ユーティリティ
│   │   └── markdown.ts
│   ├── App.tsx
│   ├── main.tsx
│   └── index.css
├── package.json
├── tsconfig.json
├── vite.config.ts
└── tailwind.config.js
```

## Markdown処理の実装

### Frontmatterのパース

`src/utils/markdown.ts`:

```typescript
import matter from 'gray-matter';
import { unified } from 'unified';
import remarkParse from 'remark-parse';
import remarkGfm from 'remark-gfm';
import remarkMath from 'remark-math';
import remarkRehype from 'remark-rehype';
import rehypeKatex from 'rehype-katex';
import rehypeStringify from 'rehype-stringify';

interface ArticleMeta {
  title: string;
  date: string;
  updated?: string;
  tags: string[];
  cover?: string;
}

interface Article {
  meta: ArticleMeta;
  content: string;
  html: string;
}

export async function parseMarkdown(markdown: string): Promise<Article> {
  // Frontmatterをパース
  const { data, content } = matter(markdown);
  
  // MarkdownをHTMLに変換
  const result = await unified()
    .use(remarkParse)
    .use(remarkGfm)          // GitHub Flavored Markdown
    .use(remarkMath)         // 数式サポート
    .use(remarkRehype)
    .use(rehypeKatex)        // KaTeX変換
    .use(rehypeStringify)
    .process(content);
  
  return {
    meta: data as ArticleMeta,
    content,
    html: String(result),
  };
}
```

### 記事取得フック

`src/hooks/useArticle.ts`:

```typescript
import { useState, useEffect } from 'react';
import { parseMarkdown } from '../utils/markdown';

export function useArticle(slug: string) {
  const [article, setArticle] = useState<Article | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);

  useEffect(() => {
    async function fetchArticle() {
      try {
        setLoading(true);
        const response = await fetch(`/blog/${slug}.md`);
        
        if (!response.ok) {
          throw new Error('Article not found');
        }
        
        const markdown = await response.text();
        const parsed = await parseMarkdown(markdown);
        setArticle(parsed);
      } catch (e) {
        setError(e as Error);
      } finally {
        setLoading(false);
      }
    }

    fetchArticle();
  }, [slug]);

  return { article, loading, error };
}
```

## 基本コンポーネントの作成

### レイアウトコンポーネント

`src/components/Layout.tsx`:

```tsx
import { ReactNode } from 'react';

interface LayoutProps {
  children: ReactNode;
}

export function Layout({ children }: LayoutProps) {
  return (
    <div className="min-h-screen bg-gray-50 dark:bg-gray-900">
      <header className="bg-white dark:bg-gray-800 shadow">
        <div className="max-w-4xl mx-auto px-4 py-6">
          <h1 className="text-2xl font-bold text-gray-900 dark:text-white">
            My Blog
          </h1>
        </div>
      </header>
      
      <main className="max-w-4xl mx-auto px-4 py-8">
        {children}
      </main>
      
      <footer className="bg-white dark:bg-gray-800 border-t">
        <div className="max-w-4xl mx-auto px-4 py-6 text-center text-gray-600">
          © 2025 My Blog
        </div>
      </footer>
    </div>
  );
}
```

### 記事カードコンポーネント

`src/components/ArticleCard.tsx`:

```tsx
import { Link } from 'react-router-dom';

interface ArticleCardProps {
  slug: string;
  title: string;
  date: string;
  tags: string[];
  cover?: string;
}

export function ArticleCard({ slug, title, date, tags, cover }: ArticleCardProps) {
  return (
    <Link 
      to={`/article/${slug}`}
      className="block bg-white dark:bg-gray-800 rounded-lg shadow-md 
                 hover:shadow-lg transition-shadow overflow-hidden"
    >
      {cover && (
        <img 
          src={cover} 
          alt={title}
          className="w-full h-48 object-cover"
        />
      )}
      
      <div className="p-6">
        <time className="text-sm text-gray-500">{date}</time>
        <h2 className="mt-2 text-xl font-semibold text-gray-900 dark:text-white">
          {title}
        </h2>
        
        <div className="mt-4 flex flex-wrap gap-2">
          {tags.map(tag => (
            <span 
              key={tag}
              className="px-2 py-1 text-xs bg-blue-100 text-blue-800 rounded"
            >
              {tag}
            </span>
          ))}
        </div>
      </div>
    </Link>
  );
}
```

## Viteの設定

`vite.config.ts`:

```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import path from 'path';

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
    },
  },
  // Markdown ファイルをアセットとして扱う
  assetsInclude: ['**/*.md'],
});
```

## 開発サーバーの起動

```bash
npm run dev
```

ブラウザで `http://localhost:5173` を開くと、ブログが表示されます 🎉

## 型定義の追加

`src/types/index.ts`:

```typescript
export interface ArticleMeta {
  title: string;
  date: string;
  updated?: string;
  tags: string[];
  cover?: string;
  description?: string;
}

export interface Article {
  slug: string;
  meta: ArticleMeta;
  content: string;
  html: string;
}

export interface ArticleIndex {
  slug: string;
  meta: ArticleMeta;
}
```

## まとめ

前編では以下を学びました：

| 項目 | 内容 |
| --- | --- |
| 技術選定 | React + Vite + Tailwind |
| プロジェクト構造 | コンポーネント、フック、ユーティリティの分離 |
| Markdown処理 | unified/remark による変換 |
| 基本UI | レイアウト、記事カードの実装 |

後編では、以下を実装します：

- [ ] ルーティングの設定
- [ ] 記事一覧ページ
- [ ] 記事詳細ページ
- [ ] ダークモード対応
- [ ] ビルドとデプロイ

---

**次回**: [自作ブログ構築（後編）- デプロイと運用](/sample-blog/blog/blog-start-11-build-blog-part2.html)

**前回**: [継続のコツ](/sample-blog/blog/blog-start-09-consistency.html)

