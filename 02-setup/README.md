## 2. セットアップ

### 2.1 AWSアカウントのセットアップとTerraformの設定

AWSのセットアップでは、アクセスキーとシークレットアクセスキーが必要になります。これらのキーはAWSのIAM（Identity and Access Management）コンソールから取得することができます。Terraformは、これらのキーを利用してAWSリソースにアクセスします。

### 2.2 AWS認証情報の設定

AWS認証情報は`~/.aws/credentials`ファイルに保存されます。AWS CLIを使用して設定することができます。以下の手順で設定を行います。

1. ターミナルを開き、以下のコマンドを実行します。

```bash
$ aws configure
```

2. アクセスキーとシークレットアクセスキーを入力し、デフォルトのリージョンと出力形式を指定します。

```
AWS Access Key ID [None]: YOUR_ACCESS_KEY
AWS Secret Access Key [None]: YOUR_SECRET_KEY
Default region name [None]: YOUR_REGION
Default output format [None]: json
```

### 2.3 Terraformの初期化

Terraformプロジェクトを初期化するためには、Terraform設定ファイル（`.tf`ファイル）があるディレクトリで`terraform init`コマンドを実行します。これにより、必要なプロバイダー（この場合はAWS）のプラグインがダウンロードされます。

以下の手順で初期化を行います。

1. ターミナルを開き、Terraform設定ファイルがあるディレクトリに移動します。

```bash
$ cd path/to/terraform/project
```

2. `terraform init`コマンドを実行します。

```bash
$ terraform init
```

初期化が完了すると、Terraformプロジェクトがセットアップされ、プロバイダーのダウンロードが行われます。
