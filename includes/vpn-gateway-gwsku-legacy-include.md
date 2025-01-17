---
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 11/09/2018
ms.author: cherylmc
ms.openlocfilehash: f2ee442d0d6fecf34449ad28f058615a1274bbea
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66159209"
---
レガシ (古い) VPN ゲートウェイ SKU には以下があります。

* Basic
* Standard
* HighPerformance

VPN Gateway では、UltraPerformance ゲートウェイ SKU が使用されません。 UltraPerformance SKU については、[ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) のドキュメントを参照してください。

レガシ SKU を操作する場合は、以下を考慮してください。

* PolicyBased VPN タイプを使用する場合には、Basic SKU を使用する必要があります。 PolicyBased VPN (旧称静的ルーティング) は、その他の SKU ではサポートされていません。
* BGP は、Basic SKU ではサポートされていません。
* ExpressRoute と VPN Gateway が共存する構成は、Basic SKU ではサポートされていません。
* アクティブ/アクティブ S2S VPN ゲートウェイ接続は、HighPerformance SKU のみで構成できます。