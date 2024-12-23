---
title: "LINEログイン APIをRustで使うために"
---


# はじめに
この本ではLINEログインAPIを使うためのライブラリ「[line-login-api](https://github.com/uiuifree/rust-line-login-api)」の使い方を紹介していきます。



# インストール方法
Cargo.tomlの設定
```toml title:cargo.toml
[dependencies]
line-login-api = "0.1"

serde = { version = "~1" }
serde_json = "~1"
serde_derive = "~1"
```


# LINEログインAPIのクライアント作成

```rust
use line_login_api::LineLoginClient;

let client = LineLoginClient::new("LINE_CLIENT_ID", "LINE_CLIENT_SECRET");
```


# 目次

1. [OAuth](oauth)
2. [プロフィール](profile)
3. [友達関係](friendship)
