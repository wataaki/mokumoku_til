# 10. 開発者ツール

## 10-1. AWS における継続的なアプリケーション開発の支援サービス
アプリケーションは継続的に価値を高めていかなければならない。  
ソースコードのビルドやテストを走らせるなどを自動化する考え方として、
**継続的インテグレーション (CI)** や**継続的デリバリー (CD)** と呼ばれる。  
そのための環境である **CI/CD 環境**をマネージドサービスとしているのが Code シリーズ。  

### Code シリーズの概要と各サービスの役割
- CodeCommit  
  ソースコードを管理する Git リポジトリサービス
- CodeBuild  
  ソースコードのビルド / テスティングサービス  
- CodeDeploy  
  ビルドされたモジュール (アーティファクト) のデプロイサービス  
- CodePipeline  
  上記の 3 つのサービスを利用した CI/CD 環境を自動構築するサービス  
- CodeStar  
  上記 4 つのサービスを利用した CI/CD 環境を自動構築するサービス  

## 10-2. [CodeCommit](../services/CodeCommit.md)

## 10-3. [CodeBuild](../services/CodeBuild.md)

## 10-4. [CodeDeploy](../services/CodeDeploy.md)

## 10-5. [CodePipeline](../services/CodePipeline.md)
