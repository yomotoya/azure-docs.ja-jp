---
title: Azure スケール セット テンプレートでの既存の仮想ネットワークの参照 | Microsoft Docs
description: 仮想ネットワークを既存の Azure 仮想マシン スケール セット テンプレートに追加する方法について説明します。
services: virtual-machine-scale-sets
documentationcenter: ''
author: mayanknayar
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2019
ms.author: manayar
ms.openlocfilehash: 8b75b9898eb767866c0843594a82570cfb65d122
ms.sourcegitcommit: e7d4881105ef17e6f10e8e11043a31262cfcf3b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2019
ms.locfileid: "64868952"
---
# <a name="add-reference-to-an-existing-virtual-network-in-an-azure-scale-set-template"></a>既成の仮想ネットワークへの参照を Azure スケール セット テンプレートに追加する

この記事では、[基本のスケール セット テンプレート](virtual-machine-scale-sets-mvss-start.md)を変更して、新しい仮想ネットワークを作成するのではなく、既存の仮想ネットワークにデプロイする方法について説明します。

## <a name="change-the-template-definition"></a>テンプレートの定義を変更する

[前回のアーティクル](virtual-machine-scale-sets-mvss-start.md)では、基本的なスケール セット テンプレートを作成しました。 では、以前のテンプレートを使用して、スケール セットを既存の仮想ネットワークに展開するテンプレートを作成します。 

まず、`subnetId` パラメーターを追加します。 この文字列はスケール セット構成に渡されます。これにより、スケール セットは仮想マシンをデプロイする作成済みのサブネットを特定できるようになります。 この文字列は、`/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>` の形式で指定する必要があります。

たとえば、名前が `myvnet`、サブネットが `mysubnet`、リソース グループが `myrg`、サブスクリプションが `00000000-0000-0000-0000-000000000000` の既存の仮想ネットワークにスケール セットをデプロイする場合、subnetId は `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet` になります。

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "subnetId": {
+      "type": "string"
     }
   },
```

次に、`resources` 配列から仮想ネットワーク リソースを削除します。ここでは既存の仮想ネットワークを使用し、新しい仮想ネットワークをデプロイする必要はないためです。

```diff
   "variables": {},
   "resources": [
-    {
-      "type": "Microsoft.Network/virtualNetworks",
-      "name": "myVnet",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "2018-11-01",
-      "properties": {
-        "addressSpace": {
-          "addressPrefixes": [
-            "10.0.0.0/16"
-          ]
-        },
-        "subnets": [
-          {
-            "name": "mySubnet",
-            "properties": {
-              "addressPrefix": "10.0.0.0/16"
-            }
-          }
-        ]
-      }
-    },
```

テンプレートをデプロイする前に仮想ネットワークが既に存在するので、スケール セットの dependsOn 句を仮想ネットワークに指定する必要はありません。 次の行を削除します。

```diff
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "location": "[resourceGroup().location]",
       "apiVersion": "2019-03-01",
-      "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
-      ],
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
```

最後に、ユーザーが設定した `subnetId` パラメーターを渡します (`resourceId` を使用して同じデプロイの vnet の ID は取得しません。これは、基本のスケール セット テンプレートで実行されます)。

```diff
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
-                          "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
+                          "id": "[parameters('subnetId')]"
                         }
                       }
                     }
```




## <a name="next-steps"></a>次の手順

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
