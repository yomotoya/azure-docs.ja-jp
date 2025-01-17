---
title: Microsoft Authentication Library for .NET を使用してトークン キャッシュをクリアする | Azure
description: Microsoft Authentication Library for .NET (MSAL.NET) を使用してトークン キャッシュをクリアする方法を説明します。
services: active-directory
documentationcenter: dev-center-name
author: rwike77
manager: CelesteDG
editor: ''
ms.service: active-directory
ms.subservice: develop
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/07/2019
ms.author: ryanwi
ms.reviewer: saeeda
ms.custom: aaddev
ms.collection: M365-identity-device-management
ms.openlocfilehash: c6763c6b2b1f9b4de7d8669a50a4979a7aac00c7
ms.sourcegitcommit: f6c85922b9e70bb83879e52c2aec6307c99a0cac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/11/2019
ms.locfileid: "65544118"
---
# <a name="clear-the-token-cache-using-msalnet"></a>MSAL.NET を使用してトークン キャッシュをクリアする

Microsoft Authentication Library for .NET (MSAL.NET) を使用して[アクセス トークンを取得](msal-acquire-cache-tokens.md)すると、トークンはキャッシュされます。 トークンが必要な場合に、アプリケーションは最初に `AcquireTokenSilent` メソッドを呼び出して、キャッシュ内に利用可能なトークンがあるかどうかを確認します。 

キャッシュのクリアは、キャッシュからアカウントを削除することによって行います。 ただし、これによってブラウザーにあるセッション Cookie が削除されることはありません。  次の例は、パブリック クライアント アプリケーションをインスタンス化し、アプリケーションのアカウントを取得してから、アカウントを削除します。

```csharp
private readonly IPublicClientApplication _app;
private static readonly string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
private static readonly string Authority = string.Format(CultureInfo.InvariantCulture, AadInstance, Tenant);

_app = PublicClientApplicationBuilder.Create(ClientId)
                .WithAuthority(Authority)
                .Build();

var accounts = (await _app.GetAccountsAsync()).ToList();

// clear the cache
while (accounts.Any())
{
   await _app.RemoveAsync(accounts.First());
   accounts = (await _app.GetAccountsAsync()).ToList();
}

```

トークンの取得とキャッシュの詳細については、[アクセス トークンの取得](msal-acquire-cache-tokens.md)に関するページを参照してください。
