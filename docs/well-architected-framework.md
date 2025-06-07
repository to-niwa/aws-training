# AWS Well-Architected Framework

## 概要

AWS Well-Architected Framework（WAF）は、クラウドアーキテクチャ設計におけるベストプラクティス集。  
SAA試験では、6つの柱（Pillars）に基づく設計判断が頻出。

---

## 1. Operational Excellence（運用上の優秀性）

### 🔹 目的
システムの運用を自動化・監視し、継続的に改善する。

### 🔹 設計原則
- 運用の自動化（SSM, Lambda）
- 障害からの学習と改善
- ログ・監査（CloudWatch Logs, CloudTrail）

### 🔹 試験ポイント
- EC2 自動復旧：CloudWatch Alarm + Auto Recovery
- パッチ適用：SSM Patch Manager
- 運用の自動化：SSM Automation、Run Command

---

## 2. Security（セキュリティ）

### 🔹 目的
データとシステムを保護し、アクセス制御とインシデント対応を徹底する。

### 🔹 設計原則
- 最小権限の原則（IAM, SCP）
- データの保護（KMS, Secrets Manager）
- 多層防御（WAF, SG, NACL）
- 継続的な脅威検出（GuardDuty）

### 🔹 試験ポイント
- IAMロール + ポリシーでアクセス制御
- S3暗号化：SSE-KMS、SSE-S3
- GuardDuty で脅威検出
- CloudTrail + Config で監査

---

## 3. Reliability（信頼性）

### 🔹 目的
障害から回復し、安定したパフォーマンスと可用性を維持する。

### 🔹 設計原則
- 冗長構成（Multi-AZ, Auto Scaling）
- 変更のテスト（Blue/Green, CloudFormation）
- クォータ管理とリトライ戦略

### 🔹 試験ポイント
- RDS リードレプリカ / クロスリージョン
- ALB + Auto Scaling
- S3 バージョニングとレプリケーション

---

## 4. Performance Efficiency（パフォーマンス効率）

### 🔹 目的
適切なリソースとサービスを使って、効率よくスケーラブルに動作させる。

### 🔹 設計原則
- 適切なサービス選択（Lambda, Fargate, S3）
- オートスケーリング（App Auto Scaling）
- キャッシュ利用（ElastiCache, CloudFront）

### 🔹 試験ポイント
- CloudFront で静的コンテンツ高速化
- DynamoDB + DAX で低レイテンシ読み取り
- ALB + Auto Scaling によるリクエスト分散

---

## 5. Cost Optimization（コスト最適化）

### 🔹 目的
無駄な支出を避け、コスト効率を最大化する。

### 🔹 設計原則
- 使用量の可視化（Cost Explorer）
- 課金モデルの最適化（RI, Savings Plans, Spot）
- 不要リソースの削除（EBS, RDS）

### 🔹 試験ポイント
- S3 Lifecycle で古いデータを IA / Glacier に移行
- Spot インスタンスの活用
- Cost Explorer + Budgets で可視化とアラート

---

## 6. Sustainability（持続可能性）

### 🔹 目的
環境への影響を抑え、長期的に持続可能な設計を行う。

### 🔹 設計原則
- 環境効率の良いリージョン選択
- Graviton プロセッサ活用（高性能/省電力）
- サーバーレス設計（Lambda, Fargate）
- スリープ / シャットダウンの自動化

### 🔹 試験ポイント
- 出題頻度はまだ少ないが、今後増加の可能性あり

---

## 試験対策まとめ表

| 柱                        | 主要サービス・キーワード例                                    |
|---------------------------|---------------------------------------------------------------|
| Operational Excellence    | CloudWatch, SSM, Lambda, CloudTrail                           |
| Security                  | IAM, KMS, WAF, GuardDuty, Secrets Manager                     |
| Reliability               | Multi-AZ, Auto Scaling, Route 53, RDS リードレプリカ           |
| Performance Efficiency    | Lambda, CloudFront, ElastiCache, ALB, DAX                     |
| Cost Optimization         | RI, Spot, Cost Explorer, S3 Lifecycle, Budgets                |
| Sustainability            | Graviton, サーバーレス, スリープ設計, 環境効率の高いリージョン |

---

