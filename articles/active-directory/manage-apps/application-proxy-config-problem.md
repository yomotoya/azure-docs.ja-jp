---
title: アプリケーション プロキシ アプリケーションの作成時に発生する問題 | Microsoft Docs
description: Azure AD 管理ポータルでアプリケーション プロキシ アプリケーションを作成する際に発生する問題のトラブルシューティング方法
services: active-directory
documentationcenter: ''
author: msmimart
manager: CelesteDG
ms.assetid: ''
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: mimart
ms.reviewer: asteen
ms.collection: M365-identity-device-management
ms.openlocfilehash: 104b98cba0948ec5d0896877e54eab1e7cd4049f
ms.sourcegitcommit: be9fcaace62709cea55beb49a5bebf4f9701f7c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65825814"
---
# <a name="problem-creating-an-application-proxy-application"></a>アプリケーション プロキシ アプリケーションの作成時に発生する問題 

ここでは、新しいアプリケーション プロキシ アプリケーションを作成する際によく発生する問題をいくつか取り上げます。

## <a name="recommended-documents"></a>推奨されるドキュメント 

管理ポータルでのアプリケーション プロキシ アプリケーションの作成の詳細については、「[Azure AD アプリケーション プロキシを使用したアプリケーションの発行](application-proxy-add-on-premises-application.md)」を参照してください。

同ドキュメントの手順に従ってアプリケーションを作成しているときにエラーが発生した場合、アプリケーションの修復方法に関する情報や推奨事項については、そのエラーの詳細を見て確認してください。 ほとんどのエラー メッセージには、推奨される解決方法が記載されています。 

## <a name="specific-things-to-check"></a>具体的なチェック項目

一般的なエラーを避けるために、以下の点を確認してください。

-   アプリケーション プロキシ アプリケーションする権限を持った管理者であること。

-   内部 URL が一意であること。

-   外部 URL が一意であること。

-   URL が http または https から始まり、"/" で終わっていること。

-   URL がドメイン名であって IP アドレスではないこと。

アプリケーションを作成する際、エラー メッセージは右上隅に表示されます。 通知アイコンを選択してエラー メッセージを表示することもできます。

   ![通知アイコン](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a>次の手順
[Azure Portal でアプリケーション プロキシを有効にする](application-proxy-add-on-premises-application.md)
