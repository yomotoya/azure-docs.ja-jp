---
title: Power BI アプリ オファーのプランの設定 | Azure Marketplace
description: Microsoft AppSource Marketplace 用に Power BI アプリ オファーのプランの設定を構成します。
services: Azure, AppSource, Marketplace, Cloud Partner Portal, Power BI
author: v-miclar
ms.service: marketplace
ms.topic: conceptual
ms.date: 04/24/2019
ms.author: pabutler
ms.openlocfilehash: be2c2b4f5d9461aa0fdc6dde89931ed4b6418ced
ms.sourcegitcommit: c53a800d6c2e5baad800c1247dce94bdbf2ad324
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2019
ms.locfileid: "64943464"
---
# <a name="power-bi-apps-offer-settings-tab"></a>Power BI アプリの [プランの設定] タブ

サービス アプリの **[新しいプラン]** ページを開くと、最初に **[プランの設定]** タブが表示されます。このタブで、オファーの主要な識別子と名前を指定します。アスタリスク (*) は必須フィールドを示しています。

![[プランの設定] タブ](./media/offer-settings-tab.png)


## <a name="offer-settings-fields"></a>[Offer Settings]\(オファーの設定\) のフィールド 

**[オファーの設定]** タブでは、次の必須フィールドに情報を入力する必要があります。 必須フィールドはアスタリスク (*) で示されます。

|  フィールド        |  説明                                                               |
|---------------|----------------------------------------------------------------------------|
| **オファー ID\***  | オファーの (発行元プロファイル内での) 一意識別子です。 この ID は、製品 URL、Azure Resource Manager テンプレート、および課金レポートに表示されます。 最大長は 50 文字です。 小文字の英数字とダッシュ (-) のみを使用できます。 末尾にダッシュを使用することはできません。 この識別子は、オファーの運用開始後に変更することはできません。 Contoso がオファー ID `sample-SvcApp` でオファーを発行した場合、そのオファーには AppSource URL `https://appsource.microsoft.com/marketplace/apps/contoso.sample-SvcApp` が割り当てられます。      |
| **発行元\*** | [AppSource](https://appsource.microsoft.com) での組織の一意識別子です。 すべてのオファリングには、発行元 ID が関連付けられる必要があります。 オファーの保存後にこの値を変更することはできません。                         |
| **[名前]\***      | オファーの表示名です。 この名前は、AppSource と Cloud パートナー ポータルに表示されます。 最大長は 50 文字です。 製品のわかりやすいブランド名を使用します。 ここには組織名を含めないでください。ただし、アプリがその名前で販売される場合を除きます。 他の Web サイトやパブリケーションでこのオファーを提供する場合は、すべてのパブリケーションで同じ名前を使用します。    <br/>Power BI アプリのプレビュー期間中にオファーをリリースする場合は、`Sample Scv App (Preview)` のように、アプリケーション名の最後に `(Preview)` という文字列を追加します。 |
|     |     |


## <a name="next-steps"></a>次の手順

次のタブで、オファーの[技術情報](./cpp-technical-info-tab.md)を指定します。
