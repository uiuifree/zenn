---
title: "ボット情報"
---

## ボットの情報を取得する

https://developers.line.biz/ja/reference/messaging-api/#get-bot-info



### 実装
```rust
let res = client.bot_info().await.unwrap();
dbg!(res);
```



### 出力結果

```rust
res = LineApiBotInfoResponse {
  user_id: "Ufxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  basic_id: "@xxx",
  premium_id: None,
  display_name: Some(
  "dev_LINE BOT",
  ),
  picture_url: Some(
  "https://profile.line-scdn.net/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  ),
  chat_mode: "chat",
  mark_as_read_mode: "manual",
}
```
