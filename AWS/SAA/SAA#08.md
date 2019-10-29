# 8. セキュリティとアイデンティティ  

## 8-1. セキュリティとアイデンティティ  
### AWS のアカウントの種類  
「AWS アカウント」と「IAM ユーザー」の 2 種類が存在する。  
また、複数の AWS アカウントを管理するための **AWS Organization** という機能もある。  
複数のアカウントの請求をひとまとめにする一括決済が可能となる。  

### AWS アカウント
AWS へサインアップするときに作成されるアカウント。  
AWS の全てのサービスをネットワーク上のどこからでも利用可能。  
ルートユーザーとも呼ばれる。  
非常に強力なアカウントであるため、取り扱いには十分注意する必要がある。  
AWS でシステムを構成・運用する場合 IAM ユーザー利用するべき。  

### IAM ユーザー
AWS を利用する各利用者向けに作成されるアカウント。  
各 IAM ユーザーに対して、操作を許可する (しない) サービスを定義できる。  
IAM ユーザーの管理はセキュリティのかなめ。  

### [IAM の機能](../services/IAM.md)

## 8-2. [KMS と CloudHSM](../services/KMSとCloudHSM.md)

## 8-3. [AWS Certificate Manager](../services/ACM.md)
## サーバー証明書
サーバーの信頼性を確認するために利用される。
プロトコルは SSL/TLS。  

## 証明書の役割と種類  
証明書を利用して実現できることは主に 2 つある。  
- 経路間の通信の安全性の確保  
- 通信している相手が誰かの証明  

### 証明の方法
- 自己証明書  
  自分で認証局を立てて証明書を発行する   
- ドメイン認証 (DV)  
  ドメインの所有のみを認証。組織情報の確認はされない。  
- 組織認証 (OV)  
  組織情報の審査を経てから認証する。  
- 拡張認証 (EV)  
  OV より厳格な審査で認証する。アドレスバーに組織名が表示される。  