---
title: Azure Active Directory ポータルの使用状況と分析情報のレポート | Microsoft Docs
description: Azure Active Directory ポータルの使用状況と分析情報のレポートの概要
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: daveba
editor: ''
ms.assetid: 3fba300d-18fc-4355-9924-d8662f563a1f
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.subservice: report-monitor
ms.date: 05/13/2019
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 3fe1e72d277bffd4bc9b38ac377e33b341967e17
ms.sourcegitcommit: 36c50860e75d86f0d0e2be9e3213ffa9a06f4150
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2019
ms.locfileid: "65804857"
---
# <a name="usage-and-insights-report-in-the-azure-active-directory-portal"></a>Azure Active Directory ポータルの使用状況と分析情報のレポート

使用状況と分析情報のレポートを使用すると、アプリケーションを中心にしてサインイン データを表示することができます。 次の質問への回答を導き出すことができます。

*   組織内で最もよく使われるアプリケーションはどれか。
*   サインインに最も失敗したアプリケーションはどれか。 
*   各アプリケーションの上位のサインイン エラーは何か。

## <a name="prerequisites"></a>前提条件 

使用状況と分析情報のレポートのデータにアクセスするには、次のものが必要です。

* Azure AD テナント
* サインイン データを表示するための Azure AD Premium (P1/P2) ライセンス
* グローバル管理者、セキュリティ管理者、セキュリティ閲覧者、またはレポート閲覧者のロールに含まれているユーザー。 さらに、任意のユーザー (非管理者) が自分のサインインにアクセス可能。 

## <a name="access-the-usage-and-insights-report"></a>使用状況と分析情報のレポートへのアクセス

1. [Azure Portal](https://portal.azure.com) に移動します。
2. 正しいディレクトリを選択して、 **[Azure Active Directory]** を選択し、 **[エンタープライズ アプリケーション]** を選択します。
3. **[アクティビティ]** セクションで、 **[使用状況と分析情報]** を選択してレポートを開きます。 

![使用状況と分析情報のレポート](./media/concept-usage-insights-report/main-menu.png)
                                     

## <a name="use-the-report"></a>レポートを使用する

使用状況と分析情報のレポートには、1 回以上サインインを試行したアプリケーションの一覧が表示され、成功したサインインの数、失敗したサインインの数、および成功率で並べ替えることができます。

一覧の下部にある [さらに読みこむ] をクリックすると、ページにその他のアプリケーションを表示することができます。 日付範囲を選択して、その範囲内で使用されたすべてのアプリケーションを表示することができます。

また、特定のアプリケーションにフォーカスを設定することもできます。 一定時間にわたるサインイン アクティビティと上位のエラーを表示するには、 **[サインイン アクティビティを表示する]** を選択します。  

アプリケーション使用状況グラフ内の日付を選択すると、アプリケーションのサインイン アクティビティの詳細な一覧が表示されます。  

![使用状況と分析情報のレポート](./media/concept-usage-insights-report/usage-and-insights-report.png)

## <a name="next-steps"></a>次の手順

* [サインイン レポート](concept-sign-ins.md)