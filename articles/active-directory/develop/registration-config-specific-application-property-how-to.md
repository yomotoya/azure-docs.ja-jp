---
title: 独自に開発したアプリケーションの特定のフィールドを指定する方法 | Microsoft Docs
description: 独自に開発したアプリケーションを Azure AD に登録する際に特定のフィールドを指定する方法についてのガイダンス
services: active-directory
documentationcenter: ''
author: rwike77
manager: CelesteDG
ms.assetid: ''
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/11/2018
ms.author: ryanwi
ms.collection: M365-identity-device-management
ms.openlocfilehash: a8b93f26080229e980b680c157f59db4edf33e7a
ms.sourcegitcommit: f6c85922b9e70bb83879e52c2aec6307c99a0cac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/11/2019
ms.locfileid: "65545494"
---
# <a name="how-to-fill-out-specific-fields-for-a-custom-developed-application"></a>独自に開発したアプリケーションの特定のフィールドを指定する方法

この記事では、[Azure portal](https://portal.azure.com) のアプリケーション登録フォームで使用できるすべてのフィールドについて簡単に説明します。

## <a name="register-a-new-application"></a>新しいアプリケーションの登録

-   新しいアプリケーションを登録するには、[Azure Portal](https://portal.azure.com) に移動します。

-   左側のナビゲーション ウィンドウで、**[Azure Active Directory]** をクリックします。

-   **[アプリの登録]** を選択して、**[追加]** をクリックします。

-   アプリケーション登録フォームが開きます。

## <a name="fields-in-the-application-registration-form"></a>アプリケーション登録フォームのフィールド


| フィールド            | 説明                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| Name             | アプリケーションの名前です。 4 文字以上にする必要があります。                |
| アプリケーションの種類 | **Web アプリ/Web API**:Web アプリケーションまたは Web API、あるいはその両方を表すアプリケーションを追加します。 
| |**ネイティブ**:ユーザーのデバイスまたはコンピューターにインストールできるアプリケーションです。           |
| [サインオン URL]      | アプリケーションを使用するためにユーザーがサインインする URL です。                                  |

上記のフィールドに入力すると、Azure portal でアプリケーションの登録が行われ、アプリケーション ページにリダイレクトされます。 アプリケーション ウィンドウの **[設定]** ボタンをクリックすると、[設定] ページが開きます。このページには、アプリケーションをカスタマイズするためのその他のフィールドが表示されます。 次の表では、[設定] ページのすべてのフィールドについて説明します。 Web アプリケーションとネイティブ アプリケーションのどちらを作成したかに応じて、これらのフィールドの一部のみが表示されることに注意してください。

| フィールド           | 説明                                                                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| アプリケーション ID  | アプリケーションを登録すると、Azure AD によってそのアプリケーションにアプリケーション ID が割り当てられます。 このアプリケーション ID は、Azure AD に対する認証要求でアプリケーションを一意に識別するために使用できるほか、Graph API などのリソースにアクセスするためにも使用できます。                                                          |
| アプリケーション ID/URI      | これは一意の URI である必要があります (通常は **https://&lt;tenant\_name&gt;/&lt;application\_name&gt; という形式**)。 これは、トークンの発行対象であるリソースを指定するための一意の識別子として承認付与フロー中に使用されます。 発行されたアクセス トークンの "aud" 要求にもなります。 |
| 新しいロゴのアップロード | これを使用すると、アプリケーションのロゴをアップロードできます。 ロゴの形式は .bmp、.jpg、.png のいずれかにし、ファイル サイズは 100 KB 未満にする必要があります。 イメージのサイズは 215 x 215 ピクセル、中央のイメージのサイズは 94 x 94 ピクセルにする必要があります。                                                       |
| ホーム ページ URL   | これは、アプリケーション登録時に指定されるサインオン URL です。                                                                                                                                                                                                                                              |
| ログアウト URL      | これは、シングル サインアウトのログアウト URL です。 登録されているその他のアプリケーションを使用してユーザーが Azure AD とのセッションを消去した場合、Azure AD はログアウト要求をこの URL に送信します。                                                                                                                                       |
| マルチテナント  | このスイッチでは、アプリケーションが複数のテナントで使えるかどうかを指定します。 通常、マルチテナントを有効にすると、お客様のアプリケーションを外部組織が使用できるようになります。このとき、外部組織は自社のテナントにアプリケーションを登録して、自社のデータへのアクセスを許可します。                                                                   |
| 応答 URL      | 応答 URL は、アプリケーションによって要求されたトークンを Azure AD が返すエンドポイントです。                                                                                                                                                                                                          |
| リダイレクト URI   | ネイティブ アプリケーションの場合、ユーザーは承認が成功した後にこの URI に移動します。 Azure AD は、OAuth 2.0 要求でアプリケーションが使用したリダイレクト URI が、ポータルに登録されている値のいずれかと一致していることを確認します。                                                            |
| 構成する            | キーを作成すると、Azure AD によってセキュリティ保護された Web API にプログラムでアクセスすることができ、ユーザーの操作が不要になります。 \*\*[キー]\*\* ページでキーの説明と有効期限を入力して保存し、キーを生成します。 後でアクセスすることができないため、安全な場所に保存してください。             |

## <a name="next-steps"></a>次の手順
[Azure Active Directory でのアプリケーションの管理](../manage-apps/what-is-application-management.md)
