---
title: Azure Marketplace から VM をデプロイする
description: Azure Marketplace の事前構成済み仮想マシンから仮想マシンをデプロイする方法について説明します。
services: Azure, Marketplace, Cloud Partner Portal,
author: v-miclar
ms.service: marketplace
ms.topic: article
ms.date: 11/29/2018
ms.author: pabutler
ms.openlocfilehash: 482840f5e611bc2d8092add2822a0ed5b2c8f883
ms.sourcegitcommit: c53a800d6c2e5baad800c1247dce94bdbf2ad324
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2019
ms.locfileid: "64938698"
---
# <a name="deploy-a-virtual-machine-from-the-azure-marketplace"></a>Azure Marketplace から仮想マシンをデプロイする

この記事では、与えられた Azure PowerShell スクリプトを使用し、Azure Marketplace から事前構成済み仮想マシンをデプロイする方法について説明します。  このスクリプトによって、VM 上で WinRM HTTP と HTTPS のエンドポイントも公開されます。  このスクリプトでは、Azure Key Vault に証明書を既にアップロードしていることが前提条件となります。詳細は「[Create certificates for Azure Key Vault](./cpp-create-key-vault-cert.md)」(Azure Key Vault の証明書を作成する) にあります。 

[!INCLUDE [updated-for-az](../../../../includes/updated-for-az.md)]

## <a name="vm-deployment-template"></a>VM デプロイ テンプレート

クイック スタートの Azure VM デプロイ テンプレートはオンライン ファイル [azuredeploy.json](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-vm-winrm-keyvault-windows/azuredeploy.json) として利用できます。  これには次のパラメーターが含まれています。

|  **パラメーター**        |   **説明**                                 |
|  -------------        |   ---------------                                 |
| newStorageAccountName | ストレージ アカウントの名前                       |
| dnsNameForPublicIP    | パブリック IP の DNS 名。 小文字にする必要があります。    |
| adminUserName         | 管理者のユーザー名                          |
| adminPassword         | 管理者のパスワード                          |
| imagePublisher        | イメージ発行者                                   |
| imageOffer            | イメージ オファー                                       |
| imageSKU              | イメージ SKU                                         |
| vmSize                | VM のサイズ                                    |
| vmName                | VM の名前                                    |
| vaultName             | Key Vault の名前                             |
| vaultResourceGroup    | Key Vault のリソース グループ                   |
| certificateUrl        | 証明書の URL。`https://testault.vault.azure.net/secrets/testcert/b621es1db241e56a72d037479xab1r7` のように KeyVault のバージョンが含まれます |
|  |  |


## <a name="deployment-script"></a>デプロイ スクリプト

次の Azure PowerShell スクリプトを編集し、それを実行して指定の Azure Marketplace VM をデプロイします。

```powershell

New-AzResourceGroupDeployment -Name "dplvm$postfix" -ResourceGroupName "$rgName" -TemplateUri "https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-vm-winrm-keyvault-windows/azuredeploy.json" -newStorageAccountName "test$postfix" -dnsNameForPublicIP $vmName -adminUserName "isv" -adminPassword $pwd -vmSize "Standard_A2" -vmName $vmName -vaultName "$kvname" -vaultResourceGroup "$rgName" -certificateUrl $objAzureKeyVaultSecret.Id 

```


## <a name="next-steps"></a>次の手順

事前構成済み VM をデプロイしたら、それに含まれるソリューションやサービスにアクセスし、構成したり、さらなる開発のために使用したりできます。 
