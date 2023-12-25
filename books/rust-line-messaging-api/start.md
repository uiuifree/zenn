---
title: "LINE Messaging APIをRustで使うために"
---


# はじめに
この本ではLINE Messaging APIを使うためのライブラリ「[line-bot-messaging-api](https://github.com/uiuifree/rust-line-messaging-api)」の使い方を紹介していきます。

社内展開ためのドキュメントくらいの立ち位置です、ベース作ってから順次改善していきます。


# Cargo.tomlの設定
```toml title:cargo.toml
[dependencies]
line-bot-messaging-api = "0.1"

serde = { version = "~1" }
serde_json = "~1"
serde_derive = "~1"
```


# LINE Messaging APIのクライアント作成

```rust
use line_bot_messaging_api::LineClient;

let line_token = "LINE TOKEN";
let clinet= LineClient::new(line_token);
```



#　目次

1. ボット
2. リッチメニューの設定（共通）
2. リッチメニューの設定（個人）
3. メッセージ配信

[//]: # (4. MessageBuilderの使い方)

[//]: # (6. ユーザー情報の取得)

[//]: # (5. 集計)

[//]: # (5. オーディエンス管理)

[//]: # (5. グループトーク)

[//]: # (5. 複数人トーク)

[//]: # (5. リッチメニューエイリアス)
