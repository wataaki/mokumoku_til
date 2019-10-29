# CodePipeline
ソースコードの変更を検知し、ビルドし、デプロイする。といった流れを自動化したい場合に利用する。  

## CodePipeline の特徴
### 開発プロセスの自動化
以下の自動化されたパイプラインを作成することができる。

- ソースコードの Push  
- (Push を検知して) -> ソースコードのビルド  
- (ビルドが完了したことを検知して) -> アーティファクトのデプロイ  

すべてのプロセスを Code シリーズで用意する必要はない。  

## 承認プロセスを定義することも可能
リリースの承認プロセスをパイプラインの途中に挟むことも可能。  
以下のような承認プロセスを定義することができる。  
- 開発環境へのリリースまでは自動で行う。  
- UAT 環境へのリリースの直前に承認者にメールを送信し、承認者が承認するまでパイプラインの処理を停止する。  
- 承認者は承認したタイミングで UAT 環境へのリリースを行う。  