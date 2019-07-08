# ELB (Elastic Load Balancing)
負荷分散、ロードバランサーのマネージドサービス。
3 タイプのロードバランサがある。

### Classic Load Balancer (CLB)
L4/L7 レイヤーでの負荷分散を行う。

### Application Load Balancer (ALB)
L7 レイヤーでの負荷分散を行う。
CLB より機能が豊富。

### Network Load Balancer (NLB)
L4 レイヤーでの負荷分散を行う。
HTTP, HTTPS 以外のプロトコル通信以外の負荷分散に使用する。

## ELB の特徴
負荷に応じて自動でスケールする設計になっている。
しかし、瞬時に行われるわけではないので急激に負荷がかかるシーン (スパイク) が予想される場合、
事前に ELB プレウォーミングの申請をする必要がある。

### ヘルスチェック
