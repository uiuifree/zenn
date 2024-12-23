---
title: "メッセージ配信"
---

https://developers.line.biz/ja/reference/messaging-api/#messages

## 応答メッセージを送る
### 実装
```rust
let client = LineClient::new(line_token);
let mut builder = LineMessagesBuilder::new();
builder.append(LineMessageText::new("Hello, world!"));

let res = client
    .message_send_reply(&builder.to_reply_request(reply_token)).await;

dbg!(res);
```



### 出力結果

```rust
res = Ok(
    LineApiMessageReplyResponse {
        sent_messages: [
            LineApiSendMessage {
                id: "100000000000",
                quote_token: Some(
                    "xxxxxx",
                ),
            },
        ],
    },
)
```
## プッシュメッセージを送る
### 実装
```rust
let client = LineClient::new(line_token);
let mut builder = LineMessagesBuilder::new();
builder.append(LineMessageText::new("Hello, world!"));

let res = client
    .message_send_push(&builder.to_push_request(user_id)).await;

dbg!(res);
```



### 出力結果

```rust
res = Ok(
    LineApiMessagePushResponse {
        sent_messages: [
            LineApiSendMessage {
                id: "100000000000",
                quote_token: Some(
                    "xxxxxx",
                ),
            },
        ],
    },
)

```
## マルチキャストメッセージを送る
### 実装
```rust
let client = LineClient::new(line_token);
let mut builder = LineMessagesBuilder::new();
builder.append(LineMessageText::new("Hello, world!"));

let res = client
    .message_send_multicast(&builder.to_multi_cast_request(vec![user_id.to_string()])).await;

dbg!(res);
```



## ブロードキャストメッセージを送る

### 実装
```rust
let client = LineClient::new(line_token);
let mut builder = LineMessagesBuilder::new();
builder.append(LineMessageText::new("Hello, world!"));

let res = client
    .message_send_broadcast(&builder.to_broad_cast_request()).await;

dbg!(res);
```


