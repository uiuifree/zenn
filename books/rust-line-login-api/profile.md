---
title: "プロフィール"
---

https://developers.line.biz/ja/reference/line-login/#profile


## ユーザープロフィールを取得する

### 実装
```rust
let Ok(res) = client.profile(&access_token).await else {
return assert!(false, "profile error");
};
println!("{:?}", res);
```



### 出力結果

```rust
res = LineLoginProfileResponse {
    user_id: "Ufxxxxxxxxxxxxxxxx",
    display_name: "Line Login API",
    picture_url: Some(
        "https://profile.line-scdn.net/xxxxxxxxxx",
    ),
    status_message: Some(
        "プロフィールメッセージ！",
    ),
}
```
