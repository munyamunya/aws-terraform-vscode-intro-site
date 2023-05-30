## 3. リソースの作成と管理

### 3.1 インフラストラクチャの定義

Terraformを使用してインフラストラクチャを定義するには、`.tf`ファイルにAWSリソースの定義を記述します。これにより、TerraformはAWS上で作成するリソースの詳細を把握し、必要なリソースを管理します。

### 3.2 Terraformコードの作成

Terraformコードは、AWSリソースの作成、更新、削除を行うための指示を含む`.tf`ファイルです。TerraformコードはHCL（HashiCorp Configuration Language）と呼ばれる言語で記述されます。このコードは、必要なAWSリソースの設定や相互の依存関係を定義します。

例えば、以下のようなTerraformコードでEC2インスタンスを作成することができます：

```hcl
resource "aws_instance" "example" {
  ami           = "ami-0c94855ba95c574c8"
  instance_type = "t2.micro"
}
```

このコードは、指定したAMI（Amazon Machine Image）を使用して`t2.micro`のインスタンスを作成することを定義しています。

### 3.3 リソースのプランニングとデプロイ

Terraformを使用してリソースを作成、変更、削除する場合、まず`terraform plan`コマンドを実行してプランを確認します。このコマンドは、Terraformが実行する変更の概要を表示します。具体的には、作成、更新、削除されるリソースの詳細なプランを示します。

```bash
$ terraform plan
```

プランを確認した後、`terraform apply`コマンドを実行して変更を適用します。このコマンドは、Terraformによって定義されたリソースをAWSに作成、更新、削除するための指示を与えます。

```bash
$ terraform apply
```

コマンドを実行すると、Terraformはプランを再確認し、変更を実際に適用します。

**注意:** プランを確認し、変更を適用する前に、変更の影響を十分に理解し、確認してください。