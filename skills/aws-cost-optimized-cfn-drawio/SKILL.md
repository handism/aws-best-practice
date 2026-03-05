---
name: aws-cost-optimized-cfn-drawio
description: AWSの低コスト構成をCloudFormation(YAML)で設計し、そのIaCに対応するDraw.io構成図を作成する。`aws-iac`サーバーの利用を求められたとき、最新ベストプラクティス反映を求められたとき、公式AWSアイコン（AWS 2026）を使った図面作成を求められたときに使う。
---

# AWS Cost Optimized CFN + Draw.io

## Goal

以下を一貫して作成する。

- `iac/<name>.yaml`: 低コスト重視のCloudFormationテンプレート
- `draw.io/<name>.drawio`: テンプレートと整合したAWS構成図
- 必要に応じて `img/<name>.drawio.svg`: 図のエクスポート

## Workflow

1. 要件を短く確定する  
最初に以下を確認する。未指定ならコスト重視の既定値を採用する。
- ワークロード種別（API / バッチ / 静的配信 / イベント駆動）
- 可用性要件（単一AZ許容か、マルチAZ必須か）
- データ保持期間とバックアップ要件
- 想定トラフィック（低 / 中 / 高）

2. `aws-iac`サーバーを優先利用する  
`aws-iac`が利用可能なら、テンプレート骨子・パラメータ・リソース設計を取得して反映する。  
利用不可なら、このリポジトリの `iac/` 既存テンプレートを参考に自力で生成する。

3. CloudFormation YAMLを作成する  
以下を必ず満たす。
- YAMLで記述する
- Parameters / Outputs を定義する
- 最小権限IAM、暗号化、ログ保持を含める
- コスト最適化設定を明示する（詳細は [cost-checklist.md](references/cost-checklist.md)）

4. 最新ベストプラクティスを確認する  
「最新」要件がある場合、生成前に一次情報（AWS公式ドキュメント）を確認する。  
回答では確認日を明示し、反映したポイントを箇条書きで示す。

5. Draw.io図を作成する  
IaCのリソース構成・通信経路と1:1対応する図を `draw.io/` に作成する。  
アイコンは公式AWSアイコン（AWS 2026）を使用する。手順は [drawio-aws-2026.md](references/drawio-aws-2026.md) を優先する。

6. 整合性チェックを実施する  
最低限以下を確認する。
- IaCにある主要リソースが図に存在する
- 図にある主要リソースがIaCに存在する
- 通信方向・公開境界（Internet/VPC/Subnet）が一致する

## Default Design Rules

- まずはサーバーレス構成を優先する（例: API Gateway + Lambda + DynamoDB）
- 従量課金を優先する（オンデマンド、必要時のみ実行）
- 常時稼働リソースを最小化する
- ログ保持は短めの既定値を設定し、要件で延長する
- 監視は最低限のアラームから始める
- 将来拡張を考慮し、パラメータで切替可能にする

## Output Contract

作業完了時は以下を報告する。

1. 生成・更新したファイルパス
2. 低コスト化の要点（3-7項目）
3. 最新ベストプラクティス確認元（AWS公式URL）
4. 図で使用したAWS 2026アイコンの適用方法
5. 未解決事項（あれば）

## References

- コスト最適化チェック: [cost-checklist.md](references/cost-checklist.md)
- Draw.io + AWS 2026アイコン運用: [drawio-aws-2026.md](references/drawio-aws-2026.md)
- 共通仕様（エージェント非依存）: [common-spec.md](references/common-spec.md)
- エージェント別マッピング: [agent-mapping.md](references/agent-mapping.md)
