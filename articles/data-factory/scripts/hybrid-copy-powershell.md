---
title: 'PowerShell スクリプト: Data Factory を使用したオンプレミスから Azure へのデータのコピー | Microsoft Docs'
description: この PowerShell スクリプトは、オンプレミスの SQL Server データベースから別の Azure Blob Storage にデータをコピーします。
services: data-factory
author: linda33wj
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 10/31/2017
ms.author: jingwang
ms.openlocfilehash: 1218408bee067d6edb274fdcbf4fae62b8245a01
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "66160662"
---
# <a name="use-powershell-to-create-a-data-factory-pipeline-to-copy-data-from-on-premises-to-azure"></a>PowerShell を使用して、オンプレミスから Azure にデータをコピーするための Data Factory パイプラインを作成する

このサンプル PowerShell スクリプトは、オンプレミスの SQL Server データベースから Azure Blob Storage にデータをコピーするパイプラインを Azure Data Factory に作成します。

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh-az.md)]

## <a name="prerequisites"></a>前提条件

- **SQL Server**。 このサンプルでは、オンプレミスの SQL Server データベースを**ソース** データ ストアとして使用します。
- **Azure Storage アカウント**。 このサンプルでは、Azure Blob Storage を**コピー先/シンク** データ ストアとして使用します。 Azure ストレージ アカウントがない場合、ストレージ アカウントの作成手順については、「 [ストレージ アカウントの作成](../../storage/common/storage-quickstart-create-account.md) 」をご覧ください。
- **セルフホステッド統合ランタイム**。 [ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=39717)から MSI ファイルをダウンロードして実行し、セルフホステッド統合ランタイムをマシンにインストールします。  

### <a name="create-sample-database-in-sql-server"></a>SQL Server にサンプル データベースを作成する
1. オンプレミスの SQL Server データベースで、次の SQL スクリプトを使用して **emp** という名前のテーブルを作成します。 

   ```sql   
     CREATE TABLE dbo.emp
     (
         ID int IDENTITY(1,1) NOT NULL,
         FirstName varchar(50),
         LastName varchar(50),
         CONSTRAINT PK_emp PRIMARY KEY (ID)
     )
     GO
   ```

2. テーブルにサンプル データをいくつか挿入します。

   ```sql
     INSERT INTO emp VALUES ('John', 'Doe')
     INSERT INTO emp VALUES ('Jane', 'Doe')
   ```

## <a name="sample-script"></a>サンプル スクリプト

> [!IMPORTANT]
> このスクリプトは、Data Factory エンティティ (リンクされたサービス、データセット、およびパイプライン) を定義する JSON ファイルをハード ドライブ上の c:\ フォルダー内に作成します。

```powershell
$resourceGroupName = "<Resource group name>"
$dataFactoryName = "<Data factory name>" # must be globally unique
$storageAccountName = "<Az.Storage account name>"
$storageAccountKey = "<Az.Storage account key>"
$sqlServerName = "<SQL server name>"
$sqlDatabaseName = "SQL Server database name"
$sqlTableName = "emp" # create the emp table if it does not already exist in your database with ID, FirstName, and LastName columns of type String. 
$sqlUserName = "<SQL Authentication - user name>"
$sqlPassword = "<SQL Authentication - user password>"
$blobFolderPath = "<Azure blob container name>/<Azure blob folder name>"
$integrationRuntimeName = "<Self-hosted integration runtime name"
$pipelineName = "SqlServerToBlobPipeline"
$dataFactoryRegion = "China East"

# Create a resource group
New-AzResourceGroup -Name $resourceGroupName -Location $dataFactoryRegion

# create a data factory
$df = Set-AzDataFactory -ResourceGroupName $resourceGroupName -Name $dataFactoryName -Location $dataFactoryRegion

# create a self-hosted integration runtime
Set-AzDataFactoryIntegrationRuntime -Name $integrationRuntimeName -Type SelfHosted -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName

# get the authorization key from the created integration runtime in the cloud
Get-AzDataFactoryIntegrationRuntimeKey -Name $integrationRuntimeName -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName | ConvertTo-Json

# IMPORTANT: Install self-hosted integration runtime on your machine and use one of the keys to register the IR installed on your machine with the cloud service

# create an Az.Storage linked service

## JSON definition of the linked service. 
$storageLinkedServiceDefinition = @"
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": {
                "value": "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey",
                "type": "SecureString"
            }
        }
    }
}
"@

## IMPORTANT: stores the JSON definition in a file that will be used by the Set-AzDataFactoryLinkedService command. 
$storageLinkedServiceDefinition | Out-File c:\AzureStorageLinkedService.json

## Creates a linked service in the data factory
Set-AzDataFactoryLinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureStorageLinkedService" -File c:\AzureStorageLinkedService.json

# create an on-premises SQL Server linked service

## JSON definition of the linked service. 
$sqlServerLinkedServiceDefinition = @"
{
   "properties": {
     "type": "SqlServer",
     "typeProperties": {
         "connectionString": {
             "type": "SecureString",
            "value": "Server=$sqlServerName;Database=$sqlDatabaseName;User ID=$sqlUserName;Password=$sqlPassword;Timeout=60"
         }
     },
     "connectVia": {
       "type": "integrationRuntimeReference",
       "referenceName": "$integrationRuntimeName"
     }
 },
 "name": "SqlServerLinkedService"
}
"@

## IMPORTANT: stores the JSON definition in a file that will be used by the Set-AzDataFactoryLinkedService command. 
$sqlServerLinkedServiceDefinition | Out-File c:\SqlServerLinkedService.json

## Encrypt SQL Server credentials 
New-AzDataFactoryLinkedServiceEncryptCredential -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -IntegrationRuntimeName $integrationRuntimeName -File "c:\SqlServerLinkedService.json" > c:\EncryptedSqlServerLinkedService.json

# Create a SQL Server linked service
Set-AzDataFactoryLinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName "EncryptedSqlServerLinkedService" -File "c:\EncryptedSqlServerLinkedService.json"


# Create a source dataset for source SQL Server Database

## JSON definition of the dataset
$sourceSqlServerDatasetDefiniton = @"
{
   "properties": {
        "type": "SqlServerTable",
        "typeProperties": {
            "tableName": "$sqlTableName"
        },
        "structure": [
             {
                "name": "ID",
                "type": "String"
            },
            {
                "name": "FirstName",
                "type": "String"
            },
            {
                "name": "LastName",
                "type": "String"
            }
        ],
        "linkedServiceName": {
            "referenceName": "EncryptedSqlServerLinkedService",
            "type": "LinkedServiceReference"
        }
    },
    "name": "SqlServerDataset"
}
"@

## IMPORTANT: store the JSON definition in a file that will be used by the Set-AzDataFactoryDataset command. 
$sourceSqlServerDatasetDefiniton | Out-File c:\SqlServerDataset.json

# Create an Azure Blob dataset in the data factory
Set-AzDataFactoryDataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SqlServerDataset" -File "c:\SqlServerDataset.json"

# Create a dataset for sink Azure Blob Storage

## JSON definition of the dataset
$sinkBlobDatasetDefiniton = @"
{
    "properties": {
        "type": "AzureBlob",
        "typeProperties": {
            "folderPath": "$blobFolderPath",
            "format": {
                "type": "TextFormat"
            }
        },
        "linkedServiceName": {
            "referenceName": "AzureStorageLinkedService",
            "type": "LinkedServiceReference"
        }
    },
    "name": "AzureBlobDataset"
}
"@

## IMPORTANT: store the JSON definition in a file that will be used by the Set-AzDataFactoryDataset command. 
$sinkBlobDatasetDefiniton | Out-File c:\AzureBlobDataset.json

## Create the Azure Blob dataset
Set-AzDataFactoryDataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureBlobDataset" -File "c:\AzureBlobDataset.json"


# Create a pipeline in the data factory

## JSON definition of the pipeline
$pipelineDefinition = @"
{
   "name": "$pipelineName",
    "properties": {
        "activities": [       
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource"
                    },
                    "sink": {
                        "type":"BlobSink"
                    }
                },
                "name": "CopySqlServerToAzureBlobActivity",
                "inputs": [
                    {
                        "referenceName": "SqlServerDataset",
                        "type": "DatasetReference"
                    }
                ],
                "outputs": [
                    {
                        "referenceName": "AzureBlobDataset",
                        "type": "DatasetReference"
                    }
                ]
            }
        ]
    }
}
"@

## IMPORTANT: store the JSON definition in a file that will be used by the Set-AzDataFactoryPipeline command. 
$pipelineDefinition | Out-File c:\SqlServerToBlobPipeline.json

## Create a pipeline in the data factory
Set-AzDataFactoryPipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "$pipelineName" -File "c:\SqlServerToBlobPipeline.json"


# start the pipeline run
$runId = Invoke-AzDataFactoryPipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName $pipelineName

# Check the pipeline run status until it finishes the copy operation
while ($True) {
    $result = Get-AzDataFactoryActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)

    if (($result | Where-Object { $_.Status -eq "InProgress" } | Measure-Object).count -ne 0) {
        Write-Host "Pipeline run status: In Progress" -foregroundcolor "Yellow"
        Start-Sleep -Seconds 30
    }
    else {
        Write-Host "Pipeline $pipelineName run finished. Result:" -foregroundcolor "Yellow"
        $result
        break
    }
}

# Get the activity run details 
    $result = Get-AzDataFactoryActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName `
        -PipelineRunId $runId `
        -RunStartedAfter (Get-Date).AddMinutes(-10) `
        -RunStartedBefore (Get-Date).AddMinutes(10) `
        -ErrorAction Stop

    $result

    if ($result.Status -eq "Succeeded") {`
        $result.Output -join "`r`n"`
    }`
    else {`
        $result.Error -join "`r`n"`
    }

# To remove the data factory from the resource gorup
# Remove-AzDataFactory -Name $dataFactoryName -ResourceGroupName $resourceGroupName
# 
# To remove the whole resource group
# Remove-AzResourceGroup  -Name $resourceGroupName
```


## <a name="clean-up-deployment"></a>デプロイのクリーンアップ

このサンプル スクリプトを実行した後、次のコマンドを使用して、リソース グループとそれに関連付けられたすべてのリソースを削除できます。

```powershell
Remove-AzResourceGroup -ResourceGroupName $resourceGroupName
```
リソース グループからデータ ファクトリを削除するには、次のコマンドを実行します。 

```powershell
Remove-AzDataFactoryV2 -Name $dataFactoryName -ResourceGroupName $resourceGroupName
```

## <a name="script-explanation"></a>スクリプトの説明

このスクリプトでは以下のコマンドを使用します。 

| command | メモ |
|---|---|
| [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup) | すべてのリソースを格納するリソース グループを作成します。 |
| [Set-AzDataFactoryV2](/powershell/module/az.datafactory/set-Azdatafactoryv2) | データ ファクトリを作成します。 |
| [New-AzDataFactoryV2LinkedServiceEncryptCredential](/powershell/module/az.datafactory/new-Azdatafactoryv2linkedserviceencryptedcredential) | リンクされたサービスの資格情報を暗号化し、暗号化された資格情報で新しいリンクされたサービスの定義を生成します。 
| [Set-AzDataFactoryV2LinkedService](/powershell/module/az.datafactory/Set-Azdatafactoryv2linkedservice) | データ ファクトリ内にリンクされたサービスを作成します。 リンクされたサービスは、データ ストアまたは計算をデータ ファクトリにリンクします。 |
| [Set-AzDataFactoryV2Dataset](/powershell/module/az.datafactory/Set-Azdatafactoryv2dataset) | データ ファクトリ内にデータセットを作成します。 データセットは、パイプライン内のアクティビティの入出力を表します。 | 
| [Set-AzDataFactoryV2Pipeline](/powershell/module/az.datafactory/Set-Azdatafactoryv2pipeline) | データ ファクトリ内にパイプラインを作成します。 パイプラインには、特定の操作を実行する 1 つ以上のアクティビティが含まれています。 このパイプラインでは、コピー アクティビティが Azure Blob Storage 内のある場所から別の場所にデータをコピーします。 |
| [Invoke-AzDataFactoryV2Pipeline](/powershell/module/az.datafactory/Invoke-Azdatafactoryv2pipeline) | パイプラインの実行を作成します。 つまり、パイプラインを実行します。 |
| [Get-AzDataFactoryV2ActivityRun](/powershell/module/az.datafactory/get-Azdatafactoryv2activityrun) | パイプライン内のアクティビティの実行 (アクティビティ実行) に関する詳細情報を取得します。 
| [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) | 入れ子になったリソースすべてを含むリソース グループを削除します。 |
|||

## <a name="next-steps"></a>次の手順

Azure PowerShell の詳細については、[Azure PowerShell のドキュメント](https://docs.microsoft.com/powershell/)を参照してください。

Azure Data Factory のその他の PowerShell サンプル スクリプトについては、[Azure Data Factory の PowerShell のサンプル](../samples-powershell.md)に関する記事をご覧ください。
