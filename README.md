# AWS Infrastruction

・CloudFormation (VPC + Basiton + ECS managed Fargate + S3 bucket + DB + codepipeline)
マスターテンプレートは、drafan/vpc-bastion-fargate-rds.cfn.yml
drafan/templates以下の必要なサービスをネストしています。

構築に約20分、デプロイに約10分かかります。

## GitHub連携

GitHub連携のときは、アカウントのTokenが必要です。
こちらのページからトークンを発行して貼り付けてください。
https://github.com/settings/tokens

## 変更スタック

プロパティーの値やスタックの構成を変えたい場合、変更スタックを作成すれば変更できます。
ECS（Fargate）のCPU/Memoryは組み合わせが決まっているので、注意。
https://docs.aws.amazon.com/ja_jp/AmazonECS/latest/developerguide/task-cpu-memory-error.html

## TODO
・Laravelのプログラムをデプロイ
・LaravelのログをCloudWatchで出力
・DeletePolicyの設定：スタックを削除したときに各サービスが消去されないように設定
・SNS設定：デプロイやCloudWatchアラートをSlackに飛ばすように設定

# おまけ

## おまけスタック

code2s3.yml
プッシュするとCodePipelineでAWSのs3バケットに特定ディレクトリを飛ばす設定がされています。
SNS通知あり。テンプレートの更新に！（aws-cliの方が早いけど）

## スタックを消すとき

ロールバックで[ECSリポジトリの削除]と[S3バケットの削除]で引っかかるので、
マスタースタックを消して（※データ消えます）再構築したいときは、マスタースタック削除前にECSリポジトリとS3バケットを削除してください。