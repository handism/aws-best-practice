# AWSベストプラクティス IaCリポジトリ

このリポジトリは、AWSの様々なアーキテクチャパターンをベストプラクティスに沿って実装した、Infrastructure as Code (IaC) のテンプレート集です。

## 概要

このリポジトリの目的は、一般的なAWSのユースケースに対して、すぐに利用できる、よく設計されたソリューションを提供することです。テンプレートはAWS CloudFormationで記述されており、セキュリティ、スケーラビリティ、コスト効率を考慮して設計されています。

## ディレクトリ構成

- `iac/`: 各アーキテクチャのCloudFormationテンプレートが格納されています。
- `draw.io/`: アーキテクチャ図の元ファイルが格納されています。
- `img/`: エクスポートされたアーキテクチャ図の画像が格納されています。

## 利用可能なアーキテクチャパターン

`iac`ディレクトリには、以下のアーキテクチャパターンのテンプレートが含まれています。

- **コンテナオーケストレーション**: Amazon ECSまたはEKSを使用してコンテナオーケストレーション環境をデプロイします。
- **コスト最適化サーバーレス**: API Gateway、Lambda、DynamoDBを使用してコスト最適化されたサーバーレスアプリケーションを実装します。
- **高可用性パターン**: 複数のアベイラビリティゾーンにまたがる高可用で耐障害性のあるアーキテクチャをセットアップします。
- **Langfuse on AWS**: AWS上にLangfuse可観測性プラットフォームをデプロイします。
- **S3静的ウェブサイト**: Amazon S3とCloudFrontを使用して、セキュアでスケーラブルな静的ウェブサイトをホストします。
- **サーバーレスAPI**: API GatewayとLambdaを使用して標準的なサーバーレスAPIを作成します。
- **ストリーミングアーキテクチャ**: リアルタイムデータストリーミングアーキテクチャを構築します。
- **3層アーキテクチャ**: 古典的な3層ウェブアプリケーションをデプロイします。
- **VPC Latticeサービス間通信**: VPC Latticeを使用したサービス間通信を実証します。

## 利用方法

1.  `iac`ディレクトリに移動します。
2.  ユースケースに合ったテンプレートを選択します。
3.  AWSマネジメントコンソールまたはAWS CLIを使用してスタックをデプロイします。

### AWS CLIでのデプロイ例

```bash
aws cloudformation create-stack \
  --stack-name my-architecture-stack \
  --template-body file://iac/<template-name>.yaml \
  --parameters ParameterKey=MyParameter,ParameterValue=MyValue \
  --capabilities CAPABILITY_IAM
```

**注意:** 各テンプレートには固有のパラメータや要件があります。詳細については、`iac/README.md`内の各テンプレートのドキュメントや、テンプレートファイル自体を確認してください。

## Amazon Qへの指示出し方法

aws-iacサーバーを使って、なるべく安価にAWSを利用する構成のCloudFormationのコードをYAMLで書いて。最新のベストプラクティスを反映して。

さらに、作成したIaCのコードを元にして、AWSの構成図をDraw.ioで作成して。AWSサービスについては、ちゃんとAWS公式が提供している「AWS 2026」のアイコンを利用してください。

## Codex Skill

この指示を再利用できるよう、以下のSkillを追加しています。

- Skill名: `$aws-cost-optimized-cfn-drawio`
- 定義: `skills/aws-cost-optimized-cfn-drawio/SKILL.md`
- 参照資料:
  - `skills/aws-cost-optimized-cfn-drawio/references/cost-checklist.md`
  - `skills/aws-cost-optimized-cfn-drawio/references/drawio-aws-2026.md`
