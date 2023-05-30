## 1. はじめに

### 1.1 インフラストラクチャ・コード（IaC）の紹介

Infrastructure as Code (IaC)は、設定管理の一部としてデータセンターのインフラストラクチャを管理するためのアプローチです。IaCは、手動プロセスに代わる自動化されたプロセスを提供します。例えば、EC2インスタンスを手動で作成する代わりに、以下のようなTerraformコードを記述し、実行することで、自動的にインスタンスを作成します。

```terraform
resource "aws_instance" "example" {
  ami           = "ami-0c94855ba95c574c8"
  instance_type = "t2.micro"
}
```

### 1.2 AWSアカウントのセットアップとTerraformの設定

AWSとTerraformを使用するための初期セットアップには、以下のステップが含まれます。

**1.2.1 AWSアカウントの作成** 

まず、[AWS Management Console](https://aws.amazon.com/console/) から新しいAWSアカウントを作成します。これは無料で行うことができ、一部のサービスは無料枠の範囲内で利用することができます。

**1.2.2 AWS CLIのインストール**

AWS CLIをインストールするには、Homebrewを使用します。以下のコマンドをターミナルに入力します。

```bash
$ brew install awscli
```

インストールが完了したら、次のコマンドでバージョンを確認してインストールの成功を確認します。

```bash
$ aws --version
```

**1.2.3. asdfのインストールとTerraformのバージョン管理**

asdfは多くのランタイムのバージョン管理が可能なプラグインベースのツールで、Terraformのバージョン管理にも使用します。以下のコマンドを実行してasdfをインストールし、Terraformプラグインを追加します。

```bash
# asdfのインストール
$ brew install asdf

# asdfのTerraformプラグイン追加
$ asdf plugin-add terraform https://github.com/asdf-community/asdf-hashicorp.git
```

次に、特定のバージョンのTerraformをインストールします。例えば、バージョン0.14.0をインストールする場合は、次のコマンドを実行します。

```bash
# Terraformのバージョン0.14.0をインストール
$ asdf install terraform 0.14.0

# 特定バージョンを全体のデフォルトとして設定
$ asdf global terraform 0.14.0
```

**1.2.4. AWS CLIとAWS認証情報の設定**

次に、AWSの認証情報を設定します。これには、通常、AWS CLIを使用します。これにより、TerraformはAWS APIを呼び出し、リソースを作成、更新、削除することができます。以下のコマンドを実行して、AWSの認証情報を設定します。

```bash
$ aws configure
AWS Access Key ID [None]: YOUR_ACCESS_KEY
AWS Secret Access Key [None]: YOUR_SECRET_KEY
Default region name [None]: YOUR_REGION
Default output format [None]: json
```
この時点で、AWSアカウントとTerraformが設定され、Terraformを使用してAWSリソースを管理する準備が整います。


### 1.3 最初のTerraformコードの実行

最初のTerraformコードを実行するための手順は以下の通りです。

**1. ディレクトリの作成と移動**

まず、Terraformコードを格納する新しいディレクトリを作成し、そのディレクトリに移動します。

```bash
$ mkdir terraform_first_code
$ cd terraform_first_code
```

**2. Terraformファイルの作成**

新しく作成したディレクトリに `main.tf` という名前のファイルを作成します。このファイルにTerraformコードを記述します。今回は、以下のように簡単なEC2インスタンスを作成するコードを書きます。

```terraform
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0c94855ba95c574c8"
  instance_type = "t2.micro"
}
```

**3. Terraformコードの初期化と適用**

次に、Terraformコードを初期化し、適用します。初期化は `terraform init` コマンドを実行することで行います。このコマンドはTerraformのプロジェクトを初期化し、必要なプロバイダープラグインをダウンロードします。

```bash
$ terraform init
```

初期化が完了したら、`terraform apply` コマンドを実行してコードを適用します。このコマンドは、コードに記述されたインフラストラクチャが作成されるようにAWSに指示します。

```bash
$ terraform apply
```

コマンドを実行すると、Terraformは作成するリソースのプランを表示し、承認を求めます。これが適切であると確認したら、`yes`を入力してプランを承認します。

これにより、AWSにEC2インスタンスが作成されます。

**注意:** 使用後はコストを抑えるために、作成したリソースを削除してください。これは `terraform destroy` コマンドを実行することで行います。

```bash
$ terraform destroy
```
