# 4. コンピューティングサービス  

## 4-1 AWS におけるコンピューティングサービス  

### コンピューティングサービス  
アプリケーションを稼働させるインフラストラクチャサービスで、  
システムアーキテクチャの中核を担う。  

## 4-2. [EC2](../services/EC2.md)  

## 4-3. [ELB](../services/ELB.md)  

### 単一障害点  
ある特定の部分が止まると全体が止まってしまう箇所のこと  
いかに単一障害点をなくすかというところが大事。  
部分部分の障害に備えた設計をすることを心得る。  

## 4-4. [ECS](../services/ECS.md)  

### その他のコンテナサービス  
- AWS Fargete  
  ECS とは違い EC2 を使用せずにコンテナを動かすことができる。  
- EKS (Amazon Elastic Container Service for Kubernetes)  
  Kubernetes というコンテナ管理の自動化のためのオープンソースプラットフォーム。  
- ECR (Amazon Elastic Container Registy)  
  コンテナイメージを管理するレジストリを提供する。  

## 4-5. [Lambda](../services/Lambda.md)  
