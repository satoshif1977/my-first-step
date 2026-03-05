# my-first-step

AWS アーキテクチャ設計図のリポジトリです。
実務・学習・試験対策（AWS 生成 AI プロフェッショナル含む）を目的に作成した構成図を管理しています。

---

## 構成図一覧

| ファイル名 | 内容 |
|-----------|------|
| `260220.drawio` | AWS Web アプリケーション構成図（Multi-AZ / Auto Scaling） |
| `260226.drawio` | Amazon Bedrock RAG 構成図 |
| `Agent Broker Architecture 構成図.drawio` | Bedrock Converse API を使ったマルチエージェント構成 |
| `Bedrock Agents 構成図.drawio` | Amazon Bedrock Agents 構成図 |
| `GenU構成図.drawio` | 社内 AI チャットボット（GenU）構成図 |

---

## 各構成図の概要

### Web アプリケーション構成（260220.drawio）

Multi-AZ・Auto Scaling を備えた本番想定の Web アプリケーション構成です。

```
Route53 → WAF → CloudFront → IGW → ALB
  → Auto Scaling（EC2 x2, マルチAZ）
  → RDS（Multi-AZ, MySQL）
  → S3（静的コンテンツ / VPC Endpoint）
  → Bastion Host（SSHアクセス管理）
```

**ポイント:**
- EC2 を直接公開せず ALB 経由でアクセス
- WAF + CloudFront でエッジセキュリティ
- RDS Multi-AZ で高可用性を確保

---

### Bedrock RAG 構成（260226.drawio）

Retrieval-Augmented Generation（RAG）を使った AI チャットボット構成です。

```
ユーザー → Cognito 認証 → API Gateway → Lambda
  → Bedrock Knowledge Base（OpenSearch Serverless）
  → S3（ドキュメント格納）
  → DynamoDB（会話履歴）
  → CloudWatch（ログ・監視）
```

**ポイント:**
- Cognito による認証・認可
- OpenSearch Serverless をベクターデータベースとして使用
- AWS 生成 AI プロフェッショナル試験の頻出構成

---

### Agent Broker アーキテクチャ（Agent Broker Architecture 構成図.drawio）

Bedrock Converse API を中心としたマルチエージェント構成です。

```
ユーザー → Agent Broker（Converse API）
  → 専門エージェント A（情報取得）
  → 専門エージェント B（データ分析）
  → 専門エージェント C（レポート生成）
```

---

### Bedrock Agents 構成（Bedrock Agents 構成図.drawio）

Amazon Bedrock Agents を使ったタスク自動化構成です。

```
ユーザー → API Gateway → Lambda → Bedrock Agent
  → 基盤モデル（Claude 3）
  → Action Group（Lambda）
  → Knowledge Base（S3 + OpenSearch）
  → DynamoDB（会話履歴）
```

---

### GenU 社内 AI チャットボット（GenU構成図.drawio）

Generative AI Use Cases（GenU）を使った社内向け AI チャットボット構成です。

```
社員 → Cognito → CloudFront → S3（画面）
     → API Gateway → Lambda → Bedrock（Claude 3）
     → DynamoDB（履歴）
     → Kendra（社内文書検索）
     → WAF + CloudWatch（セキュリティ・監視）
```

---

## 使用ツール

- [draw.io / diagrams.net](https://app.diagrams.net/) - 構成図の作成・編集

## 参考

- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [Amazon Bedrock ドキュメント](https://docs.aws.amazon.com/bedrock/)
- [AWS 認定 AI プラクティショナー（AIF-C01）](https://aws.amazon.com/certification/certified-ai-practitioner/)
