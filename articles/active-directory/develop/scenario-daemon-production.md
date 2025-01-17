---
title: Web API を呼び出すデーモン アプリ (運用環境への移行) - Microsoft ID プラットフォーム
description: Web API を呼び出すデーモン アプリを構築する方法 (運用環境への移行) について説明します
services: active-directory
documentationcenter: dev-center-name
author: jmprieur
manager: CelesteDG
editor: ''
ms.service: active-directory
ms.subservice: develop
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/07/2019
ms.author: jmprieur
ms.custom: aaddev
ms.collection: M365-identity-device-management
ms.openlocfilehash: 627dab0cb23800664c5fb5b3df9c61f5071d4b87
ms.sourcegitcommit: f6c85922b9e70bb83879e52c2aec6307c99a0cac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/11/2019
ms.locfileid: "65545403"
---
# <a name="daemon-app-that-calls-web-apis---move-to-production"></a>Web API を呼び出すデーモン アプリ - 運用環境への移行

これでトークンを取得してサービス間の呼び出しに使用する方法がわかったので、運用環境にアプリを移行する方法について説明します。

## <a name="deployment---case-of-multi-tenant-daemon-apps"></a>デプロイ - マルチテナント デーモン アプリの場合

複数のテナントで実行できるデーモン アプリケーションを作成している ISV では、テナントによって確実に以下の管理を行う必要があります。

- アプリケーション用にサービス プリンシパルをプロビジョニングする
- アプリケーションへの同意を許可する

顧客に対しては、これらの操作の実行方法を説明する必要があります。 詳しくは、「[テナント全体の同意を要求する](v2-permissions-and-consent.md#requesting-consent-for-an-entire-tenant)」をご覧ください。

[!INCLUDE [Move to production common steps](../../../includes/active-directory-develop-scenarios-production.md)]

## <a name="next-steps"></a>次の手順

以下に、詳細を学習できるリンクをいくつか示します。

### <a name="net"></a>.NET

- まだ行っていない場合は、クイック スタートの「[トークンを取得し、コンソール アプリからアプリの ID を使用して Microsoft Graph API を呼び出す](./quickstart-v2-netcore-daemon.md)」を試してください。
- 以下に関するリファレンス ドキュメント:
  - [ConfidentialClientApplication](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.confidentialclientapplicationbuilder) のインスタンス化
  - [AcquireTokenForClient](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.acquiretokenforclientparameterbuilder) の呼び出し
- 他のサンプル/チュートリアル:
  - [microsoft-identity-platform-console-daemon](https://github.com/Azure-Samples/microsoft-identity-platform-console-daemon) では、Microsoft Graph を照会しているテナントのユーザーを表示するシンプルな .NET Core デーモン コンソール アプリケーションを取り上げています。

    ![トポロジ](media/scenario-daemon-app/daemon-app-sample.svg)

    同じサンプルには、証明書を利用したバリエーションも示されています。

    ![トポロジ](media/scenario-daemon-app/daemon-app-sample-with-certificate.svg)

  - [microsoft-identity-platform-aspnet-webapp-daemon](https://github.com/Azure-Samples/microsoft-identity-platform-aspnet-webapp-daemon) では、ユーザーの代理ではなく、アプリケーションの ID を使用して Microsoft Graph からのデータを同期する ASP.NET MVC の Web アプリケーションを取り上げています。 サンプルには、管理者の同意プロセスも示されています。

    ![トポロジ](media/scenario-daemon-app/damon-app-sample-web.svg)

### <a name="python"></a>Python

MSAL Python は現在、パブリック プレビュー段階です。 詳しい情報については、[MSAL Python クライアント資格情報のリポジトリ内のサンプル](https://github.com/AzureAD/azure-activedirectory-library-for-python/blob/dev/sample/client_credentials_sample.py)に関するページをご覧ください。

### <a name="java"></a>Java

MSAL Python は現在、パブリック プレビュー段階です。 詳しい情報については、[MSAL Java のリポジトリ内のサンプル](https://github.com/AzureAD/azure-activedirectory-library-for-java/tree/dev/src/samples)に関するページをご覧ください。