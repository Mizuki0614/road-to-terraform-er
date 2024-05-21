# HCP Terraform Getting Started

HCL TerraformでのProject管理にかかわるプラクティスレポジトリです。  
下記に当チュートリアルで学習したことを記載します。  
[Get Started - HCP Terraform](https://developer.hashicorp.com/terraform/tutorials/cloud-get-started)
- HCP Terraformでできること
  - OrganizationにWorkspacesを作成する
  - Projectに複数Workspacesをアサインすることが可能
  - CLIからのHCP Terraformへのログインは```terraform login```コマンドを使用する
  - 認証にはトークンを使用
  - クラウドプロバイダーへのアクセスはIAMユーザーのクレデンシャルを使用して行う
    - OIDC認証でのロールベースのアクセスも可能らしい
  - HCP Terraform側で変数の定義とその変数を適用するスコープを作成可能
  - ```terraform apply```のyes待ちと同様に、HCP TerraformのWeb UIの"Runs"からもConfirm & applyを行うことが可能
  - HCP TerraformからVCSとの連動が可能
    - その場合、cloudブロックは必要ない
        ```
        terraform {
        /*
        cloud {
        organization = "organization-name"
        
        workspaces {
            name = "learn-terraform"
        }
        }
        */
        
        required_providers {
            aws = {
            source  = "hashicorp/aws"
            version = "~> 3.28.0"
            }
        }
        
        required_version = ">= 0.14.0"
        }
        ```
    - VCSとの統合は"Version Control"から行う
    - **Automatic speculative plans**を有効化することで、プルリクエストをmainブランチにマージした場合にHCP Terraformがトリガーされる
    - リポジトリ内の特定のパスへの変更時、または指定した形式のタグをプッシュするたびに実行をトリガーするようにワークスペースを構成することもできる

## 未対応Note
- [Terraform CloudのPlanの結果をGithub Actionsを使ってGithub上で確認する](https://dev.classmethod.jp/articles/terraform-cloud-plan-result-githubactions/)
- [Terraform CloudがValutやAWS,Azure,Google Cloudに対してOIDCで動的なクレデンシャル生成に対応](https://dev.classmethod.jp/articles/terraform-cloud-dynamic-provider-credentials/)