---
author: cephalin
ms.service: app-service-web
ms.topic: include
ms.date: 11/03/2016
ms.author: cephalin
ms.openlocfilehash: 87fd6b626efb60c7fc7ec8896f2c3758ae5cc33c
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66132866"
---
### <a name="app-service-plan"></a>App Service プラン
Web アプリをホストするためのサービス プランを作成します。 **hostingPlanName** パラメーターに、プランの名前を指定します。 プランの場所は、リソース グループに使用される場所と同じになります。 価格レベルと worker サイズは **sku** パラメーターと **workerSize** パラメーターで指定されます。

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

