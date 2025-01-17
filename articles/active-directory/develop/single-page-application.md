---
title: Azure Active Directory のシングルページ アプリケーション
description: シングルページ アプリケーション (SPA) の概要、この種のアプリのプロトコル フロー、登録、およびトークンの有効期限の基本について説明します。
services: active-directory
documentationcenter: ''
author: rwike77
manager: CelesteDG
editor: ''
ms.service: active-directory
ms.subservice: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/24/2018
ms.author: ryanwi
ms.reviewer: saeeda, jmprieur, andret
ms.custom: aaddev
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f6f66779bec9ed4e38e5a662c2d3728ba2034b6
ms.sourcegitcommit: f6c85922b9e70bb83879e52c2aec6307c99a0cac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/11/2019
ms.locfileid: "65545292"
---
# <a name="single-page-applications"></a>シングルページ アプリケーション

通常、シングルページ アプリケーション (SPA) は、ブラウザーで実行される JavaScript プレゼンテーション レイヤー (フロント エンド) と、サーバー上で実行され、アプリケーションのビジネス ロジックを実装する Web API バックエンドとして構成されます。暗黙的な承認許可の詳細と、実際のアプリケーションのシナリオに適しているかどうかを判断するために役立つ情報については、「[Azure Active Directory (AD) での OAuth2 の暗黙的な許可フローについて](v1-oauth2-implicit-grant-flow.md)」を参照してください。

このシナリオでは、ユーザーがサインインすると、JavaScript フロントエンドが [Active Directory Authentication Library for JavaScript (ADAL.JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js) と暗黙的な認証付与を使用して、Azure AD から ID トークン (id_token) を取得します。 トークンがキャッシュされ、クライアントは、OWIN ミドルウェアを使用して保護された Web API バックエンドを呼び出すときに、トークンをベアラー トークンとして要求に添付します。

## <a name="diagram"></a>ダイアグラム

![シングルページ アプリケーション ダイアグラム](./media/authentication-scenarios/single_page_app.png)

## <a name="protocol-flow"></a>プロトコル フロー

1. ユーザーが Web アプリケーションに移動します。
1. アプリケーションが JavaScript フロントエンド (プレゼンテーション層) をブラウザーに返します。
1. ユーザーが、たとえばサインイン リンクをクリックして、サインインを開始します。 ブラウザーが Azure AD 認証エンドポイントに GET を送信して ID トークンを要求します。 この要求では、クエリ パラメーターにアプリケーション ID と応答 URL が含まれています。
1. Azure AD が、Azure Portal で構成された登録済みの応答 URL と照合して応答 URL を検証します。
1. ユーザーがサインイン ページでサインインします。
1. 認証が成功すると、Azure AD が ID トークンを作成し、URL フラグメント (#) としてアプリケーションの応答 URL に返します。 実稼働アプリケーションでは、この応答 URL は HTTPS である必要があります。 返されたトークンには、トークンを検証するためにアプリケーションが必要とする、ユーザーと Azure AD に関する要求が含まれています。
1. ブラウザーで実行されている JavaScript クライアント コードが、アプリケーションの Web API バックエンドの呼び出しの保護に使用するために、トークンを応答から抽出します。
1. ブラウザーが承認ヘッダーに ID トークンを含めて、アプリケーションの Web API バックエンドを呼び出します。 Azure AD 認証サービスは、リソースがクライアント ID と同じである場合、ベアラー トークンとして使用できる ID トークンを発行します (この場合、Web API がアプリ自身のバックエンドであるため、これが該当します)。

## <a name="code-samples"></a>コード サンプル

[シングルページ アプリケーションのシナリオのコード サンプル](sample-v1-code.md#single-page-applications)を参照してください。 新しいサンプルが頻繁に追加されているので、頻繁に確認してください。

## <a name="app-registration"></a>アプリの登録

* シングル テナント: 自分の組織だけが使用するアプリケーションを構築している場合は、Azure portal を使用して、アプリケーションを会社のディレクトリに登録する必要があります。
* マルチテナント: 組織の外部のユーザーが使用できるアプリケーションを構築している場合は、アプリケーションを会社のディレクトリに登録するだけでなく、そのアプリケーションを使用する各組織のディレクトリにも登録する必要があります。 ディレクトリ内でアプリケーションを使用できるようにするには、ユーザーがアプリケーションに同意できるようにするためのサインアップ プロセスを含めます。 ユーザーがアプリケーションにサインアップするときに、アプリケーションが必要とするアクセス許可と同意オプションを示すダイアログが表示されます。 必要なアクセス許可によっては、他の組織の管理者が同意することが必要な場合があります。 ユーザーまたは管理者が同意すると、アプリケーションがディレクトリに登録されます。

アプリケーションの登録後、OAuth 2.0 暗黙的な許可プロトコルを使用するようにアプリケーションを構成する必要があります。 既定では、このプロトコルはアプリケーションで無効になっています。 アプリケーションで OAuth2 暗黙的な許可プロトコルを有効にするには、Azure portal でそのアプリケーション マニフェストを編集し、"oauth2AllowImplicitFlow" 値を true に設定します。 詳細については、[アプリケーション マニフェスト](reference-app-manifest.md)に関するページを参照してください。

## <a name="token-expiration"></a>トークンの有効期限

ADAL.js を使用すると、以下の場合に役立ちます。

* 期限切れのトークンを更新する
* Web API リソースを呼び出すアクセス トークンを要求する

認証に成功すると、Azure AD はユーザーのブラウザーに Cookie を書き込んでセッションを確立します。 ユーザーと Azure AD の間にセッションが存在することに注意してください (ユーザーと Web アプリケーションの間ではありません)。 トークンの有効期限が切れると、ADAL.js はこのセッションを使用して、ダイアログを表示せずに別のトークンを取得します。 ADAL.js は非表示の iFrame を使用し、OAuth 暗黙的な許可プロトコルを使用して要求を送受信します。 アプリケーションが呼び出す他の Web API リソースが、クロス オリジン リソース共有 (CORS) をサポートし、ユーザーのディレクトリに登録されており、サインイン時にユーザーから必要な同意を得られていれば、ADAL.js は同じメカニズムを使用して、ダイアログを表示せずに、それらのリソースのアクセス トークンを取得することもできます。

## <a name="next-steps"></a>次の手順

* その他の[アプリケーションの種類とシナリオ](app-types.md)について学習する
* Azure AD [認証の基本](authentication-scenarios.md)について学習する
