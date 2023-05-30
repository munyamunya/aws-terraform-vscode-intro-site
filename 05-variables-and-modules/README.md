## 5. 状態の管理とバージョン管理

### 5.1 Terraformの状態ファイル

Terraformは、管理しているリソースの現在の状態を`.tfstate`ファイルに保存します。この状態ファイルには、作成されたリソースの詳細情報や依存関係が含まれています。Terraformは、この状態ファイルを使用して、計画と適用の間で何が変更されるべきかを把握します。

例えば、以下はTerraformでEC2インスタンスを作成するコードです：

```hcl
resource "aws_instance" "example" {
  ami           = "ami-0c94855ba95c574c8"
  instance_type = "t2.micro"
  tags = {
    Name = "ExampleInstance"
  }
}
```

このコードを実行すると、Terraformは`.tfstate`ファイルを作成し、作成されたEC2インスタンスの情報を保持します。これにより、Terraformは次回の実行時に、作成済みのインスタンスを識別し、変更の必要性を判断できます。

`.tfstate`ファイルは重要な情報を含んでいるため、適切に管理する必要があります。Terraform CloudやAWS S3などのリモートバックエンドを使用することで、状態ファイルを安全に管理することができます。

### 5.2 バージョン管理とワークスペース

Terraformプロジェクトは成長していくため、バージョン管理が重要になってきます。バージョン管理ツール（Gitなど）を使用してTerraformコードをバージョン管理し、変更履歴を追跡することが推奨されます。

例えば、以下はGitを使用してTerraformコードをバージョン管理する手順です：

1. TerraformプロジェクトのディレクトリをGitリポジトリに初期化します。

```bash
$ cd my_terraform_project
$ git init
```

2. `.tf`ファイルやその他のプロジェクトファイルをコミットします。

```bash
$ git add .
$ git commit -m "Initial commit"
```

3. 変更を加えたり新機能を追加したりするたびに、コードの変更をコミットします。

```bash
$ git add .
$ git commit -m "Update EC2 instance configuration"
```

ワークスペースを使用することで、同じ設定を異なる環境で再利用できます。ワークスペースを使うことで、開発、ステージング、本番などの環境ごとにTerraformの設定を管理できます。ワークスペースは状態ファイルを分離し、異なる環境でのリソースの作成や変更を管理するのに役立ちます。

例えば、以下はTerraformのワークスペースを使用して、異なる環境で同じコードを実行する手順です：

1. 開発用のワークスペースを作成します。

```bash
$ terraform workspace new dev
```

2. `dev`ワークスペースに切り替えます。

```bash
$ terraform workspace select dev
```

3. プロジェクトのディレクトリでTerraformコマンドを実行します。

```bash
$ terraform plan
$ terraform apply
```

これにより、異なる環境での設定の再利用と管理が容易になります。