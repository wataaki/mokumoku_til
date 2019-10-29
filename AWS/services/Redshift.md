# Amazon Redshift
データウェアハウス向けのデータベースサービス。  

## Redshift の構成
複数ノードによる分散並列実行が大きな特徴としてあげられる。  
1 つの Redshift を構成する複数のノードのまとまりを Redshift クラスタと呼ぶ。  
クラスタの 1 つのリーダーノードと複数のコンピュートノードから構成される。  
- リーダーノード  
  SQL クライアントや BI ツールからの実行クエリを受け付けて、クエリの解析や実行プランの作成を行う。  
  コンピュートノードの数に応じて最適な分散処理が実行できるようにする司令塔のような役割。  
- コンピュートノード  
  リーダーノードからの実行クエリを処理するノード。  
  コンピュートノードを追加することで CPU やメモリ、ストレージといったリソースを増やすことができ Redshift のパフォーマンスが向上する。  
- ノードスライス  
  Redshift が分散並列処理をする最小の単位。  
  ノード内のスライス数はコンピュートノードのインスタンスタイプによって異なる。  

## Redshift の特徴  
### 列指向型 (カラムナ) データベース  
データウェアハウスでは、大量のデータに対して集計処理を実行することがメインとなる。  
データウェアハウスの最大のボトルネック要因はデータ I/O になる。  
列指向型 (カラムナ) データベースは、集計処理に使われるデータをまとめて (列単位で) 管理し、ストレージからのデータ取得を効率化する。  

### 多くの圧縮エンコード方式への対応  
データ I/O のボトルネックを発生させないための方法として、取得するデータ量を削減するアプローチもある。  
Redshift は 9 種類の圧縮エンコード方式に対応している。  

### ゾーンマップ  
Redshift ではブロック単位でデータが格納される。1 ブロックの容量は 1MB。  
ゾーンマップとはそのブロック内に格納されるデータの最小値と最大値をメモリに保存する仕組み。  
この仕組みを活用することで、データ検索条件に該当するあたいの有無を効率的に判断でき、データが存在しない場合はそのブロックを読み飛ばして処置を高速化する。  

### 柔軟な拡張性  
Redshift の柔軟な拡張性を実現している仕組みは MPP とシェアードナッシングの 2 つ。  
- MPP  
  1 回の集計処置を複数のノードに分散して実行する仕組み。  
  ノードを追加するだけで分散並列処理のパフォーマンスを向上させることができる。
- シェアードナッシング  
  各ノードがディスクを共有ぜず、ノードとディスクセットで拡張する仕組み。  
  複数のノードが同一のディスクを共有する事による I/O 性能の劣化を回避するために採用される。  

### ワークロードの管理機能  
Redshift では、多種多様なデータ解析要求を効率的に処理するための管理機能が用意されている。  
Redshift のパラメータグループにある `wlm_json_configuration` パラメータでクエリの実行に関する定義が可能。  

- クエリキューの定義  
  実行するクエリの種類に応じて専用のキューを作成する。  

### Redshift Spectrum  
Redshift Spectrum は S3 に置かれたデータを外部テーブルとして定義できるようにし Redshift 内にデータを取り込むことなくクエリの実行を可能にする拡張サービス。  
Redshift 内のデータと S3 上のデータを組み合わせた SQL の実行も可能なため、  
アクセス頻度の低いデータを S3 に置いてディスク容量を節約する、複数の Redshift クラスタから S3 上のデータを共有するなどが可能となった。  