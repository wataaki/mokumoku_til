# API. The Good Parts
## 2 章

### API を設計する
必要な機能を洗い出し、画面遷移図に書き出す
機能ごとに必要なAPIを洗い出す
APIとして統合できそうな機能を考える（e.g. 一覧取得と検索機能）

### [エンドポイントを考える](../notes/uri_endpoint.md)

### [HTTP メソッドとエンドポイント](../notes/request_method.md)

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
