# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要
Zenn公開記事・書籍の管理リポジトリ。zenn-cliを使用してMarkdown形式で記事(articles)と書籍(books)を管理。

## 主要コマンド

### プレビュー
```bash
npx zenn preview
```
ブラウザでコンテンツをプレビュー

### 新規作成
```bash
npx zenn new:article    # 新しい記事を作成
npx zenn new:book       # 新しい本を作成
```

### 一覧表示
```bash
npx zenn list:articles  # 記事の一覧
npx zenn list:books     # 本の一覧
```

## コンテンツ構造

### 記事 (articles/)
- ファイル名: `{slug}.md` (12文字のランダム文字列)
- フロントマター必須項目:
  ```yaml
  ---
  title: "記事タイトル"
  emoji: "😸"
  type: "tech" # tech: 技術記事 / idea: アイデア
  topics: ["rust", "php"]
  published: true
  ---
  ```

### 書籍 (books/)
- ディレクトリ構造: `books/{book-slug}/`
- `config.yaml`: 書籍のメタデータ
  ```yaml
  title: "書籍タイトル"
  summary: "概要"
  topics: []
  published: true
  price: 0  # 有料の場合200〜5000
  chapters:
    - chapter1
    - chapter2
  ```
- チャプター: `{chapter-name}.md`

## 注意事項
- zenn-cliのバージョンは0.1.146と古い。最新版へのアップデート推奨
- 記事・書籍の新規作成にはzenn-cliのコマンドを使用（手動ファイル作成も可能）
- GitHubリポジトリ: https://github.com/uiuifree/zenn

## 参考URL
- Zenn CLIガイド: https://zenn.dev/zenn/articles/zenn-cli-guide
