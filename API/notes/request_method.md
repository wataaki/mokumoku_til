# HTTP メソッド
GET/POST との関係性は大事
URIとメソッドの関係は、操作するものと操作方法の関係

|メソッド|説明|
|-|-|
|GET|リソースの取得|
|POST|リソースの新規登録|
|PUT|既存リソースの更新|
|DELETE|リソースの削除|
|PATCH|リソースの一部変更|
|HEAD|リソースのメタ情報の取得|

## GET メソッド
  - URI で指定したリソースを取得する
  - サーバ上のリソースが変更されることはない

## POST メソッド
  - URI に新しいリソースを送信する
  - サーバ上のリソースが変更される

## PUT メソッド
  - URI で指定したリソースを置き換えする
  - URI で指定したリソースが存在しない場合、新しく作成することも可能 (非推奨)

## DELETE メソッド
  - URI のリソースを削除する

## PATCH メソッド
  - PUT と同様リソースを更新する
  - リソースの一部を更新する際に使用しよう

### X-HTTP-Method-Override ヘッダ
環境によって PUT や DELETE や PATCH が利用できない場合に、
ヘッダにメタ情報として、本当に利用したいメソッドを明記する。
サーバー側のフレームワークやミドルウェアが標準でサポートしている場合も大い。

- X-HTTP-Method-Override
HTTPリクエストヘッダを利用する方法
```
  POST /v1/users/123 HTTP/1.1
  Host: api.example.com
  X-HTTP-Method-Override: DELETE
```

- _method
From のパラメータの 1 つとして送信する。
```
ContentType: application/x-www-form-urlencoded
user=testuser&_method=PUT
```
