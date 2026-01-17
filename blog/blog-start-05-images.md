---
title: "ブログの始め方入門 #05 - 画像の活用法"
date: 2025-09-09
updated: 2025-09-15
tags:
  - サンプルシリーズ
  - ブログ入門
  - 画像
  - ビジュアル
cover: https://images.unsplash.com/photo-1516035069371-29a1b244cc32?w=800
---

# ブログの始め方入門 #05 - 画像の活用法

**前回**: [書式テクニック](/sample-blog/blog/blog-start-04-formatting.html)

---

## 画像が記事の価値を高める

> 「百聞は一見にしかず」

この言葉はブログでも真実です。適切な画像は：

- 読者の注目を引く
- 複雑な概念を視覚的に説明する
- 記事の滞在時間を延ばす
- SNSでシェアされやすくなる

## 画像の基本的な挿入方法

### Markdown記法

```text
![代替テキスト](https://example.com/image.png)
```

**代替テキスト**（alt属性）は重要です：
- 画像が表示されないときに表示される
- スクリーンリーダーで読み上げられる
- SEOに影響する

### 実際の例

![タイピングする手元の写真](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e1/Typing-computer-keyboard.jpg/1200px-Typing-computer-keyboard.jpg)

## 画像サイズとレイアウト

### サイズの考慮

| 用途 | 推奨幅 | ファイルサイズ |
| --- | --- | --- |
| カバー画像 | 1200px | 200KB以下 |
| 本文中の画像 | 800px | 150KB以下 |
| サムネイル | 400px | 50KB以下 |

$$
\text{読み込み時間} \propto \text{ファイルサイズ}
$$

大きすぎる画像は読み込みを遅くし、読者の離脱を招きます。

### HTMLでのサイズ指定

Markdownだけではサイズ指定が難しいため、HTMLを使うこともあります：

```html
<img src="画像URL" alt="説明" width="600">
```

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3f/Placeholder_view_vector.svg/600px-Placeholder_view_vector.svg.png" alt="プレースホルダー画像" width="400">

### レイアウトのバリエーション

**中央配置**:
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3f/Placeholder_view_vector.svg/600px-Placeholder_view_vector.svg.png" alt="中央配置の画像" style="display: block; margin: 0 auto; width: 300px;">

**横並び**:
<div style="display: flex; gap: 10px; flex-wrap: wrap;">
  <img src="https://placehold.co/200x150/png" alt="画像1" style="flex: 1; min-width: 150px;">
  <img src="https://placehold.co/200x150/png" alt="画像2" style="flex: 1; min-width: 150px;">
  <img src="https://placehold.co/200x150/png" alt="画像3" style="flex: 1; min-width: 150px;">
</div>

## フリー画像の入手先

### おすすめのフリー素材サイト

1. **Unsplash** - 高品質な写真
2. **Pexels** - 写真とビデオ
3. **Pixabay** - 写真、イラスト、ベクター
4. **Wikimedia Commons** - パブリックドメイン画像

### ライセンスの確認

| ライセンス | 商用利用 | クレジット表記 |
| --- | --- | --- |
| CC0 | ◎ | 不要 |
| CC BY | ◎ | 必要 |
| CC BY-SA | ◎ | 必要 + 同条件 |
| CC BY-NC | × | 必要 |

> ⚠️ **注意**: ライセンスは必ず確認してください。著作権侵害は深刻な問題です。

### Wikimedia Commonsの活用

Wikipedia関連のプロジェクトで使われている画像は、多くがフリーで使えます。

![地球の写真（NASA撮影）](https://upload.wikimedia.org/wikipedia/commons/thumb/c/cb/The_Blue_Marble_%28remastered%29.jpg/600px-The_Blue_Marble_%28remastered%29.jpg)

*出典: NASA, Public Domain*

## スクリーンショットの撮り方

技術系ブログでは、スクリーンショットが必須です。

### OS別のショートカット

| OS | 全画面 | 範囲選択 |
| --- | --- | --- |
| Windows | <kbd>Win</kbd>+<kbd>PrintScreen</kbd> | <kbd>Win</kbd>+<kbd>Shift</kbd>+<kbd>S</kbd> |
| macOS | <kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>3</kbd> | <kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>4</kbd> |
| Linux | <kbd>PrintScreen</kbd> | <kbd>Shift</kbd>+<kbd>PrintScreen</kbd> |

### スクリーンショットのベストプラクティス

- [x] 不要な情報を切り取る
- [x] 注目してほしい部分をハイライト
- [x] 個人情報を隠す
- [x] 適切なサイズに圧縮

<details>
<summary>おすすめのスクリーンショットツール</summary>

**無料ツール**:
- **Snipping Tool** (Windows) - 標準搭載
- **Screenshot.app** (macOS) - 標準搭載
- **Flameshot** (Linux) - 高機能フリーソフト

**有料ツール**:
- **CleanShot X** (macOS) - プロ向け機能
- **ScreenPal** - 動画も撮れる

</details>

## 図解の作成

### ツールの選択

| ツール | 特徴 | 価格 |
| --- | --- | --- |
| Excalidraw | 手書き風、軽量 | 無料 |
| draw.io | 多機能、無料 | 無料 |
| Figma | プロ向け、共同編集 | 無料〜 |
| Canva | テンプレート豊富 | 無料〜 |

### 図解のポイント

1. **シンプルに**: 1つの図に1つのメッセージ
2. **色は3色まで**: 多すぎると見にくい
3. **矢印を活用**: 流れを示す
4. **余白を確保**: 詰め込みすぎない

### 例：フローチャート

```
┌─────────┐     ┌─────────┐     ┌─────────┐
│ 記事を  │ ──▶ │ 画像を  │ ──▶ │ 公開    │
│ 書く    │     │ 追加    │     │ する    │
└─────────┘     └─────────┘     └─────────┘
```

## 画像の最適化

### なぜ最適化が必要か

Webサイトの表示速度は、ユーザー体験とSEOに直結します。

> Google によると、ページの読み込みが3秒を超えると53%のユーザーが離脱します。[^1]

### 画像形式の選択

| 形式 | 特徴 | 用途 |
| --- | --- | --- |
| JPEG | 写真向け、圧縮率高い | 写真 |
| PNG | 透過対応、可逆圧縮 | スクリーンショット |
| WebP | 高圧縮、モダン | すべて（推奨） |
| SVG | ベクター、拡大劣化なし | アイコン、ロゴ |

### 圧縮ツール

**オンラインツール**:
- TinyPNG (https://tinypng.com/)
- Squoosh (https://squoosh.app/)

**コマンドライン**:
```bash
# ImageMagickで圧縮
convert input.jpg -quality 80 output.jpg

# WebPに変換
cwebp input.png -q 80 -o output.webp
```

[^1]: Google Research, "The Need for Mobile Speed" (2017)

## アクセシビリティへの配慮

### alt属性の書き方

**悪い例**:
- `![image1](photo.jpg)` → 意味のない名前
- `![](photo.jpg)` → altが空

**良い例**:
- `![夕焼けに染まる海岸線の写真](sunset.jpg)` → 具体的な説明

### 色覚多様性への配慮

赤と緑だけで情報を区別しないでください。約8%の男性が色覚異常を持っています。

```
✅ 色 + 形 + テキストで区別
❌ 色だけで区別
```

## 画像管理のヒント

### フォルダ構成の例

```
blog/
├── posts/
│   ├── 2025-01-article/
│   │   ├── index.md
│   │   └── images/
│   │       ├── cover.jpg
│   │       ├── figure-01.png
│   │       └── screenshot-01.png
```

### 命名規則

```
❌ IMG_20250101_123456.jpg
❌ スクリーンショット 2025-01-01 12.34.56.png

✅ cover-blog-intro.jpg
✅ figure-01-architecture.png
✅ screenshot-vscode-settings.png
```

## まとめ

画像活用のポイント：

1. **適切なサイズ**で最適化する
2. **alt属性**を必ず書く
3. **ライセンス**を確認する
4. **図解**で複雑な概念を視覚化
5. **アクセシビリティ**に配慮する

画像は記事の価値を大きく高めます。しかし、**必要以上に使わない**ことも大切です。テキストで十分な箇所に画像を入れると、かえって読みにくくなります。

次回は、技術ブログの要である「コードブロック」の活用法を解説します 💻

---

**次回**: [コードブロックの活用 - 技術記事の書き方](/sample-blog/blog/blog-start-06-code-blocks.html)

**前回**: [書式テクニック](/sample-blog/blog/blog-start-04-formatting.html)

