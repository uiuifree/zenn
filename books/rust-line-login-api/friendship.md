---
title: "友達関係"
---

https://developers.line.biz/ja/reference/line-login/#friendship-status


## LINE公式アカウントとの友だち関係を取得する

### 実装
```rust
let Ok(res) = client.friend_ship(&access_token).await else {
    return assert!(false, "friend_ship error");
};
```



### 出力結果

```rust
LineLoginFriendShip { friend_flag: true }
```
