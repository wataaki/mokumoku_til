# Storage Gateway  
オンプレミスにあるデータをクラウドへ連携するための受け口を提供するサービス。  
データの保存先には S3 や Glacier などの耐久性が高く低コストなストレージが利用される。  
参照頻度が高いデータはオンプレミスの高速ストレージに保存し、参照頻度が低いデータやバックアップデータは  
Storage Gateway を利用してクラウドに保管するなどの使い分けができる。  

## Storage Gateway のタイプ  

### ファイルゲートウェイ  
S3 をクライアントサーバーから NFS マウントして、ファイルシステムのように扱うことができるタイプのボリュームゲートウェイ。  
非同期だが、ほぼリアルタイムで S3 にアップロードされる。  
保存されたデータに S3 の API を利用してアクセスすることも可能。  
注意点として、データの読み書きがローカルディスクに比べて遅い。  
S3 の Web API でアクセスするようなユースケースに有効。  

### ボリュームゲートウェイ
データを S3 に保存することはファイルゲートウェイと同じだが、各オブジェクトとして管理するのではなく、  
S3 のデータ保存領域全体を 1 つのボリュームとして管理する。  
そのため、 S3 に保存されたデータに S3 の API を利用してアクセスすることはできない。  
クライアントサーバーからの接続方式は NFS ではなく iSCSI 接続になる。  
ボリュームはスナップショットを取得することができるので、スナップショットから EBS を作成し、  
EC2 インスタンスにアタッチすることで、スナップショットを取得した時点までのデータにアクセスできるようになる。  

#### キャッシュ型ボリューム  
頻繁に利用するデータは Storage Gateway 内のキャッシュディスク (EBS) に保存して高速にアクセスすることを可能とし、  
全てのデータを保存するストレージとして S3 を利用するタイプのボリュームゲートウェイ。  
キャッシュ上に存在しないデータにアクセスする場合は S3 から取得する必要があるため、データの読み込み速度が重要な場合は適さない。  
**キャッシュボリューム**: 頻繁に使用するデータに対して高速にアクセスするためのもの。  
**アップロードバッファボリューム**: S3 にアップロードするデータを一時的に保管するためのもの。  

#### 保管型ボリューム  
全てのデータを保存するストレージとしてローカルストレージを利用し、データを定期的にスナップショット形式で S3 へ転送するタイプのボリュームゲートウェイ。  
必要に応じてスナップショットを EC2 インスタンスにアタッチすることでデータを参照することができる。  

### テープゲートウェイ  
テープデバイスの代替として S3 や Glacier にデータをバックアップするタイプのゲートウェイ。  
物理のテープカートリッジを入れ替えたり遠隔地にオフサイト保存するということをする必要がなくなる。  

## セキュリティ  
### CHAP 認証  
クライアントから Storage Gateway に iSCSI で接続する際に、CHAP 認証を設定することができる。  
不正なクライアントからのなりすましを防止でき、通信の盗聴といった脅威に対するリスクを軽減できる。  

### データの暗号化  
AWS KMS を使ってデータの暗号化が可能。  
データが保管されるタイミングで暗号化される。  
また、暗号化されたボリュームから取得したスナップショットも同じキーで暗号化される。  

### 通信の暗号化  
オンプレミスから Storage Gateway 経由で S3 にデータを転送する際には HTTPS が使用されるので、通信路のデータ内容は暗号化される。  