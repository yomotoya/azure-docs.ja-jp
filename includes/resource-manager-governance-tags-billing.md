---
title: インクルード ファイル
description: インクルード ファイル
services: azure-resource-manager
author: tfitzmac
ms.service: azure-resource-manager
ms.topic: include
ms.date: 02/19/2018
ms.author: tomfitz
ms.custom: include file
ms.openlocfilehash: e7fcb72cecbfad2de80b844ed5281267d5e4c0c3
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66164619"
---
リソースにタグを適用した後、それらのタグでリソースのコストを表示できます。 コスト分析に最新の使用状況が表示されるには少し時間がかかるため、まだコストが表示されない可能性があります。 コストが使用可能な場合は、サブスクリプション内のリソース グループにまたがるリソースのコストを表示できます。 コストを表示するには、ユーザーに[課金情報へのサブスクリプション レベルのアクセス権](../articles/billing/billing-manage-access.md)が必要です。

ポータル内でタグでコストを表示するには、サブスクリプションを選択し、**[コスト分析]** を選択します。

![コスト分析](./media/resource-manager-governance-tags-billing/select-cost-analysis.png)

次に、タグ値でフィルター処理し、**[適用]** を選択します。

![タグでコストを表示する](./media/resource-manager-governance-tags-billing/view-costs-by-tag.png)

[Azure Billing API](../articles/billing/billing-usage-rate-card-overview.md) を使用して、プログラムでコストを表示することもできます。
