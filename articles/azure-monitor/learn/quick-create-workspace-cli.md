---
title: Azure CLI を使用して Log Analytics ワークスペースを作成する | Microsoft Docs
description: Azure CLI で Log Analytics ワークスペースを作成して、クラウドおよびオンプレミス環境から管理ソリューションを有効にし、データを収集できるようにする方法を学習します。
services: log-analytics
documentationcenter: log-analytics
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.topic: conceptual
ms.date: 03/12/2019
ms.author: magoedte
ms.openlocfilehash: 4be33b809ee2e620a565c9907a5b77833a279567
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "66130405"
---
# <a name="create-a-log-analytics-workspace-with-azure-cli-20"></a>Azure CLI 2.0 を使用して Log Analytics ワークスペースを作成する

Azure CLI 2.0 は、コマンド ラインやスクリプトで Azure リソースを作成および管理するために使用します。 このクイック スタートでは、Azure CLI 2.0 を使って、Azure Monitor に Log Analytics ワークスペースをデプロイする方法を示します。 Log Analytics ワークスペースは、Azure Monitor ログ データ用の一意の環境です。 各ワークスペースには、独自のデータ リポジトリと構成があり、データ ソースとソリューションは、特定のワークスペースにデータを格納するように構成されます。 次のソースからデータを収集しようとする場合、Log Analytics ワークスペースが必要です。

* サブスクリプション内の Azure リソース  
* System Center Operations Manager によって監視されているオンプレミスのコンピューター  
* System Center Configuration Manager のデバイス コレクション  
* Azure ストレージからの診断またはログ データ  
 
環境内の Azure VM、Windows VM、Linux VM などの他のソースについては、次のトピックを参照してください。

* [Azure Virtual Machines に関するデータの収集](../learn/quick-collect-azurevm.md)
* [ハイブリッド Linux コンピューターからのデータの収集](../learn/quick-collect-linux-computer.md)
* [ハイブリッド Windows コンピューターからのデータの収集](quick-collect-windows-computer.md)

Azure サブスクリプションをお持ちでない場合は、開始する前に[無料アカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)を作成してください。

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

CLI をローカルにインストールして使用することを選択する場合、このクイック スタートでは、Azure CLI バージョン 2.0.30 以降を実行している必要があります。 バージョンを確認するには、`az --version` を実行します。 インストールまたはアップグレードする必要がある場合は、「[Azure CLI 2.0 のインストール](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)」を参照してください。

## <a name="create-a-workspace"></a>ワークスペースの作成
[az group deployment create](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create) を使用してワークスペースを作成します。 次の例では、ローカル コンピューターから Resource Manager テンプレートを使用して、*eastus* の場所にあるリソース グループ *Lab* に *TestWorkspace* という名前のワークスペースを作成します。 JSON テンプレートは、ワークスペースの名前の入力だけをユーザーに求め、環境の標準構成として使用される可能性のある他のパラメーターには既定値を指定するように構成されています。 または、組織内の共有アクセス用に Azure ストレージ アカウントにテンプレートを格納することができます。 テンプレートを操作する方法の詳細については、「[Resource Manager テンプレートと Azure CLI を使用したリソースのデプロイ](../../azure-resource-manager/resource-group-template-deploy-cli.md)」を参照してください

サポートされているリージョンについては、[Log Analytics を使用できるリージョン](https://azure.microsoft.com/regions/services/)に関するページを参照し、**[製品を検索する]** フィールドから Azure Monitor を検索してください。 

以下のパラメーターには、既定値が設定されます。

* location - 既定値は米国東部
* sku - 既定値は、2018 年 4 月の価格モデルでリリースされた新しい 1 GB あたりの価格レベル

>[!WARNING]
>新しい 2018 年 4 月の価格モデルを選択したサブスクリプションで Log Analytics ワークスペースを作成または構成する場合、有効な Log Analytics 価格レベルは **PerGB2018** のみです。 
>

### <a name="create-and-deploy-template"></a>テンプレートの作成とデプロイ

1. 以下の JSON 構文をコピーして、ファイルに貼り付けます。

    ```json
    {
    "$schema": "https://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "workspaceName": {
            "type": "String",
            "metadata": {
              "description": "Specifies the name of the workspace."
            }
        },
        "location": {
            "type": "String",
            "allowedValues": [
              "eastus",
              "westus"
            ],
            "defaultValue": "eastus",
            "metadata": {
              "description": "Specifies the location in which to create the workspace."
            }
        },
        "sku": {
            "type": "String",
            "allowedValues": [
              "Standalone",
              "PerNode",
              "PerGB2018"
            ],
            "defaultValue": "PerGB2018",
            "metadata": {
            "description": "Specifies the service tier of the workspace: Standalone, PerNode, Per-GB"
        }
          }
    },
    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "name": "[parameters('workspaceName')]",
            "apiVersion": "2015-11-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "sku": {
                    "Name": "[parameters('sku')]"
                },
                "features": {
                    "searchVersion": 1
                }
            }
          }
       ]
    }
    ```

2. 要件に合わせてテンプレートを編集します。 どのプロパティと値がサポートされているかを調べるには、[Microsoft.OperationalInsights/workspaces テンプレート](https://docs.microsoft.com/azure/templates/microsoft.operationalinsights/workspaces)のリファレンスを参照してください。 
3. このファイルを **deploylaworkspacetemplate.json** としてローカル フォルダーに保存します。   
4. これでこのテンプレートをデプロイする準備が整いました。 テンプレートがあるフォルダーから以下のコマンドを使用します。

    ```azurecli
    az group deployment create --resource-group <my-resource-group> --name <my-deployment-name> --template-file deploylaworkspacetemplate.json
    ```

デプロイが完了するまでに数分かかる場合があります。 完了すると、次のような結果を含むメッセージが表示されます。

![デプロイ完了時の結果の例](media/quick-create-workspace-cli/template-output-01.png)

## <a name="next-steps"></a>次の手順
使用できるワークスペースが用意されたので、管理テレメトリの収集の構成、ログ検索の実行によるデータの分析、管理ソリューションの追加による追加データと分析的な考察の提供を行うことができます。  

* Microsoft Azure Diagnostics または Azure ストレージを使用して Azure リソースからデータを収集できるようにするには、「[Log Analytics で Azure サービスのログとメトリックを使用できるように収集する](../platform/collect-azure-metrics-logs.md)」を参照してください。  
* Operations Manager 管理グループに報告するエージェントからデータを収集して Log Analytics ワークスペースに格納するには、[データ ソースとして System Center Operations Manager を追加](../platform/om-agents.md)します。  
* 階層内のコレクションのメンバーであるコンピュータをインポートするには、[構成マネージャー](../platform/collect-sccm.md)に接続します。  
* 使用可能な[監視ソリューション](../insights/solutions.md)と、ソリューションをワークスペースに対して追加または削除する方法を確認します。
