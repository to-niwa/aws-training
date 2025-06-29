## AWS における DR 戦略の種類と特徴

### 1. バックアップ＆リストア（Backup and Restore）

- 最もシンプルな DR 戦略
- 定期的に S3 や Glacier にバックアップ
- **復旧時間（RTO）は長いがコストは最小**

### 2. パイロットライト（Pilot Light）

- 必須の最小限コンポーネントのみ常時起動（例：DB）
- その他のコンポーネントは障害時に起動
- **低コスト × 中程度の復旧時間**

### 3. ウォームスタンバイ（Warm Standby）

- 本番と同等の構成を縮小規模で常時稼働
- 障害時にスケールアップして切替
- **中コスト × 短めの復旧時間**

### 4. マルチサイトアクティブ-アクティブ（Multi-Site Active-Active）

- 複数リージョンに本番環境を常時稼働
- リージョン障害でも即座に切替可能
- **高コスト × 最短の復旧時間（RTO ほぼゼロ）**

### 比較表

| 戦略                   | コスト | RTO      | RPO      | 特徴                                 |
| ---------------------- | ------ | -------- | -------- | ------------------------------------ |
| バックアップ＆リストア | ★      | 数時間～ | 数時間～ | 安価、運用も容易                     |
| パイロットライト       | ★★     | 数十分～ | 数分～   | DB 常時稼働、App 起動が必要          |
| ウォームスタンバイ     | ★★★    | 数分～   | 数分～   | 小規模な本番環境、スケールアップ必要 |
| アクティブ-アクティブ  | ★★★★   | 秒単位   | 秒単位   | 即時切替、コスト高                   |

### よく利用されるサービス

| カテゴリ               | サービス                                                      | 役割                           |
| ---------------------- | ------------------------------------------------------------- | ------------------------------ |
| バックアップ           | AWS Backup / S3 / Glacier                                     | データの定期保存               |
| データレプリケーション | RDS リードレプリカ / Aurora Global DB / DynamoDB Global Table | データ同期                     |
| インフラ管理           | CloudFormation / Elastic Beanstalk / Terraform                | インフラの復旧用自動化         |
| ネットワーク切替       | Route 53 / Global Accelerator                                 | トラフィックのフェイルオーバー |
| モニタリング           | CloudWatch / AWS Health Dashboard                             | 障害検知と通知                 |

## AWS Global Accelerator 概要

### 目的

- グローバルなアプリケーションの**パフォーマンス向上**と**高可用性**を実現するトラフィック制御サービス

### 特徴

- **固定の Anycast IP アドレス**をグローバルに提供
- エッジロケーション経由で最適な AWS リージョンに転送
- **リージョン間のフェイルオーバー・ルーティング制御**が可能
- TCP/UDP トラフィックを対象に、L4 レベルで機能

### 主なユースケース

- マルチリージョン構成の API や Web サービスへの高速アクセス
- 災害時の**自動フェイルオーバー**
- モバイルやグローバルユーザー向けの**レイテンシ改善**

### 対象サービス

- ALB / NLB
- EC2
- EIP（Elastic IP）

### メリット

- グローバル Anycast で**高速ルーティング**
- レイテンシベースのトラフィック分散
- アクティブ/スタンバイ構成の**高速フェイルオーバー**

### 注意点

- DNS ベースの Route 53 とは異なり**IP アドレス固定**（DNS キャッシュ影響なし）
- 対象は L4（TCP/UDP）のみ（HTTP レベルのルーティングは不可）
- 有料サービス（エッジロケーション数や帯域使用に応じた課金）
