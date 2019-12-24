# Visitor パターン
「訪問者」という意味。  
Visitor オブジェクトに処理を記述し、処理の追加を簡単にする。  

## 概要
Visitor オブジェクトがどのようなクラスだろうと、受け入れ側に変更が発生しない。  

### Acceptor オブジェクト
Visitor オブジェクトを受け入れる accept(Visitor visitor) メソッドを実装する。
