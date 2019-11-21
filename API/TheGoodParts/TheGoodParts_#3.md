# 3. レスポンスデータの設計
美しいレスポンスデータとは何か。  
どうすればよりプログラムで処理しやすいレスポンスデータとなるか。  

## 3.1 データフォーマット
デフォルトで JSON に対応し、需要があれば XML に対応するのが現実に即している。  
かつては XML が主流だったが、現在では JSON の方がデファクトスタンダードとなっている。  
JSON の方がシンプルに表すことができ、JavaScript との相性もとても良いためだと考えられる。  
XML の方が表現力は豊かではある。  

### 3.1.1 データフォーマットの指定方法
クライアント側から欲しいデータの形式をサーバに伝える方法はいくつかある。  

- クエリパラメータを使う方法 (おすすめ)  
  ```
    https://api.example.com/v1/users?format=xml
  ```
- 拡張子を使う方法  
  ```
    https://api.example.com/v1/users.json
  ```
- リクエストヘッダでメディアタイプを指定する方法 (お行儀が良い)  
  ```
    GET /v1/users  
    Host: api.example.com  
    Acept: application/json
  ```

世間的にはクエリパラメータを使う方法がもっともよく使われている。  
手軽で見やすく敷居が低いのが特良。省略可能であることがわかりやすいのもある。  
HTTP の仕様的にはメディアタイプを使う方法がもっともあっているが少し敷居が高い。  

## 3.2 JSONP の取り扱い
`JSON with padding` の略。以下のように JSON にラップする JavaScript を付け加えたものをいう。  
```
  callback({"id":123, "name": "Saeed"})
```
付け加えるものは JavaScript だけでなく HTML などでも良い。  
クロスドメインの回避策。  

### 3.2.1 JSONP をサポートする場合の作法
コールバック関数を用いる方法と、グローバル変数に格納する方法がある。  