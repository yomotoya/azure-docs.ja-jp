---
title: インクルード ファイル
description: インクルード ファイル
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 01/09/2019
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 78dfd57fba6365f9c8937b30b5cf96b840749c68
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66157627"
---
| **ベンダー名** | **デバイス ファミリ** | **ファームウェア バージョン** |
| --- | --- | --- |
|Cisco | ISR| IOS 15.1 (プレビュー)|
|Cisco | ASA | 9.8 より前の ASA 用 ASA (*) RouteBased (IKEv2- No BGP) |
|Cisco | ASA | 9.8 以降の ASA 用 ASA RouteBased (IKEv2- No BGP) |
|Juniper | SRX_GA | 12.x|
|Juniper | SSG_GA | ScreenOS 6.2.x|
|Juniper | JSeries_GA | JunOS 12.x|
|Juniper | SRX | JunOS 12.x RouteBased BGP |
|Ubiquiti| EdgeRouter| EdgeOS v1.10x RouteBased VTI|
|Ubiquiti| EdgeRouter| EdgeOS v1.10x RouteBased BGP|

> [!NOTE]
> (*) 必須: NarrowAzureTrafficSelectors (UsePolicyBasedTrafficSelectors オプションを有効にする) と CustomAzurePolicies (IKE/IPsec)
>
