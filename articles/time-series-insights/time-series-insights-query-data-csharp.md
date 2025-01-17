---
title: C# コードを使用して Azure Time Series Insights GA 環境からデータを照会する | Microsoft Docs
description: この記事では、C# .NET 言語で記述されたカスタム アプリをコーディングして、Azure Time Series Insights 環境からデータを照会する方法について説明します。
ms.service: time-series-insights
services: time-series-insights
author: ashannon7
ms.author: dpalled
manager: cshankar
reviewer: jasonwhowell, kfile, tsidocs
ms.devlang: csharp
ms.workload: big-data
ms.topic: conceptual
ms.date: 06/05/2019
ms.custom: seodec18
ms.openlocfilehash: 250dd691c3ef3146d6768123de52bf0628b10e42
ms.sourcegitcommit: 1aefdf876c95bf6c07b12eb8c5fab98e92948000
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66728959"
---
# <a name="query-data-from-the-azure-time-series-insights-ga-environment-using-c"></a>C# を使用して Azure Time Series Insights GA 環境からデータを照会する

この C# サンプルでは、Azure Time Series Insights GA 環境からデータを照会する方法について説明します。

このサンプルでは、クエリ API の基本的な使用例をいくつか示します。

1. 準備手順として、Azure Active Directory API を使用してアクセス トークンを取得します。 このトークンをすべてのクエリ API 要求の `Authorization` ヘッダーで渡します。 非対話型アプリケーションのセットアップについては、「[Azure Time Series Insights API の認証と承認](time-series-insights-authentication-and-authorization.md)」を参照してください。 また、サンプルの先頭で定義されているすべての定数を正しく設定されていることを確認します。
1. ユーザーがアクセスできる環境の一覧を取得します。 環境の 1 つを関心のある環境として選択し、この環境のデータを照会します。
1. HTTPS 要求の例としては、関心のある環境の可用性データを要求します。
1. Web ソケット要求の例としては、関心のある環境のイベント集計データを要求します。 可用性の時間範囲全体のデータを要求します。

> [!NOTE]
> このコード例は [https://github.com/Azure-Samples/Azure-Time-Series-Insights](https://github.com/Azure-Samples/Azure-Time-Series-Insights/tree/master/csharp-tsi-ga-sample) にあります。

## <a name="project-dependencies"></a>プロジェクト依存関係

NuGet パッケージ `Microsoft.IdentityModel.Clients.ActiveDirectory` と `Newtonsoft.Json` を追加します。

## <a name="c-example"></a>C# の例

[!code-csharp[csharpquery-example](~/samples-tsi/csharp-tsi-ga-sample/Program.cs)]

## <a name="next-steps"></a>次の手順

- クエリの詳細については、[クエリ API リファレンス](/rest/api/time-series-insights/ga-query-api)を参照してください。

- Time Series Insights への [JavaScript シングルページ アプリの接続](tutorial-create-tsi-sample-spa.md)方法を参照してください。