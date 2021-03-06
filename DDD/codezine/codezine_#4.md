# DDD読書会 6/6

## レイヤアーキテクチャ
- いくつかの層（レイヤー）に分割してシステムを構築するパターン
- ブラウザ→WEBサーバ→DB

## レイヤアーキテクチャでのDDD
- UI層
  - 描画でのみ使用が推奨
- アプリケーション層
  - アプリケーションサービス
  - 軽量なコーディネータ
- ドメイン層
  - ユースケース、ユーザーストーリー
  - ファクトリ、集約のコンストラクタにてインスタンスを生成
  -ステートレスな操作としてドメインの操作を行う
- インフラストラクチャ
  - リポジトリを使用し、永続化を行う

## 依存性逆転の原則（DIP）
- 例）複雑化するソフトウェアにユニットテストツールを用いて品質改善対応をする際に導入
- 上位が下位に依存する形をやめ、抽象が詳細に依存するのではなく、実装が抽象に依存するべき
- DIコンテナ（依存性の注入）

## ヘキサゴナルアーキテクチャー
- ドメイン層を中心に捉え、ユーザ操作/テストの入力側も、データベース/モックの出力側も全て差し替え可能なインターフェイスにする
- 対称性
- ポート＆アダプタ
  - システムの目的→ポート
  - 差し替え可能→アダプタ
- 例）永続化機能ポート、実データベースを使うアダプタ、自動テスト用モックを使うアダプタ

## SOA（サービス指向アーキテクチャ）
- ビジネス戦略を示す「ビジネスサービス」とREST/SOAPなどの「技術的サービス」の両面を意識
