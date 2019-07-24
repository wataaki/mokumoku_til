# ECS (Amazon Elastic Container Service)  
Docker コンテナ環境を提供するサービス。  
Docker 環境に必要な設定が含まれた EC2 インスタンスを管理する。  

### Task  
EC2 インスタンス上で実行される Docker コンテナ。  
Task ごとに IAM ロールを割り当てられる。  

### Cluster  
1 つの **Cluster** 上で複数の **Task** を実行することができる。  
Cluster 上で動作する Task の定義は Task Definition で行う。  
Task の役割語とに Task Definition を用意し、それを基に Task が起動する。  

### Service  
同じ Task を複数用意したい場合に用いる。  
「Web Server 用の Task Definition で Task を 4 つ 起動する」などの指定ができる  
