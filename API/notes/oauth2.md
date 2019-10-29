# OAuth 2.0
認証には OAuth という標準的な仕様を検討するべき。  
SNS (サイト B) などの情報を利用したい時に許可を与えるのが OAuth  の役割。  
OAuth を利用する利点は、標準化され広く認知されたものであるため。  
OAuth 2.0 にはリソースにアクセスするための認可を得る手順が 4 つ定められている。 (Grant Type)  

- Authorization Code
  サーバサイドで多くの処理を行うウェブアプリケーション向け
- Implicit
  スマートフォンアプリや JavaScript を用いたクライアントサイドで処理の多くを行うアプリケーション
- Resource Owner Password Credentials
  サーバサイド (サイト B) を利用しないアプリケーション向け
- Client Credentials
  ユーザ単位での認可を行わないアプリケーション向け

この中で **Resource Owner Password Credentials** は自社開発のクライアントアプリケーションで利用できる。  
OAuth を利用する際のログイン時のエンドポイントは `/oauth2/token` が一般的で望ましい。

## OAuth で Resource Owner Password Credentials 認証
以下のデータを `application/x-www-form-urlencoded` (UTF-8) で送信する。

- grant_type
  `password` という文字列。
  `Resource Owner Password Credentials` であることを表す。
- username
  ログインするユーザ名
- password
  ログインするパスワード
- scope
  アクセスのスコープを指定する (省略可能)  
  どんな権限にアクセスをさせるかを指定するもの。  
  サービスが独自に定義することができる。  

## Authorization
クライアント認証と呼ばれ、アクセスしようとしているサービスやアプリケーションを特定するための情報。  
利用することで、許可していないアプリケーションをブロックしたりするのに利用できる。  

## レスポンス
- token_type: bearer  
  OAuth 2.0 用のトークン形式。  
- access_token  
  今後のアクセスに利用するアクセストークン  
  送信方法はいくつかある。  
  - リクエストヘッダに入れる  
    `Authorization` ヘッダを使う。  
  - リクエストボディに入れる  
    `content_type` を `application/x-www-form-urlencoded` にして、  
    `access_token` という名前で格納。  
  - クエリパラメータに入れる  
    `access_token` という名前で指定。  

## アクセストークンの有効期限と更新  
アクセストークンを取得した際のレスポンスデータに expires_in というデータがある。  
これは、アクセストークンがあと何秒で有効期限をむか会えるかを秒数で表したものになる。  
有効期限が切れた場合、サーバーは invalid_token というエラーを 401 で返却する。  
invalid_token が発生した際にはリフレッシュトークンを使ってアクセストークンを再度要求することができる。  
リフレッシュトークンはアクセストークンと同時に取得できるが、リフレッシュトークンを返さないことも可能なので、その場合は再ログインが必要となる。  
