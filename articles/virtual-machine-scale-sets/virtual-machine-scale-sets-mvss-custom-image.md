---
title: Azure スケール セット テンプレートでのカスタム イメージの参照 | Microsoft Docs
description: カスタム イメージを既存の Azure Virtual Machine Scale Set テンプレートに追加する方法について説明します。
services: virtual-machine-scale-sets
documentationcenter: ''
author: mayanknayar
manager: drewm
editor: ''
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2018
ms.author: manayar
ms.openlocfilehash: 2415d0dc2b9a2c4229d9910b42eb8ec9309ac7a7
ms.sourcegitcommit: e7d4881105ef17e6f10e8e11043a31262cfcf3b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2019
ms.locfileid: "64869107"
---
# <a name="add-a-custom-image-to-an-azure-scale-set-template"></a>Azure スケール セット テンプレートにカスタム イメージを追加する

この記事では、[基本のスケール セット テンプレート](virtual-machine-scale-sets-mvss-start.md)を変更してカスタム イメージをデプロイする方法を説明します。

## <a name="change-the-template-definition"></a>テンプレートの定義を変更する
[前回のアーティクル](virtual-machine-scale-sets-mvss-start.md)では、基本的なスケール セット テンプレートを作成しました。 では、以前のテンプレートを使用して、スケール セットをカスタム イメージから展開するテンプレートを作成します。  

### <a name="creating-a-managed-disk-image"></a>マネージド ディスク イメージを作成する

カスタムのマネージド ディスク イメージ (`Microsoft.Compute/images` 型のリソース) が既にある場合は、このセクションを省略できます。

最初に、`sourceImageVhdUri` パラメーターを追加します。これは、デプロイ元のカスタム イメージを含む Azure Storage 内の汎用化された blob への URI です。


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "The source of the generalized blob containing the custom image"
+      }
     }
   },
   "variables": {},
```

次に、`Microsoft.Compute/images` 型のリソースを追加します。これは、URI `sourceImageVhdUri` にある汎用化された blob に基づくマネージド ディスク イメージです。 このイメージは、イメージを使用するスケール セットと同じリージョンにある必要があります。 イメージのプロパティで、OS のタイプ、(`sourceImageVhdUri` パラメーターからの) blob の場所、およびストレージ アカウントのタイプを指定します。

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2019-03-01",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

スケール セット リソースで、カスタム イメージを参照する `dependsOn` 句を追加して、イメージが作成されてから、スケール セットがそのイメージからデプロイを試行するようにします。

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2019-03-01-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-to-use-the-managed-disk-image"></a>マネージド ディスク イメージを使用するようにスケール セット プロパティを変更する

スケール セット `storageProfile` の `imageReference` で、発行元、プラン、SKU、およびプラットフォーム イメージのバージョンを指定する代わりに、`Microsoft.Compute/images` リソースの `id` を指定します。

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

この例では、`resourceId` 関数を使用して、同じテンプレートで作成したイメージのリソース ID を取得します。 マネージド ディスク イメージを事前に作成している場合は、代わりにそのイメージの ID を指定する必要があります。 この ID は、`/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>` の形式で指定する必要があります。


## <a name="next-steps"></a>次の手順

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
