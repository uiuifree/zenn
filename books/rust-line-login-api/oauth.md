---
title: "OAuth"
---

https://developers.line.biz/ja/reference/line-login/#profile



## アクセストークンを発行する
> アクセストークンを発行します

### 実装
```rust
let code = "xxxxxxxx";
let redirect_uri = "https://example.com/line/connect";
let client = client();
let Ok(res) = client.create_token(code, redirect_uri).await else {
    assert!(false, "create_token error");
    return;
};

dbg!(res);

```



### 出力結果
| 項目      |説明|
|---------|-------------------|
| access_token     | アクセストークン |
| expires_in    | アクセストークンの有効期限が切れるまでの秒数 |
| id_token | ユーザー情報を含むJSONウェブトークン（JWT） |
| refresh_token | 新しいアクセストークンを取得するためのトークン（リフレッシュトークン） |
| scope | アクセストークンに付与されている権限 |
| token_type | Bearer |


```rust
res = LineLoginCreateTokenResponse {
    access_token: "xxxx",
    expires_in: 2592000,
    id_token: "yyyy",
    refresh_token: "zzzz",
    scope: "openid profile",
    token_type: "Bearer",
}
```

## アクセストークンの有効性を検証する
> アクセストークンの有効性を検証します。
### 実装
```rust
let Ok(res) = client.token_verify(&access_token).await else {
    return assert!(false, "token_verify error");
};
dbg!(res);
```



### 出力結果
| 項目      |説明|
|---------|-------------------|
| scope | アクセストークンに付与されている権限 |
| client_id | アクセストークンが発行されたチャネルID|
| expires_in | アクセストークンの有効期限が切れるまでの秒数

```rust
res = LineLoginTokenVerifyResponse {
    scope: "profile openid",
    client_id: "00000000",
    expires_in: 2591911,
}
```

## アクセストークンを更新する
> リフレッシュトークンを使って新しいアクセストークンを取得できます。
### 実装
```rust
let Ok(res) = client.update_access_token(&refresh_token).await else {
    return assert!(false, "update_access_token error");
};
dbg!(res);
```



### 出力結果
| 項目      |説明|
|---------|-------------------|
| access_token     | アクセストークン |
| expires_in    | アクセストークンの有効期限が切れるまでの秒数 |
| refresh_token | 新しいアクセストークンを取得するためのトークン（リフレッシュトークン） |
| scope | アクセストークンに付与されている権限 |
| token_type | Bearer |


```rust
res = LineLoginUpdateAccessTokenResponse {
    token_type: "Bearer",
    access_token: "xxxxxxxxxxxx",
    refresh_token: "yyyyyyyyyyyy",
    expires_in: 2592000,
    scope: "profile openid",
}
```

## アクセストークンを取り消す
> ユーザーのアクセストークンを無効にします。

### 実装
```rust
let Ok(res) = client.revoke_access_token(access_token).await else {
     return assert!(false, "revoke_access_token error");
};
dbg!(res);
```



### 出力結果
> ステータスコード200と空のレスポンスボディを返します。
```rust
()
```


## IDトークンを検証する
> 受信したIDトークンが正規のものであることを確認し、ユーザーのプロフィール情報とメールアドレスを取得します。
### 実装
```rust
let Ok(res) = client.id_token_verify(id_token, None, None).await else {
    return assert!(false, "update_access_token error");
};
dbg!(res);
```



### 出力結果
| 項目      |説明|
|---------|-------------------|
| iss     | IDトークンの生成URL |
| sub     | IDトークンの対象ユーザーID |
| aud     | チャネルID |
| exp     | Dトークンの有効期限。UNIX時間（秒）で返されます。 |
| iat    | IDトークンの生成時間。UNIX時間（秒）で返されます。 |
| auth_time    | ユーザー認証時間。UNIX時間（秒）で返されます。 |
| nonce    | 認可URLに指定したnonceの値 |
| amr    | ユーザーが使用した認証方法のリスト。 |
| name    | ユーザーの表示名 |
| picture    | ユーザープロフィールの画像URL |
| email    | ユーザーのメールアドレス |


```rust
res = LineLoginIdTokenVerifyResponse {
    iss: "https://access.line.me",
    sub: "Ufxxx",
    aud: "160000000",
    exp: 1734955133,
    iat: 1734951533,
    auth_time: None,
    nonce: None,
    amr: Some(
        [
            "linesso",
        ],
    ),
    name: Some(
        "Line Login API",
    ),
    picture: Some(
        "https://profile.line-scdn.net/xxxx",
    ),
    email: None,
}
```

## ユーザー情報を取得する
> ユーザーのユーザーID、表示名、プロフィール画像を取得します。「ユーザープロフィールを取得する」エンドポイントとは、アクセストークンに必要なスコープが異なります。

### 実装
```rust
let Ok(res) = client.user_info(&access_token).await else {
    return assert!(false, "user_info error");
};
dbg!(res);
```



### 出力結果

| 項目      |説明|
|---------|-------------------|
| sub     | ユーザーID |
| name    | ユーザー名 |
| picture | ユーザーのプロフィール画像のURL |




```rust
res = LineLoginUserInfoResponse {
    sub: "Ufxxxxxxx",
    name: Some(
        "Line Login API",
    ),
    picture: Some(
        "https://profile.line-scdn.net/xxxxxxxxxxxxxx",
    ),
}
```

