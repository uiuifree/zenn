---
title: "リッチメニュー"
---

https://developers.line.biz/ja/reference/messaging-api/#rich-menu

## リッチメニューを作成する

### 実装
```rust
    let client = LineClient::new(line_token);
    let rich_menu_json = json!({
        "size": {
          "width": 2500,
          "height": 1686
        },
        "selected": false,
        "name": "Nice rich menu",
        "chatBarText": "Tap to open",
        "areas": [
          {
            "bounds": {
              "x": 0,
              "y": 0,
              "width": 2500,
              "height": 1686
            },
            "action": {
              "type": "postback",
              "data": "action=buy&itemid=123"
            }
          }
       ]
    });


    let res = client.rich_menu_create(rich_menu_json).await.unwrap();
    dbg!(res);
```



### 出力結果

```json
res = LineApiRichMenuCreateResponse {
  rich_menu_id: "richmenu-xxxxxxx",
}
```



## リッチメニューオブジェクトを検証する


### 実装
```rust
let client = LineClient::new(line_token);
let rich_menu_json = json!({
    "size": {
      "width": 2500,
      "height": 1686
    },
    "selected": false,
    "name": "Nice rich menu",
    "chatBarText": "Tap to open",
    "areas": [
      {
        "bounds": {
          "x": 0,
          "y": 0,
          "width": 2500,
          "height": 1686
        },
        "action": {
          "type": "postback",
          "data": "action=buy&itemid=123"
        }
      }
   ]
});


let res = client.rich_menu_validate_object(rich_menu_json).await.unwrap();
dbg!(res);
```



### 出力結果

```json
LineApiRichMenuValidateObjectResponse

```

## リッチメニューの画像をアップロードする

### 実装
```rust
    let rich_menu_id = "richmenu-xxxx";
    let file =
        std::fs::read("./test_line.jpg")
            .unwrap();
    let res = client
        .rich_menu_content_upload(rich_menu_id, file)
        .await;

    dbg!(res);
```



### 出力結果

```json
res = Ok(
    Object {},
)
```

## リッチメニューの画像をダウンロードする

### 実装
```rust
let rich_menu_id = "richmenu-xxxx";
let res = client
    .rich_menu_content_download(rich_menu_id)
    .await;

// 保存
let mut file = std::fs::File::create("./test_download.jpg").unwrap();
file.write(&content).unwrap();
file.flush().unwrap();


dbg!(res);
```



### 出力結果

```json
res = Ok(
    [
        255,
      ...............
    ]
```

## リッチメニューの配列を取得する

### 実装
```rust

let client = LineClient::new(line_token);
let res = client
    .rich_menu_list()
    .await;

dbg!(res);
```



### 出力結果

```rust
res = Ok(
LineApiRichMenuListResponse {
  rich_menus: []
})    
```

## リッチメニューを取得する

### 実装
```rust
let client = LineClient::new(line_token);
let rich_menu_id = "richmenu-xxxx";
let res = client
    .rich_menu_get(rich_menu_id)
    .await;

dbg!(res);
```



### 出力結果

```json
res = Ok(
    LineApiRichMenuGetResponse {
  rich_menu: RichMenu {
  rich_menu_id: "richmenu-25687fac187a7992ded6659980e2a4c5",
  .....
}
})
```

## リッチメニューを削除する

### 実装
```rust
let client = LineClient::new(line_token);
let rich_menu_id = "richmenu-xxxx";
let res = client
    .rich_menu_delete(rich_menu_id)
    .await;

dbg!(res);
```



### 出力結果

```json
res = Ok(
    LineApiRichMenuDeleteResponse,
)

```

## デフォルトのリッチメニューを設定する

### 実装
```rust

let client = LineClient::new(line_token);
let rich_menu_id = "richmenu-xxxx";
let res = client
    .rich_menu_set_default_menu(rich_menu_id)
    .await;

dbg!(res);
```

### 出力結果

```json
res = Ok(
    LineApiRichMenuSetDefaultResponse,
)

```


## デフォルトのリッチメニューのIDを取得する

### 実装
```rust
let client = LineClient::new(line_token);
let res = client
    .rich_menu_get_default_menu_id()
    .await;

dbg!(res);
```



### 出力結果

```json
res = Ok(
    LineApiRichMenuGetDefaultResponse {
        rich_menu_id: "richmenu-xxxx",
    },
)
```


## デフォルトのリッチメニューを解除する

### 実装
```rust
let client = LineClient::new(line_token);
let res = client
    .rich_menu_delete_default_menu()
    .await;

dbg!(res);

```



### 出力結果

```json
res = Ok(
    LineApiRichMenuDeleteDefaultResponse,
)

```

