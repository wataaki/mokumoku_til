# Swarm クラスタ
swarm とは Docker が動作し、クラスタに参加しているマシングループ。  
swarm を使えば、Docker コマンドをこれまで通り使い続けながら swarm マネージャを通してクラスタ上で実行可能になる。  
swarm マネージャには Compose ファイルを通して命令できる。  

## Swarm のセットアップ  
swarm は複数のノードで構成する。  
`docker swarm init` を実行すると `swarm mode` を有効化し、現在のマシンを swarm マネージャにする。  
そして `docker swarm join` を実行し、他のマシンをワーカとして swarm に追加する。  

## クラスタの作成
