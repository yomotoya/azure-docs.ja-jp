---
title: アクセス パネルからアプリケーションへのサインインに関する問題 | Microsoft Docs
description: myapps.microsoft.com の Microsoft Azure AD アクセス パネルからアプリケーションへのアクセスに関する問題をトラブルシューティングする方法
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
ms.date: 07/11/2017
ms.author: mimart
ms.reviewer: japere
ms.collection: M365-identity-device-management
ms.openlocfilehash: 51e486e8eb2fef04c1b876dff3de644dda4aaf2e
ms.sourcegitcommit: 36c50860e75d86f0d0e2be9e3213ffa9a06f4150
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2019
ms.locfileid: "65781130"
---
# <a name="problems-signing-in-to-an-application-from-the-access-panel"></a>アクセス パネルからアプリケーションへのサインインに関する問題

Web ベースのポータルであるアクセス パネルを使用すると、Azure Active Directory (Azure AD) の職場または学校アカウントを持つユーザーは、Azure AD 管理者によってアクセスを許可されたクラウドベースのアプリケーションを表示および起動することができます。 

これらのアプリケーションは、Azure AD ポータルでユーザーのために構成されます。 アクセス パネルでアプリケーションを表示するには、アプリケーションが正しく構成され、ユーザーまたはユーザーがメンバーであるグループに割り当てられている必要があります。

ユーザーに表示されるアプリの種類は、次のカテゴリに分類されます。

-   Office 365 アプリケーション

-   フェデレーション ベースの SSO で構成されたマイクロソフトとサード パーティのアプリケーション

-   パスワードベースの SSO アプリケーション

-   既存の SSO ソリューションのアプリケーション

## <a name="general-issues-to-check-first"></a>最初に確認する一般的な問題

-   アクセス パネルの最小要件を満たす**ブラウザー**を使用していることを確認します。

-   ユーザーのブラウザーが、その**信頼済みサイト**にアプリケーションの URL を追加していることを確認します。

-   アプリケーションが正しく**構成**されていることを確認します。

-   ユーザーのアカウントがサインイン用に**有効になっている**ことを確認します。

-   ユーザーのアカウントが**ロックアウトされていない**ことを確認します。

-   ユーザーの**パスワードが期限切れになったり、忘れられたりしていない**ことを確認します。

-   **多要素認証**がユーザー アクセスをブロックしていないことを確認します。

-   **条件付きアクセス ポリシー**または **ID 保護**ポリシーがユーザー アクセスをブロックしていないことを確認します。

-   ユーザーの**認証の連絡先情報**が最新のものであり、多要素認証または条件付きアクセス ポリシーを適用できることを確認します。

-   ブラウザーの Cookie を削除してから、再度サインインを試行して、サインインできることを確認します。

## <a name="meeting-browser-requirements-for-the-access-panel"></a>アクセス パネルのブラウザーの要件を満たす

アクセス パネルには、JavaScript をサポートする CSS 対応のブラウザーが必要です。 アクセス パネルでパスワード ベースのシングル サインオン (SSO) を使用するためには、ユーザーのブラウザーにアクセス パネルの拡張機能をインストールする必要があります。 このアクセス パネルの拡張機能は、ユーザーがパスワード ベースの SSO 用に構成されているアプリケーションを選択したときに、自動的にダウンロードされます。

パスワードベースの SSO の場合、エンド ユーザーのブラウザーには次のいずれかを使用できます。

-   Internet Explorer 8、9、10、11 - Windows 7 以降

-   Microsoft Edge - Windows 10 Anniversary Edition 以降

-   Chrome - Windows 7 以降、MacOS X 以降

-   Firefox 26.0 以降 - Windows XP SP2 以降、Mac os X 10.6 以降

## <a name="how-to-install-the-access-panel-browser-extension"></a>アクセス パネルのブラウザー拡張機能をインストールする方法

アクセス パネルのブラウザー拡張機能をインストールするには、次の手順に従います。

1.  サポートされている任意のブラウザーで、[アクセス パネル](https://myapps.microsoft.com)を開き、Azure AD の**ユーザー**としてサインインします。

2.  アクセス パネルで、**パスワード SSO アプリケーション**をクリックします。

3.  ソフトウェアのインストールを確認するプロンプトで、**[今すぐインストール]** を選択します。

4.  お使いのブラウザーに基づいて、ダウンロード リンクが表示されます。 お使いのブラウザーに拡張機能を**追加**します。

5.  お使いのブラウザーに確認メッセージが表示されたら、拡張機能を **[有効にする]** または **[許可する]** のいずれかを選択します。

6.  インストールが完了したら、ブラウザー セッションを**再起動**します。

7.  アクセス パネルにサインインし、パスワード SSO アプリケーションを**起動**できるかどうかを確認します。

以下のダイレクト リンクから、Chrome および Microsoft Edge 対応の拡張機能をダウンロードすることもできます。

-   [Chrome アクセス パネル拡張機能](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Microsoft Edge アクセス パネル拡張機能](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Azure AD ギャラリー アプリケーションのフェデレーション シングル サインオンを構成する方法

Enterprise Single Sign-On 機能が有効になっている Azure AD ギャラリー内のすべてのアプリケーションには、ステップ バイ ステップ チュートリアルが用意されています。 [「SaaS アプリと Azure Active Directory を統合する方法に関するチュートリアルの一覧」](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)にアクセスして、詳しいステップ バイ ステップ ガイダンスを参照できます。

Azure AD ギャラリーからアプリケーションを構成するには、以下の手順を実行する必要があります。

-   Azure AD ギャラリーからアプリケーションを追加する

-   [Azure AD で、アプリケーションのメタデータ値を構成する (サインオン URL、識別子、応答 URL)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [ユーザー識別子を選択し、アプリケーションに送信するためのユーザー属性を追加する](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD メタデータと証明書を取得する](#download-the-azure-ad-metadata-or-certificate)

-   [アプリケーションで Azure AD メタデータ値を構成する (サインオン URL、発行者、ログアウト URL、証明書)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   アプリケーションにユーザーを割り当てる

### <a name="add-an-application-from-the-azure-ad-gallery"></a>Azure AD ギャラリーからアプリケーションを追加する

Azure AD ギャラリーからアプリケーションを追加するには、次の手順に従います。

1.  [Azure Portal](https://portal.azure.com) を開き、**グローバル管理者**または**共同管理者**としてサインインします。

2.  左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3.  フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4.  Azure Active Directory の左側のナビゲーション メニューから **[エンタープライズ アプリケーション]** をクリックします。

5.  **[エンタープライズ アプリケーション]** ウィンドウの右上隅にある **[追加]** ボタンをクリックします。

6.  **[ギャラリーから追加する]** セクションの **[名前を入力してください]** テキスト ボックスで、アプリケーションの名前を入力します

7.  シングル サインオンを構成するアプリケーションを選択します。

8.  アプリケーションを追加する前に、**[名前]** ボックスで名前を変更できます。

9.  **[追加]** ボタンをクリックして、アプリケーションを追加します。

しばらくすると、アプリケーションの構成ウィンドウが表示されます。

### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a>Azure AD ギャラリーからアプリケーションのシングル サインオンを構成する

アプリケーションのシングル サインオンを構成するには、次の手順に従います。

1. <span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>[**Azure Portal**](https://portal.azure.com/) を開き、**グローバル管理者**または**共同管理者**としてサインインします。

2. 左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3. フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4. Azure Active Directory の左側のナビゲーション メニューから **[エンタープライズ アプリケーション]** をクリックします。

5. **[すべてのアプリケーション]** をクリックして、すべてのアプリケーションの一覧を表示します。

   * ここに表示したいアプリケーションが表示されない場合は、**[All Applications List (すべてのアプリケーション リスト)]** の上部にある **[フィルター]** コントロールを使用して、**[表示]** オプションを **[すべてのアプリケーション]** に設定します。

6. シングル サインオンを構成するアプリケーションを選択します。

7. アプリケーションが読み込まれたら、アプリケーションの左側のナビゲーション メニューから **[シングル サインオン]** をクリックします。

8. **[モード]** ボックスの一覧から、**[SAML ベースのサインオン]** を選択します。

9. **[ドメインと URL]** に必要な値を入力します。 これらの値は、アプリケーション ベンダーから取得する必要があります。

   1. SP によって開始された SSO としてアプリケーションを構成するには、サインオン URL が必要な値です。 一部のアプリケーションでは、識別子も必要な値になります。

   2. IdP によって開始された SSO としてアプリケーションを構成するには、応答 URL が必要な値です。 一部のアプリケーションでは、識別子も必要な値になります。

10. **省略可能:** 必須ではない値を表示する場合は、**[詳細な URL 設定の表示]** をクリックしてください。

11. **[ユーザー属性]** で、**[ユーザー識別子]** ボックスの一覧からユーザーの一意の識別子を選択します。

12. **省略可能:** **[その他のすべてのユーザー属性を表示および編集する]** をクリックして、ユーザーがサインインするときに SAML トークンでアプリケーションに送信される属性を編集します。

    属性を追加するには、次の手順に従います。

    1. **[属性の追加]** をクリックします。 **[名前]** を入力し、ドロップダウンから **[値]** を選択します。

    2. **[保存]** をクリックします。 テーブルに新しい属性が表示されます。

13. アプリケーションでシングル サインオンを構成する方法に関するドキュメントにアクセスするには、**[&lt;アプリケーション名&gt; の構成]** をクリックします。 アプリケーションで SSO を設定するために必要なメタデータ URL と証明書も用意されています。

14. **[保存]** をクリックして構成を保存します。

15. アプリケーションにユーザーを割り当てます。

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a>ユーザー識別子を選択し、アプリケーションに送信するためのユーザー属性を追加する

ユーザー識別子を選択したり、ユーザー属性を追加したりするには、次の手順に従います。

1. [**Azure Portal**](https://portal.azure.com/) を開き、**グローバル管理者**または**共同管理者**としてサインインします。

2. 左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3. フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4. Azure Active Directory の左側のナビゲーション メニューから **[エンタープライズ アプリケーション]** をクリックします。

5. **[すべてのアプリケーション]** をクリックして、すべてのアプリケーションの一覧を表示します。

   * ここに表示したいアプリケーションが表示されない場合は、**[All Applications List (すべてのアプリケーション リスト)]** の上部にある **[フィルター]** コントロールを使用して、**[表示]** オプションを **[すべてのアプリケーション]** に設定します。

6. シングル サインオンを構成したアプリケーションを選択します。

7. アプリケーションが読み込まれたら、アプリケーションの左側のナビゲーション メニューから **[シングル サインオン]** をクリックします。

8. **[ユーザー属性]** セクションで、**[ユーザー識別子]** ボックスの一覧からユーザーの一意の識別子を選択します。 選択したオプションは、ユーザーを認証するアプリケーションで想定されている値と一致する必要があります。

   >[!NOTE]
   >Azure AD は、選択した値に基づく NameID 属性 (ユーザー ID) の形式、または SAML AuthRequest でアプリケーションによって要求された形式を選択します。 詳細については、「[シングル サインオンの SAML プロトコル](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)」の「NameIDPolicy」セクションを参照してください。
   >
   >

9. ユーザー属性を追加するには、**[その他のすべてのユーザー属性を表示および編集する]** をクリックして、ユーザーがサインインするときに SAML トークンでアプリケーションに送信される属性を編集します。

   属性を追加するには、次の手順に従います。

   1. **[属性の追加]** をクリックします。 **[名前]** を入力し、ドロップダウンから **[値]** を選択します。

   2. **[保存]** をクリックします。 テーブルに新しい属性が表示されます。

### <a name="download-the-azure-ad-metadata-or-certificate"></a>Azure AD メタデータまたは証明書をダウンロードする

Azure AD からアプリケーションのメタデータまたは証明書をダウンロードするには、次の手順に従います。

1. [**Azure Portal**](https://portal.azure.com/) を開き、**グローバル管理者**または**共同管理者**としてサインインします。

2. 左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3. フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4. Azure Active Directory の左側のナビゲーション メニューから **[エンタープライズ アプリケーション]** をクリックします。

5. **[すべてのアプリケーション]** をクリックして、すべてのアプリケーションの一覧を表示します。

   * ここに表示したいアプリケーションが表示されない場合は、**[All Applications List (すべてのアプリケーション リスト)]** の上部にある **[フィルター]** コントロールを使用して、**[表示]** オプションを **[すべてのアプリケーション]** に設定します。

6. シングル サインオンを構成したアプリケーションを選択します。

7. アプリケーションが読み込まれたら、アプリケーションの左側のナビゲーション メニューから **[シングル サインオン]** をクリックします。

8. **[SAML 署名証明書]** セクションに移動して、**[ダウンロード]** 列の値をクリックします。 アプリケーションでシングル サインオンを構成するために何が必要かに応じて、メタデータ XML または証明書をダウンロードするオプションが表示されます。

   Azure AD には、メタデータを取得する URL は用意されていません。 メタデータは、XML ファイルとしてのみ取得できます。

## <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a>ギャラリー以外のアプリケーションのフェデレーション シングル サインオンを構成する方法

ギャラリー以外のアプリケーションを構成するには、Azure AD Premium を用意する必要があり、アプリケーションが SAML 2.0 をサポートする必要があります。 Azure AD のバージョンの詳細については、[Azure AD の価格](https://azure.microsoft.com/pricing/details/active-directory/)に関するページを参照してください。

-   Azure AD で、アプリケーションのメタデータ値を構成する (サインオン URL、識別子、応答 URL)

-   [ユーザー識別子を選択し、アプリケーションに送信するためのユーザー属性を追加する](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Azure AD メタデータと証明書を取得する](#download-the-azure-ad-metadata-or-certificate)

-   アプリケーションで Azure AD メタデータ値を構成する (サインオン URL、発行者、ログアウト URL、証明書)

### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Azure AD で、アプリケーションのメタデータ値を構成する (サインオン URL、識別子、応答 URL)

Azure AD ギャラリーに含まれていないアプリケーションのシングル サインオンを構成するには、次の手順に従います。

1. [**Azure Portal**](https://portal.azure.com/) を開き、**グローバル管理者**または**共同管理者**としてサインインします。

2. 左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3. フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4. Azure Active Directory の左側のナビゲーション メニューから **[エンタープライズ アプリケーション]** をクリックします。

5. **[エンタープライズ アプリケーション]** ウィンドウの右上隅にある **[追加]** ボタンをクリックします。

6. **[独自のアプリを追加する]** セクションで、**[ギャラリー以外のアプリケーション]** をクリックします。

7. **[名前]** ボックスに、アプリケーションの名前を入力します。

8. **[追加]** ボタンをクリックして、アプリケーションを追加します。

9. アプリケーションが読み込まれたら、アプリケーションの左側のナビゲーション メニューから **[シングル サインオン]** をクリックします。

10. **[モード]** ドロップダウンから、**[SAML ベース サインオン]** を選択します。

11. **[ドメインおよび URL]** に必要な値を入力します。 これらの値は、アプリケーション ベンダーから取得する必要があります。

    1. IdP によって開始された SSO としてアプリケーションを構成するには、応答 URL と識別子を入力します。

    2. **省略可能:** SP によって開始された SSO としてアプリケーションを構成するには、サインオン URL が必要な値です。

12. **[ユーザー属性]** で、**[ユーザー識別子]** ボックスの一覧からユーザーの一意の識別子を選択します。

13. **省略可能:** **[その他のすべてのユーザー属性を表示および編集する]** をクリックして、ユーザーがサインインするときに SAML トークンでアプリケーションに送信される属性を編集します。

    属性を追加するには、次の手順に従います。

    1. **[属性の追加]** をクリックします。 **[名前]** を入力し、ドロップダウンから **[値]** を選択します。

    2. **[保存]** をクリックします。 テーブルに新しい属性が表示されます。

14. アプリケーションでシングル サインオンを構成する方法に関するドキュメントにアクセスするには、**[&lt;アプリケーション名&gt; の構成]** をクリックします。 また、アプリケーションに必要な Azure AD URL と証明書が用意されています。

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a>ユーザー識別子を選択し、アプリケーションに送信するためのユーザー属性を追加する

ユーザー識別子を選択したり、ユーザー属性を追加したりするには、次の手順に従います。

1. [**Azure Portal**](https://portal.azure.com/) を開き、**グローバル管理者**または**共同管理者**としてサインインします。

2. 左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3. フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4. Azure Active Directory の左側のナビゲーション メニューから **[エンタープライズ アプリケーション]** をクリックします。

5. **[すべてのアプリケーション]** をクリックして、すべてのアプリケーションの一覧を表示します。

   * ここに表示したいアプリケーションが表示されない場合は、**[All Applications List (すべてのアプリケーション リスト)]** の上部にある **[フィルター]** コントロールを使用して、**[表示]** オプションを **[すべてのアプリケーション]** に設定します。

6. シングル サインオンを構成したアプリケーションを選択します。

7. アプリケーションが読み込まれたら、アプリケーションの左側のナビゲーション メニューから **[シングル サインオン]** をクリックします。

8. **[ユーザー属性]** セクションで、**[ユーザー識別子]** ボックスの一覧からユーザーの一意の識別子を選択します。 選択したオプションは、ユーザーを認証するアプリケーションで想定されている値と一致する必要があります。

   >[!NOTE]
   >Azure AD は、選択した値に基づく NameID 属性 (ユーザー ID) の形式、または SAML AuthRequest でアプリケーションによって要求された形式を選択します。 詳細については、「[シングル サインオンの SAML プロトコル](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)」の「NameIDPolicy」セクションを参照してください。
   >
   >

9. ユーザー属性を追加するには、**[その他のすべてのユーザー属性を表示および編集する]** をクリックして、ユーザーがサインインするときに SAML トークンでアプリケーションに送信される属性を編集します。

   属性を追加するには、次の手順に従います。

   1. **[属性の追加]** をクリックします。 **[名前]** を入力し、ドロップダウンから **[値]** を選択します。

   2. **[保存]** をクリックします。 テーブルに新しい属性が表示されます。

### <a name="download-the-azure-ad-metadata-or-certificate"></a>Azure AD メタデータまたは証明書をダウンロードする

Azure AD からアプリケーションのメタデータまたは証明書をダウンロードするには、次の手順に従います。

1. [**Azure Portal**](https://portal.azure.com/) を開き、**グローバル管理者**または**共同管理者**としてサインインします。

2. 左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3. フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4. Azure Active Directory の左側のナビゲーション メニューから **[エンタープライズ アプリケーション]** をクリックします。

5. **[すべてのアプリケーション]** をクリックして、すべてのアプリケーションの一覧を表示します。

   * ここに表示したいアプリケーションが表示されない場合は、**[All Applications List (すべてのアプリケーション リスト)]** の上部にある **[フィルター]** コントロールを使用して、**[表示]** オプションを **[すべてのアプリケーション]** に設定します。

6. シングル サインオンを構成したアプリケーションを選択します。

7. アプリケーションが読み込まれたら、アプリケーションの左側のナビゲーション メニューから **[シングル サインオン]** をクリックします。

8. **[SAML 署名証明書]** セクションに移動して、**[ダウンロード]** 列の値をクリックします。 アプリケーションでシングル サインオンを構成するために何が必要かに応じて、メタデータ XML または証明書をダウンロードするオプションが表示されます。

   Azure AD には、メタデータを取得する URL は用意されていません。 メタデータは、XML ファイルとしてのみ取得できます。

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Azure AD ギャラリー アプリケーションのパスワード シングル サインオンを構成する方法

Azure AD ギャラリーからアプリケーションを構成するには、以下の手順を実行する必要があります。

-   Azure AD ギャラリーからアプリケーションを追加する

-   パスワード シングル サインオンに対応するようにアプリケーションを構成する

### <a name="add-an-application-from-the-azure-ad-gallery"></a>Azure AD ギャラリーからアプリケーションを追加する

Azure AD ギャラリーからアプリケーションを追加するには、次の手順に従います。

1.  [Azure Portal](https://portal.azure.com) を開き、**グローバル管理者**または**共同管理者**としてサインインします。

2.  左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3.  フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4.  Azure Active Directory の左側のナビゲーション メニューから **[エンタープライズ アプリケーション]** をクリックします。

5.  **[エンタープライズ アプリケーション]** ウィンドウの右上隅にある **[追加]** ボタンをクリックします。

6.  **[ギャラリーから追加する]** セクションの **[名前を入力してください]** テキスト ボックスで、アプリケーションの名前を入力します。

7.  シングル サインオンを構成するアプリケーションを選択します。

8.  アプリケーションを追加する前に、**[名前]** テキストボックスから名前を変更できます。

9.  **[追加]** ボタンをクリックして、アプリケーションを追加します。

しばらくすると、アプリケーションの構成ウィンドウが表示されます。

### <a name="configure-the-application-for-password-single-sign-on"></a>パスワード シングル サインオンに対応するようにアプリケーションを構成する

アプリケーションのシングル サインオンを構成するには、次の手順に従います。

1. [**Azure Portal**](https://portal.azure.com/) を開き、**グローバル管理者**または**共同管理者**としてサインインします。

2. 左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3. フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4. Azure Active Directory の左側のナビゲーション メニューから **[エンタープライズ アプリケーション]** をクリックします。

5. **[すべてのアプリケーション]** をクリックして、すべてのアプリケーションの一覧を表示します。

   * ここに表示したいアプリケーションが表示されない場合は、**[All Applications List (すべてのアプリケーション リスト)]** の上部にある **[フィルター]** コントロールを使用して、**[表示]** オプションを **[すべてのアプリケーション]** に設定します。

6. シングル サインオンを構成するアプリケーションを選択します。

7. アプリケーションが読み込まれたら、アプリケーションの左側のナビゲーション メニューから **[シングル サインオン]** をクリックします。

8. **[パスワード ベースのサインオン]** モードを選択します。

9. アプリケーションにユーザーを割り当てます。

10. さらに、ユーザーの行を選び、**[資格情報の更新]** をクリックしてユーザーに代わってユーザー名とパスワードを入力すると、ユーザーに代わって資格情報を提供することもできます。 そうしないと、起動時に自分で資格情報を入力するように求めるプロンプトがユーザーに表示されます。

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a>ギャラリー以外のアプリケーションのパスワード シングル サインオンを構成する方法

Azure AD ギャラリーからアプリケーションを構成するには、以下の手順を実行する必要があります。

-   [ギャラリー以外のアプリケーションを追加する](#add-a-non-gallery-application)

-   [パスワード シングル サインオンに対応するようにアプリケーションを構成する](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a>ギャラリー以外のアプリケーションを追加する

Azure AD ギャラリーからアプリケーションを追加するには、次の手順に従います。

1.  [Azure Portal](https://portal.azure.com) を開き、**グローバル管理者**または**共同管理者**としてサインインします。

2.  左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3.  フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4.  Azure Active Directory の左側のナビゲーション メニューから **[エンタープライズ アプリケーション]** をクリックします。

5.  **[エンタープライズ アプリケーション]** ウィンドウの右上隅にある **[追加]** ボタンをクリックします。

6.  **[ギャラリー以外のアプリケーション]** をクリックします。

7.  **[名前]** ボックスに、アプリケーションの名前を入力します。 **[追加]** を選択します。

しばらくすると、アプリケーションの構成ウィンドウが表示されます。

### <a name="configure-the-application-for-password-single-sign-on"></a>パスワード シングル サインオンに対応するようにアプリケーションを構成する

アプリケーションのシングル サインオンを構成するには、次の手順に従います。

1. [**Azure Portal**](https://portal.azure.com/) を開き、**グローバル管理者**または**共同管理者**としてサインインします。

2. 左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3. フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4. Azure Active Directory の左側のナビゲーション メニューから **[エンタープライズ アプリケーション]** をクリックします。

5. **[すべてのアプリケーション]** をクリックして、すべてのアプリケーションの一覧を表示します。

   * ここに表示したいアプリケーションが表示されない場合は、**[All Applications List (すべてのアプリケーション リスト)]** の上部にある **[フィルター]** コントロールを使用して、**[表示]** オプションを **[すべてのアプリケーション]** に設定します。

6. シングル サインオンを構成するアプリケーションを選択します。

7. アプリケーションが読み込まれたら、アプリケーションの左側のナビゲーション メニューから **[シングル サインオン]** をクリックします。

8. **[パスワード ベースのサインオン]** モードを選択します。

9. **サインオン URL** を入力します。 これは、ユーザーが自分のユーザー名とパスワードを入力してサインインする URL です。 この URL にサインイン フィールドが表示されていることを確認します。

10. アプリケーションにユーザーを割り当てます。

11. さらに、ユーザーの行を選び、**[資格情報の更新]** をクリックしてユーザーに代わってユーザー名とパスワードを入力すると、ユーザーに代わって資格情報を提供することもできます。 そうしないと、起動時に自分で資格情報を入力するように求めるプロンプトがユーザーに表示されます。

## <a name="how-to-assign-a-user-to-an-application-directly"></a>アプリケーションに直接ユーザーを割り当てる方法

1 人以上のユーザーをアプリケーションに直接割り当てるには、次の手順に従います。

1. [**Azure Portal**](https://portal.azure.com/) を開き、**グローバル管理者**としてサインインします。

2. 左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3. フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4. Azure Active Directory の左側のナビゲーション メニューから **[エンタープライズ アプリケーション]** をクリックします。

5. **[すべてのアプリケーション]** をクリックして、すべてのアプリケーションの一覧を表示します。

   * ここに表示したいアプリケーションが表示されない場合は、**[All Applications List (すべてのアプリケーション リスト)]** の上部にある **[フィルター]** コントロールを使用して、**[表示]** オプションを **[すべてのアプリケーション]** に設定します。

6. ユーザーを割り当てるアプリケーションを一覧から選びます。

7. アプリケーションが読み込まれたら、アプリケーションの左側のナビゲーション メニューから **[ユーザーとグループ]** をクリックします。

8. **[ユーザーとグループ]** 一覧の上部にある **[追加]** ボタンをクリックして、**[割り当ての追加]** ウィンドウを開きます。

9. **[割り当ての追加]** ウィンドウから **[ユーザーとグループ]** セレクターをクリックします。

10. 割り当てる対象のユーザーの**フル ネーム**または**電子メール アドレス**を **[名前または電子メール アドレスで検索]** 検索ボックスに入力します。

11. リスト内で**ユーザー**にポインターを合わせ、**チェック ボックス**を表示します。 ユーザーのプロファイル写真またはロゴの横にあるチェック ボックスをオンにして、ユーザーを **[選択済み]** リストに追加します。

12. **省略可能:** **複数のユーザーを追加**する場合は、別の**フル ネーム**または**電子メール アドレス**を **[名前または電子メール アドレスで検索]** 検索ボックスに入力し、チェック ボックスをオンにして **[選択済み]** リストにこのユーザーを追加します。

13. ユーザーの選択が完了したら、**[選択]** ボタンをクリックして、アプリケーションに割り当てるユーザーとグループの一覧に追加します。

14. **省略可能:** **[割り当ての追加]** ウィンドウで **[ロールの選択]** セレクターをクリックして、選択したユーザーに割り当てるロールを選択します。

15. **[割り当て]** ボタンをクリックして、選択したユーザーにアプリケーションを割り当てます。

しばらくすると、選択したユーザーがアクセス パネルでこれらのアプリケーションを起動できるようになります。

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a>これらのトラブルシューティング手順で問題が解決しない場合

使用可能な場合は、次の情報を含むサポート チケットを開きます。

-   関連エラー ID

-   UPN (ユーザーの電子メール アドレス)

-   TenantId

-   ブラウザーの種類

-   タイム ゾーンとエラーが発生した時刻/タイムフレーム

-   Fiddler のトレース

## <a name="next-steps"></a>次の手順
[アプリケーション プロキシを使用してアプリにシングル サインオンを提供](application-proxy-configure-single-sign-on-with-kcd.md)

