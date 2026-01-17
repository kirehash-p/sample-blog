---
title: 描画確認用の記事テスト
date: 2024-06-01
updated: 2024-06-18
tags:
  - test
  - markdown
  - sample
  - ui
cover: /sample-blog/blog/assets/cover-sample--76e6285000.jpg
---

# 見出しレベル1
本文サンプル: 日本語とEnglish / 1234567890 / !?()[]{}<>.

## 見出しレベル2
**太字** / *斜体* / ~~打ち消し~~ / `inline code`

### 見出しレベル3
- リストA
- リストB
- リストC

#### 見出しレベル4
1. 番号付き1
2. 番号付き2
3. 番号付き3

##### 見出しレベル5
> 引用ブロックの表示

###### 見出しレベル6
---

## テーブル
| 項目 | 値 | 備考 |
| --- | --- | --- |
| Alpha | 123 | メモ |
| Beta | 456 | メモ |
| Gamma | 789 | メモ |

## とても長い見出し名のテスト: 日本語の長い見出しとEnglishVeryLongHeaderNameWithoutSpacesが混在した場合の表示確認用
長い見出しの折り返しや行間を確認します。

### 長いテーブル
| ID | タイトル | 状態 | 優先度 | 担当 | 期限 | メモ |
| --- | --- | --- | --- | --- | --- | --- |
| 001 | 長いタイトルのサンプルA | Open | High | Alice | 2024-06-01 | 文章が長い場合の折り返し確認 |
| 002 | 長いタイトルのサンプルB | In Progress | Medium | Bob | 2024-06-02 | テーブルのセル内の折り返し確認 |
| 003 | 長いタイトルのサンプルC | Done | Low | Carol | 2024-06-03 | 行の高さと揃いの確認 |
| 004 | 長いタイトルのサンプルD | Open | High | Dave | 2024-06-04 | URL https://example.com/path/to/resource |
| 005 | 長いタイトルのサンプルE | In Progress | Medium | Erin | 2024-06-05 | 記号 !?()[]{}<> の表示確認 |
| 006 | 長いタイトルのサンプルF | Done | Low | Frank | 2024-06-06 | 日本語の長文も混ぜて確認します |
| 007 | Long title sample G | Open | High | Grace | 2024-06-07 | English mixed content sample for width |
| 008 | Long title sample H | In Progress | Medium | Heidi | 2024-06-08 | 文字数が多い場合の可読性 |
| 009 | Long title sample I | Done | Low | Ivan | 2024-06-09 | 余白の確認 |
| 010 | Long title sample J | Open | High | Judy | 2024-06-10 | 最終行のボーダー表示確認 |

### 超長いヘッダーのテーブル
| 極端に長い列名のサンプル_その1_とても長い日本語の説明が続く列 | 極端に長い列名のサンプル_その2_EnglishVeryLongHeaderNameWithNoSpaces | 極端に長い列名のサンプル_その3_数字1234567890を含む長い名前 | 極端に長い列名のサンプル_その4_ハイフンや記号-_-_を含む列名 | 極端に長い列名のサンプル_その5_URLを含むhttps://example.com/super/long/header |
| --- | --- | --- | --- | --- |
| A1 | 値1 | 値2 | 値3 | 値4 |
| A2 | 値1 | 値2 | 値3 | 値4 |

## チェックリスト
- [ ] 未完了
- [x] 完了
- [ ] 未完了

## コードブロック
```ts
export const demo = (value: number) => {
  return value * 2;
};
```

### 複雑なコードブロック
```ts
type User = {
  id: string;
  name: string;
  tags: string[];
  meta?: Record<string, unknown>;
};

const users: User[] = [
  { id: 'u1', name: 'Alice', tags: ['alpha', 'beta'], meta: { active: true } },
  { id: 'u2', name: 'Bob', tags: ['gamma'], meta: { active: false, note: 'long note here' } }
];

const groupBy = <T, K extends string | number>(items: T[], key: (item: T) => K) => {
  return items.reduce<Record<K, T[]>>((acc, item) => {
    const k = key(item);
    if (!acc[k]) acc[k] = [];
    acc[k].push(item);
    return acc;
  }, {} as Record<K, T[]>);
};

const grouped = groupBy(users, (user) => user.tags[0] ?? 'none');
console.log(JSON.stringify(grouped, null, 2));
const longLine =
  "This is a deliberately long line to test horizontal scrolling in code blocks with mixed characters 1234567890 !@#$%^&*() [] {} <> / ? = + - _ and some 日本語 mixed in for overflow checks.ああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああ";
```

### 複雑なコードブロック（JSON）
```json
{
  "id": "post-123",
  "title": "Complex Payload",
  "stats": {
    "views": 12345,
    "likes": 678,
    "ratios": [0.1, 0.2, 0.7]
  },
  "tags": ["alpha", "beta", "gamma"],
  "meta": {
    "author": "User A",
    "flags": ["featured", "archived"]
  }
}
```

## 画像とリンク
![図のサンプル](https://placehold.co/800x400/png)

[外部リンクの表示](https://example.com)

### 画像サイズ違い
![小](https://placehold.co/200x120/png)
![中](https://placehold.co/400x240/png)
![大](https://placehold.co/1000x560/png)

### 複数画像の並び
![列1](https://placehold.co/320x180/png)
![列2](https://placehold.co/320x180/png)
![列3](https://placehold.co/320x180/png)

## 引用の連続
> 引用1: 長めの文章が続きます。レイアウトと行間の確認用。
>
> 引用2: 連続した引用ブロックの間隔を確認します。
>
> 引用3: 強調やリンクを混ぜます。[リンク](https://example.com)

### 引用内の複雑な書式
> **太字** / *斜体* / ~~打ち消し~~ / `inline code`
>
> - 引用内リストA
> - 引用内リストB
>
> 1. 引用内番号付き1
> 2. 引用内番号付き2
>
> `コード` と [リンク](https://example.com) と ![画像](https://placehold.co/240x120/png) を混在。

## 脚注
脚注のテストです。[^ref1] さらに別の脚注です。[^ref2]

[^ref1]: 脚注1の本文です。
[^ref2]: 脚注2の本文です。

## 重複見出し
同名の見出しテストその1です。

## 重複見出し
同名の見出しテストその2です。

## details/summary
<details>
  <summary>クリックで展開する詳細</summary>
  <p>詳細コンテンツの表示確認です。</p>
  <ul>
    <li>詳細内リスト1</li>
    <li>詳細内リスト2</li>
  </ul>
</details>

## キーボード表記とマーク
<kbd>Cmd</kbd> + <kbd>K</kbd> / <mark>ハイライト</mark> / <small>small text</small>

## 定義リスト
用語A
: 用語Aの説明です。

用語B
: 用語Bの説明です。

## レイアウト確認用の短文
短い行。

やや長い行のサンプルです。行の折り返し、字間、行間を確認します。

とても長い行のサンプルです。とても長い行のサンプルです。とても長い行のサンプルです。とても長い行のサンプルです。とても長い行のサンプルです。

## KaTeX
インライン: $E=mc^2$ と $a^2+b^2=c^2$。

ブロック:
$$
\int_0^\infty e^{-x^2} \, dx = \frac{\sqrt{\pi}}{2}
$$

## 長いURLと改行
https://example.com/this/is/a/very/long/url/with/many/segments/and-parameters?alpha=123&beta=456&gamma=789&delta=longlonglongstring

手動改行テスト: 行末にスペースを2つ置くと改行されます。  
この行は改行後に続きます。

## ネスト引用
> 第一階層の引用です。
>
> > 第二階層の引用です。
> >
> > > 第三階層の引用です。

## 水平線と区切り
---

***

## Emojiと記号
😀 😺 🚀 ✨ ✅ ⚠️
記号: © ® ™ § ¶ ★ ☆ ◆ ◇ → ← ↑ ↓

## 画像の比率差
![横長](https://placehold.co/1000x300/png)
![縦長](https://placehold.co/300x800/png)

## 斜体+太字+コードの混在
***太字斜体*** / **太字** / *斜体* / `inline` / **`太字コード`**

## 複数言語混在
English, 日本語, 한국어, 中文, русский, العربية

## 画像レイアウト（HTML + style）
<!-- 横幅に合わせて拡大 -->
<img src="https://placehold.co/640x360/png" alt="full width sample" style="width: 100%; display: block;">

<!-- 中央配置 -->
<img src="https://placehold.co/320x200/png" alt="center image" style="width: 320px; max-width: 100%; display: block; margin: 0 auto;">

<!-- 左寄せ -->
<img src="https://placehold.co/320x200/png" alt="left image" style="width: 320px; max-width: 100%; display: block; margin-right: auto;">

<!-- 右寄せ -->
<img  src="https://placehold.co/320x200/png" alt="right image" style="width: 320px; max-width: 100%; display: block; margin-left: auto;">

<!-- 複数画像の横並び -->
<div style="display: flex; gap: 12px; flex-wrap: wrap;">
  <img src="https://placehold.co/300x200/png" alt="row image 1" style="flex: 1 1 200px;">
  <img src="https://placehold.co/300x200/png" alt="row image 2" style="flex: 1 1 200px;">
  <img src="https://placehold.co/300x200/png" alt="row image 3" style="flex: 1 1 200px;">
</div>

## 別記事リンクのテスト
記事一覧: [Blog一覧](../blog)

自分自身：[ArticleTest](/sample-blog/blog/ArticleTest.html)

内部記事:
- [ブログ入門00](/sample-blog/blog/blog-start-00-introduction.html)
- [ブログ入門01](/sample-blog/blog/blog-start-01-theme-selection.html)
- [サブフォルダ内記事テスト](/sample-blog/blog/サブフォルダ内記事テスト.html)

見出しリンク（Markdown形式）:
- [ブログ入門00の見出し](/sample-blog/blog/blog-start-00-introduction.html#シリーズ目次)
- [ブログ入門01の見出し](/sample-blog/blog/blog-start-01-theme-selection.html#テーマ選びの3つの原則)

見出しリンク（Wikiリンク形式）:
- [blog-start-00-introduction](/sample-blog/blog/blog-start-00-introduction.html#シリーズ目次)
- [テーマ選びの原則へ](/sample-blog/blog/blog-start-01-theme-selection.html#テーマ選びの3つの原則)

エイリアス:
- [シリーズ概要へのリンク](/sample-blog/blog/blog-start-00-introduction.html)
- [blog-start-00-introduction](/sample-blog/blog/blog-start-00-introduction.html)

