---
title: "ActixWebで開発"
---

## 選定フレームワーク

弊社のプロジェクトでは `Actix-Web`を採用しています。

理由としては
1. ドキュメントやWEB開発で必要な基本的機能が一通り揃っていること
2. フレームワークの固有機能が少ないこと
3. [Web Framework Benchmarks](https://www.techempower.com/benchmarks/#section=data-r21&hw=ph&test=composite)でのスコアが上位であったこと
![](https://storage.googleapis.com/zenn-user-upload/22a8ae1fe5cc-20231105.png)

Round21での各言語の主要フレームワークのベンチマークを確認すると他言語のフレームワークとは2~3倍以上のパフォーマンス差があることが確認することができます。
   
| フレームワーク | スコア|
| --- | --- |
| Actix(Rust) | 7,667 |
| axum(Rust)  | 6,982 | 
| Ktor(Kotlin) | 2,435 | 
| gin (Go) | 1,943 |
| spring(Java) | 1,846 | 
| Laravel(PHP) | 371 | 



Rustでのフレームワークを調べたことがあると他にも 「Rocket」「axum」などが有名で記事などがよくヒットしますが、
* 権限設定
* ルーティング設定
* 状態管理(Context)
* ログ出力
* Httpレスポンス関連

などの検証が問題なく済んだため、ActixWebが採用されました。


## ActixWebを動かしてみる

[ActixWeb](https://github.com/actix/actix-web)のサンプルになりますが、下記のコードのみで動作確認ができます。
特に難しいものではありませんが、以前のプロジェクトではLaravelを採用していたため初期レスポンスの速度差がこれだけで感じることができ感動します。


```rust
# Cargo.toml
[dependencies]
actix-web = "4"
```

```rust 
# /src/bin/web_server.rs
use actix_web::{get, web, App, HttpServer, Responder};

#[get("/hello/{name}")]
async fn greet(name: web::Path<String>) -> impl Responder {
    format!("Hello {name}!")
}

#[actix_web::main]
async fn main() -> std::io::Result<()> {
    HttpServer::new(|| {
        App::new().service(greet)
    })
    .bind(("127.0.0.1", 8080))?
    .run()
    .await
}
```

``` 
# ディレクトリ構成
└ /src
　└ lib.rs
　└ /bin
    └ web_server.rs
└ cargo.toml
```
