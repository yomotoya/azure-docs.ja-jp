---
author: rothja
ms.service: billing
ms.topic: include
ms.date: 11/09/2018
ms.author: jroth
ms.openlocfilehash: 0b24688b502a40e722d2fcc4436ff1824862f489
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66238436"
---
| Resource | 既定の制限 | 上限 |
| --- | --- | --- |
| [デプロイあたりの Web または worker ロール数](../articles/cloud-services/cloud-services-choose-me.md)<sup>1</sup> |25 |25 |
| デプロイあたりの[インスタンスの入力エンドポイント](/previous-versions/azure/reference/gg557552(v=azure.100)#instanceinputendpoint)数 |25 |25 |
| デプロイあたりの[入力エンドポイント](/previous-versions/azure/reference/gg557552(v=azure.100)#inputendpoint)数 |25 |25 |
| デプロイあたりの[内部エンドポイント](/previous-versions/azure/reference/gg557552(v=azure.100)#internalendpoint)数 |25 |25 |
| デプロイあたりの[ホストされるサービスの証明書数](../articles/cloud-services/cloud-services-certs-create.md#what-are-service-certificates) |199 |199 |

<sup>1</sup>Web または worker ロールの Azure Cloud Service には、それぞれ運用環境用とステージング環境用の 2 つのデプロイを作成することができます。 この制限は、個別のロールの数、つまり、構成を示しています。 この制限は、ロールあたりのインスタンスの数、つまり、スケーリングを示しています。

