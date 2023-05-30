以下に「4. 変数とモジュール」の内容をMarkdown形式で記述します：

## 4. 変数とモジュール

### 4.1 変数の使用方法

Terraformでは、変数を使用して設定を柔軟に行うことができます。変数を定義し、コード内で参照することで、特定の値を複数の場所で使い回すことができます。変数は`.tfvars`ファイルや環境変数、コマンドラインフラグを介して設定することができます。

例えば、以下のように変数を定義して使用することができます：

```hcl
variable "aws_region" {
  description = "AWSリージョン"
  type        = string
  default     = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0c94855ba95c574c8"
  instance_type = "t2.micro"
  region        = var.aws_region
}
```

この例では、`aws_region`という変数を定義し、その値を`aws_instance`リソースの`region`パラメータとして使用しています。

### 4.2 モジュールの作成と利用

Terraformモジュールは、再利用可能なコンポーネントを作成するためのものです。モジュールはTerraformコードの一部をパッケージ化し、他のTerraformプロジェクトで再利用できるようにします。

モジュールを作成するには、Terraformコードを適切に構造化し、モジュールの入力変数と出力値を定義します。他のプロジェクトでモジュールを使用する際には、モジュールの入力変数に値を指定することで、再利用できます。

例えば、以下のようにモジュールを作成して利用することができます：

```hcl
# モジュール定義 (module.tf)
module "example_module" {
  source = "./modules/example"

  variable1 = "value1"
  variable2 = "value2"
}

# モジュールの利用
resource "aws_instance" "example" {
  ami           = module.example_module.ami
  instance_type = module.example_module.instance_type
}
```

この例では、`example_module`という名前のモジュールを作成し、そのモジュールに対して入力変数 `variable1` と `variable2` の値を指定しています。その後、モジュール内で定義された出力値を `aws_instance`リソース内で使用しています。
