---
title: インクルード ファイル
description: インクルード ファイル
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 10/17/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 49f48c2d0bf865cf8c8fde831e7a597f8701d213
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66150018"
---
"Get-AzVirtualNetworkGatewayConnection" コマンドレットを使用して、接続が成功したことを確認できます。"-Debug" は指定しても指定しなくてもかまいません。 

1. 次のコマンドレットを使用します。値は実際の値に置き換えてください。 プロンプトが表示されたら、"A" を選択して "すべて" (All) を実行します。 この例では、テストする接続の名前が "-Name" で示されています。

   ```azurepowershell-interactive
   Get-AzVirtualNetworkGatewayConnection -Name VNet1toSite1 -ResourceGroupName TestRG1
   ```
2. コマンドレットの実行後、値を確認します。 以下の例では、接続状態は "Connected" と表示され、受信バイトと送信バイトを確認できます。
   
   ```
   "connectionStatus": "Connected",
   "ingressBytesTransferred": 33509044,
   "egressBytesTransferred": 4142431
   ```