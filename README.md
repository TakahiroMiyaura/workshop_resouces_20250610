# workshop_resouces_20250610

[Microsoftの技術で理解するAI エージェントの始め方](https://osaka-driven-dev.connpass.com/event/354374/)内で実施するワークショップに関するリソースプロジェクトです。

## 必要な環境

1. Azureサブスクリプション - [無料で作成](https://azure.microsoft.com/free/cognitive-services?WT.mc_id=aiml-132569-bethanycheum)
1. [サポートされているリージョンでGPT-4oとDALL.E 3モデルがサポートされているAzure OpenAIリソース](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models#assistants-preview?WT.mc_id=aiml-132569-bethanycheum)。推奨リージョンは**Sweden Central**です。

Azureのリソースについては以下のリンクからARMテンプレートを用いて展開可能です。

[![Deploy to Azure](https://camo.githubusercontent.com/3a3895e70f3c2f85416ce486a768b7e02e23cc574ed4bb9f302aa7e0e5e09881/68747470733a2f2f616b612e6d732f6465706c6f79746f617a757265627574746f6e)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FTakahiroMiyaura%2Fworkshop_resouces_20250610%2Frefs%2Fheads%2Fmain%2Flab%2Fassets%2FAITour24_WKR540_Template.json)

展開後のリソース
![Deploy to Azure](/images/deploy.png)

<details>
<summary>検証時にエラーが出る場合</summary>

1. Quota関連のエラー  
今回デプロイするGPT-4OはQuotaを30ほど消費します。既に設定したリージョン内でデプロイ済みのモデルがあり、Quotaに余裕がない場合はそのことがエラーとして通知されます。**既存のQuotaを見直してQuotaを確保してください。**
1. モデルエラー  
Azure OpenAI で利用できる各モデルは随時更新されています。ARMテンプレートに設定されているモデルじゃージョンが廃止になりエラーが発生する場合があります。この場合、サイトでサポートバージョンを確認しテンプレートの修正を行います。  
カスタムデプロイの画面で[テンプレートの編集]をクリックし92行目付近から始まるモデル定義を修正します。
```json
"deployments": {
  "value": [
    {
      "name": "gpt-4o-mini",
      "model": {
        "format": "OpenAI",
        "name": "gpt-4o-mini",
        "version": "2024-07-18"
      },
      "sku": {
        "name": "Standard",
        "capacity": 30
      }
    },
    {
      "name": "dall-e-3",
      "model": {
        "format": "OpenAI",
        "name": "dall-e-3",
        "version": "3.0"
      },
      "sku": {
        "name": "Standard",
        "capacity": 1
      }
    },
    {
      "name": "gpt-4o-realtime-preview",
      "model": {
        "format": "OpenAI",
        "name": "gpt-4o-realtime-preview",
        "version": "2024-12-17"
      },
      "sku": {
        "name": "GlobalStandard",
        "capacity": 1
      }
    }
  ]
}
```

</details>