---
title: インクルード ファイル
description: インクルード ファイル
services: functions
author: ggailey777
ms.service: functions
ms.topic: include
ms.date: 04/06/2019
ms.author: glenga
ms.custom: include file
ms.openlocfilehash: b6cafcfe6c892cd43f056458fe3586da834c2fd1
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66131423"
---
Functions を使用すると、[Azure portal] から関数アプリに Application Insights 統合を簡単に追加できます。

1. [ポータル][Azure portal] で、**[すべてのサービス] > [関数アプリ]** を選択し、関数アプリを選択してから、ウィンドウの上部にある **Application Insights** バナーを選択します。

    ![ポータルから Application Insights を有効にする](media/functions-connect-new-app-insights/enable-application-insights.png)

1. 画像の下の表に指定されている設定を使用して、Application Insights リソースを作成します。

   ![Application Insights リソースの作成](media/functions-connect-new-app-insights/ai-general.png)

    | Setting      | 推奨値  | Description                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Name** | 一意のアプリ名 | 関数アプリと同じ名前を使用するのが最も簡単です。この名前は、サブスクリプション内で一意である必要があります。 | 
    | **場所** | 西ヨーロッパ | 可能であれば、関数アプリと同じ[リージョン](https://azure.microsoft.com/regions/)、または近隣のリージョンを使用してください。 |

1. **[OK]** を選択します。 Application Insights リソースは、関数アプリと同じリソース グループおよびサブスクリプションに作成されます。 作成が完了したら、Application Insights ウィンドウを閉じます。

1. 関数アプリに戻り、**[アプリケーション設定]** を選択し、**[アプリケーション設定]** まで下にスクロールします。 `APPINSIGHTS_INSTRUMENTATIONKEY` という名設定が表示された場合は、Azure で実行されている関数アプリに対して Application Insights 統合が有効になっていることを意味します。

[Azure Portal]: https://portal.azure.com
