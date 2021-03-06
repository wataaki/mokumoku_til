# 2. エンドポイントの設計とリクエストの形式

## API を設計する  
必要な機能を洗い出し、画面遷移図に書き出す  
機能ごとに必要なAPIを洗い出す  
APIとして統合できそうな機能を考える（e.g. 一覧取得と検索機能）  

## [2.2 API エンドポイントの考え方](../notes/uri_endpoint.md)  

## [2.3 HTTP メソッドとエンドポイント](../notes/request_method.md)  

## 2.4 API のエンドポイント設計  

### リソースにアクセスするためのエンドポイントの設計の注意点  
#### 複数形の名詞を利用する  
リソースは集合を表すもの。  
URI はリソースを表すもの。動詞はメソッドで。  

#### 利用する単語に気をつける  
search と find の違いなど、ネイティヴではないとわからないようなもの。  
類似の API がどのような単語を利用しているかを調べるのが良い。  

#### スペースやエンコードを必要とする文字を使わない  
URI に使用できない文字は、パーセントエンコーディングされる。  
空白は `+` に変換される。  
どちらも UIR を見づらくするので使わないのが基本。  

#### 単語をつなげる必要がある場合はハイフンを利用する  
決定的な理由はないが、世間的にハイフンつなぎが普及している。  
Google が推奨しているので SEO 的にもハイフンつなぎが良い。  

## 2.5 検索とクエリパラメータの設計  
ユーザの一覧を取得するような API を考えた時、  
すべてのユーザを取得してしまうと、場合によっては莫大な数となってしまう。  
それをさけるため、1度に取得できる数をしぼったりする必要がある。  
そこで使用するのが、クエリパラメータとなる。  

### 取得数と取得位置のクエリパラメータ  
いわゆるページネーションのこと。  
一般的に page/per_page offset/limit などが使用される。  

### 相対位置を利用する問題点  
データの数が増えるとパフォーマンスも落ちる。  
更新のタイミングにかち合えば、データの不整合がおこりうる。  

### 絶対位置でデータを取得する  
「先頭から数えて何番目」ではなく、  
指定した ID や更新日時より前といった方法で指定する方法。  

### 絞り込みのためのパラメータ  
欲しい情報の 1 データを指定する方法。  
クエリパラメータの名前は絞り込む要素名、値には絞り込む値を指定する。  
検索するフィールドがほぼ 1 つに決まる場合、 q (query) というパラメータが使われる場合もある。  
q は部分一致のイベージが強いので、使用する際は気をつける。 (Google の検索等で使われている)  

### クエリパラメータとパスの使い分け  
クエリパラメータ を URI の中に入れる方法も可能。  
その判断の基準となるのは以下のようなもの。  

- 一意なリソースを表すのに必要な情報  
  URI はリソースそのものであるという思想からのもの。  
  ユーザ ID など、指定することで一意にきまるものがそれ。  
- 省略可能でない  
  ページ指定などのデフォルト値があるようなもので省略が可能なものは  
  クエリパラメータが適している。  

## 2.6 [ログインと OAuth 2.0](../notes/oauth2.md)  

### 自分の情報へのエイリアス  
ユーザ情報を取得するエンドポイントでユーザ ID を指定する代わりに me または self というキーワードをしてすると  
現在のアクセストークンに紐づいた「自分」のユーザ情報を取得できるというもの。  

## 2.7 ホスト名とエンドポイントの共通部分
`https://api.example.com/v1` の部分は API に共通する部分となる。  
さまざまなサービスの共通部分を調べると、いくつか共通点が見える。  
- `api.example.com` のように `API` という名前がホスト名に含まれている。  
- `v1` などの API のバージョン番号が含まれている。  

## 2.8 SSKDs と API デザイン  
機能毎に API を細かく分けていくのは、広く一般に公開する `LSUDs` に向いている。
逆に、アプリ専用の API である `SSKDs` にはあまり適していない場合もある。
例えば、EC サイトのホーム画面を表示するために「おすすめ商品」「新着情報」「ユーザ情報」などを取得するためになども API にアクセスする必要があり、
非効率である上に、画面表示までに時間がかかってしまう場合もある。  
なので、「ホーム画面表示用 API」を作成し、1 回のアクセスで全て取得できた方が利便性が高いと言える。  

## 2.9 HATEOAS と REST LEVEL3 API  
REST API にいたるための設計レベル。  
- REST LEVEL 0 - HTTP を使っている  
- REST LEVEL 1 - リソースの概念の導入  
- REST LEVEL 2 - HTTP の動詞 (GET/POST/PUT/DELETE など) の導入  
- REST LEVEL 3 - HATEOAS の概念の導入  

### REST LEVEL 3 API (HATEOAS)
API の返すデータの中に、次に行う行動、取得するデータ等の URI をリンクとして含めることで、次にアクセスするエンドポイントがわかる設計。  
こうすることで、クライアントがあらかじめエンドポイントを知らなくても動作可能となる。  
メディアタイプを返すデータ形式ごとに変えることで、クライアントがどんなデータが送られてきたかを知ることができる。  

### REST LEVEL 3 API のメリット
クライアントがああらかじめ URI を知る必要がないので URI の変更がしやすくなる点、および URI を改造しやすい物にする必要がなくなるという点。  

### REST LEVEL 3 API
特定のクライアントのみで使われるような SSKDs 向け API では、ニージ次第で採用可能。  

## 2.10 まとめ
- URI は**リソース**を表す。  
- URI と HTTP メソッドの組み合わせで処理の対象と内容を表す。  
- 覚えやすく、どんな機能を持つかが一目でわかるエンドポイントにする。  
- 適切な HTTP メソッドを利用する。  
- 適切な英単語を利用し、単数形、複数形に注意する。  
- 認証には OAuth 2.0 を使う
