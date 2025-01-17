---
title: インクルード ファイル
description: インクルード ファイル
services: virtual-machines-windows
author: cynthn
ms.service: virtual-machines-windows
ms.topic: include
ms.date: 09/12/2018
ms.author: cynthn
ms.custom: include file
ms.openlocfilehash: ec6cbcbc93fe87634c87caeb0041b75ec916a22f
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66154780"
---
サブネットまたは仮想マシン (VM) ネットワーク インターフェイスでネットワーク フィルターを作成して、Azure で VM へのポートを開くか、エンドポイントを作成します。 インバウンドとアウトバウンドの両方のトラフィックを制御するこれらのフィルターを、トラフィックを受信するリソースに接続されているネットワーク セキュリティ グループに配置します。

この記事の例では、標準の TCP ポート 80 を使用するネットワーク フィルターを作成する方法を示します (適切なサービスが既に開始され、VM 上で OS ファイアウォール規則が開かれているものと仮定しています)。

標準の TCP ポート 80 で Web 要求を処理するように構成された VM を作成した後は、次の操作を実行できます。

1. ネットワーク セキュリティ グループを作成します。

2. トラフィックを許可するインバウンド セキュリティ規則を作成し、次の設定に値を割り当てます。

   - **[宛先ポート範囲]** : 80

   - **発信元ポート範囲**: * (すべての発信元ポートを許可)

   - **優先度**:65,500 より小さく、既定の包括的なインバウンド拒否規則よりも優先される値を入力します。

3. ネットワーク セキュリティ グループと VM のネットワーク インターフェイスまたはサブネットを関連付けます。

この例では単純な規則を使用して HTTP トラフィックを許可していますが、ネットワーク セキュリティ グループと規則を使用して、より複雑なネットワーク構成を作成することもできます。 




