# データベースサービス

## 6-1. AWS のデータベースサービス  
AWS では 5 つのデータベースサービスを提供している。  
- Amazon RDS  
- Amazon DynamoDB  
- Amazon Neptune  
- Amazon Redshift  
- Amazon ElastiCache  

### データベースの 2 大アーキテクチャ  
RDB と NoSQL と呼ばれる 2 つのアーキテクチャに分類する。  

#### RDB (Relational Database)  
日本語訳で「関係データベース」と呼ばれるもの。  
データを表形式で表現し、各表の関係を定義・関連付けすることでデータを管理するデータベース。  
RDB の各種操作には SQL を使用する。  
AWS のデータベースサービスのうち RDS と Redshift が RDB のサービス。  
主なソフトウェアに Oracle, Microsoft SQL Server, MySQL, PostgreSQL などがある。  

#### NoSQL (Not Only SQL)  
RDB のデータ操作で利用する SQL を使わないデータベースアーキテクチャの総称。  
RDB と比較すると「柔軟でスキーマレスなデータモデル」「水平スケーラビリティ」「分散アーキテクチャ」「高速な処理」特徴としてあげられる。  
RDB が抱えるパフォーマンスとデータモデルの問題に対処することを目的に作られた新しいアーキテクチャ。  
AWS のデータベースサービスのうち DynamoDB, ElastiCache, Neptune が NoSQL のサービス。  
主なソフトウェアに Redis, Memcached, Cassandra, HBase, MongoDB, CouchDB, Neo4j, Titan などがある。  

### RDB と NoSQL に得意不得意を理解する  
これまでのシステムは、システムの中に RDB が 1 つあり、保持しておく必要があるデータは全てその中に格納するという構成が大半を占めていた。  
新たに　登場した NoSQL は、RDB を完全に置き換えるものではない。  
1 つのシステムの中でどちらか一方だけを使うのではなく、アプリケーションのユースケースに応じて複数のデーベースを使い分けるという考え方を持つようにすると良い。  

## 6-2. [RDS](../services/RDS.md)
