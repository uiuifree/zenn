---
title: "LINE Messaging APIをRustで使うために"
---


# はじめに
この本ではLINE Messaging APIを使うためのライブラリ「[line-bot-messaging-api](https://github.com/uiuifree/rust-line-messaging-api)」の使い方を紹介していきます。

# Cargo.tomlの設定
```toml
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
