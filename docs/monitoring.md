## AWS X-Ray 概要

### 目的

- アプリケーションの**分散トレーシング**を実現し、パフォーマンスボトルネックやエラーの原因を特定

### 特徴

- リクエストの**エンドツーエンドの流れを可視化**
- Lambda、API Gateway、ECS、ELB、DynamoDB、S3 などと統合
- 各サービスの**レイテンシ・ステータス・エラー情報**を可視化

### 主要概念

- **セグメント（Segment）**：各コンポーネントでの処理情報
- **サブセグメント（Subsegment）**：より細かい処理単位（DB クエリなど）
- **トレース（Trace）**：リクエスト全体の処理フロー
- **アノテーション / メタデータ**：検索可能な情報と詳細情報

### メリット

- アプリケーションの内部動作を視覚化
- マイクロサービス間の依存関係を分析
- パフォーマンス改善・障害調査に有効

### 注意点

- トレースデータ保持期間は 30 日間
- 高トラフィック時は**サンプリング**で制御
- 料金体系はリクエスト数とトレース量に依存

### 主なユースケース

- Lambda の処理遅延やエラーの追跡
- API Gateway → Lambda → RDS/DynamoDB の呼び出しフローの可視化
- サービス間通信のボトルネック調査
