---
title: インクルード ファイル
description: インクルード ファイル
services: virtual-machines-linux
author: dlepow
ms.service: virtual-machines-linux
ms.topic: include
ms.date: 06/19/2018
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: 1de7221f100077e07a2211bdb94e0198b35cb77c
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66170399"
---
## <a name="deployment-considerations"></a>デプロイに関する考慮事項

* N シリーズ VM を利用できるリージョンについては、「[リージョン別の利用可能な製品](https://azure.microsoft.com/regions/services/)」を参照してください。

* N シリーズ VM をデプロイするには、Resource Manager デプロイ モデルを使用する必要があります。

* N シリーズ VM は、それぞれのディスクに対してサポートされる Azure Storage の種類が異なります。 NC および NV の VM では、Standard Disk Storage (HDD) で提供される VM ディスクのみがサポートされます。 NCv2、NCv3、ND、NDv2、および NVv2 の VM では、Premium Disk Storage (SSD) で提供される VM ディスクのみがサポートされます。

* 多数の N シリーズ VM をデプロイする場合は、従量課金制サブスクリプションまたは他の購入オプションを検討してください。 [Azure 無料アカウント](https://azure.microsoft.com/free/)を使用している場合は、使用できる Azure コンピューティング コアの数に制限があります。

* Azure サブスクリプションの (リージョンごとの) コア クォータと NC、NCv2、NCv3、ND、NDv2、NV、または NVv2 コアの個別のクォータを増やす必要が生じる場合があります。 クォータを増やすためのリクエストは、[オンライン カスタマー サポートに申請](../articles/azure-supportability/how-to-create-azure-support-request.md) (無料) してください。 既定の制限は、サブスクリプション カテゴリによって異なる場合があります。




