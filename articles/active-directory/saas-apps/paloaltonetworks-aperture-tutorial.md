---
title: チュートリアル:Azure Active Directory と Palo Alto Networks - Aperture の統合 | Microsoft Docs
description: Azure Active Directory と Palo Alto Networks - Aperture の間でシングル サインオンを構成する方法について説明します。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: a5ea18d3-3aaf-4bc6-957c-783e9371d0f1
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 03/19/2019
ms.author: jeedes
ms.openlocfilehash: 375b58f47454a7f5904bcdbd132b8318091e9ebd
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "65870039"
---
# <a name="tutorial-azure-active-directory-integration-with-palo-alto-networks---aperture"></a>チュートリアル:Azure Active Directory と Palo Alto Networks - Aperture の統合

このチュートリアルでは、Palo Alto Networks - Aperture と Azure Active Directory (Azure AD) を統合する方法について説明します。
Palo Alto Networks - Aperture と Azure AD の統合には、次のメリットがあります。

* Palo Alto Networks - Aperture にアクセスする Azure AD ユーザーを制御できます。
* ユーザーが自分の Azure AD アカウントで Palo Alto Networks - Aperture に自動的にサインイン (シングル サインオン) できるように設定できます。
* 1 つの中央サイト (Azure Portal) でアカウントを管理できます。

SaaS アプリと Azure AD の統合の詳細については、「 [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)」を参照してください。
Azure サブスクリプションをお持ちでない場合は、開始する前に[無料アカウントを作成](https://azure.microsoft.com/free/)してください。

## <a name="prerequisites"></a>前提条件

Azure AD と Palo Alto Networks - Aperture の統合を構成するには、次のアイテムが必要です。

* Azure AD サブスクリプション。 Azure AD の環境がない場合は、[こちら](https://azure.microsoft.com/pricing/free-trial/)から 1 か月の評価版を入手できます
* Palo Alto Networks - Aperture でのシングル サインオンが有効なサブスクリプション

## <a name="scenario-description"></a>シナリオの説明

このチュートリアルでは、テスト環境で Azure AD のシングル サインオンを構成してテストします。

* Palo Alto Networks - Aperture では、**SP** と **IDP** によって開始される SSO がサポートされます

## <a name="adding-palo-alto-networks---aperture-from-the-gallery"></a>ギャラリーからの Palo Alto Networks - Aperture の追加

Azure AD への Palo Alto Networks - Aperture の統合を構成するには、ギャラリーから管理対象 SaaS アプリの一覧に Palo Alto Networks - Aperture を追加する必要があります。

**ギャラリーから Palo Alto Networks - Aperture を追加するには、次の手順を実行します。**

1. **[Azure Portal](https://portal.azure.com)** の左側のナビゲーション ウィンドウで、**[Azure Active Directory]** アイコンをクリックします。

    ![Azure Active Directory のボタン](common/select-azuread.png)

2. **[エンタープライズ アプリケーション]** に移動し、**[すべてのアプリケーション]** オプションを選択します。

    ![[エンタープライズ アプリケーション] ブレード](common/enterprise-applications.png)

3. 新しいアプリケーションを追加するには、ダイアログの上部にある **[新しいアプリケーション]** をクリックします。

    ![[新しいアプリケーション] ボタン](common/add-new-app.png)

4. 検索ボックスに「**Palo Alto Networks - Aperture**」と入力し、結果ウィンドウで **[Palo Alto Networks - Aperture]** を選択し、**[追加]** をクリックして、アプリケーションを追加します。

     ![結果一覧の Palo Alto Networks - Aperture](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD シングル サインオンの構成とテスト

このセクションでは、**Britta Simon** というテスト ユーザーに基づいて、Palo Alto Networks - Aperture で Azure AD のシングル サインオンを構成し、テストします。
シングル サインオンを機能させるには、Azure AD ユーザーと Palo Alto Networks - Aperture 内の関連ユーザーとの間にリンク関係が確立されている必要があります。

Palo Alto Networks - Aperture で Azure AD のシングル サインオンを構成してテストするには、次の手順を完了する必要があります。

1. **[Azure AD シングル サインオンの構成](#configure-azure-ad-single-sign-on)** - ユーザーがこの機能を使用できるようにします。
2. **[Palo Alto Networks - Aperture のシングル サインオンの構成](#configure-palo-alto-networks---aperture-single-sign-on)** - アプリケーション側でシングル サインオン設定を構成します。
3. **[Azure AD のテスト ユーザーの作成](#create-an-azure-ad-test-user)** - Britta Simon で Azure AD のシングル サインオンをテストします。
4. **[Azure AD テスト ユーザーの割り当て](#assign-the-azure-ad-test-user)** - Britta Simon が Azure AD シングル サインオンを使用できるようにします。
5. **[Palo Alto Networks - Aperture テスト ユーザーの作成](#create-palo-alto-networks---aperture-test-user)** - Palo Alto Networks - Aperture で Britta Simon に対応するユーザーを作成し、Azure AD の Britta Simon にリンクします。
6. **[シングル サインオンのテスト](#test-single-sign-on)** - 構成が機能するかどうかを確認します。

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD シングル サインオンの構成

このセクションでは、Azure portal 上で Azure AD のシングル サインオンを有効にします。

Palo Alto Networks - Aperture で Azure AD シングル サインオンを構成するには、次の手順を行います。

1. [Azure portal](https://portal.azure.com/) の **Palo Alto Networks - Aperture** アプリケーション統合ページで、**[シングル サインオン]** を選択します。

    ![シングル サインオン構成のリンク](common/select-sso.png)

2. **[シングル サインオン方式の選択]** ダイアログで、**[SAML/WS-Fed]** モードを選択して、シングル サインオンを有効にします。

    ![シングル サインオン選択モード](common/select-saml-option.png)

3. **[SAML でシングル サインオンをセットアップします]** ページで、**[編集]** アイコンをクリックして **[基本的な SAML 構成]** ダイアログを開きます。

    ![基本的な SAML 構成を編集する](common/edit-urls.png)

4. **[基本的な SAML 構成]** セクションで、アプリケーションを **IDP** 開始モードで構成する場合は、次の手順を実行します。

    ![[Palo Alto Networks - Aperture のドメインと URL] のシングル サインオン情報](common/idp-intiated.png)

    a. **[識別子]** ボックスに、`https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/metadata` の形式で URL を入力します。

    b. **[応答 URL]** ボックスに、`https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/auth` のパターンを使用して URL を入力します

5. アプリケーションを **SP** 開始モードで構成する場合は、**[追加の URL を設定します]** をクリックして次の手順を実行します。

    ![[Palo Alto Networks - Aperture のドメインと URL] のシングル サインオン情報](common/metadata-upload-additional-signon.png)

    **[サインオン URL]** ボックスに、`https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/sign_in` という形式で URL を入力します。

    > [!NOTE]
    > これらは実際の値ではありません。 実際の識別子、応答 URL、サインオン URL でこれらの値を更新します。 これらの値を取得するには、[Palo Alto Networks - Aperture クライアント サポート チーム](https://live.paloaltonetworks.com/t5/custom/page/page-id/Support)に連絡してください。 Azure portal の **[基本的な SAML 構成]** セクションに示されているパターンを参照することもできます。

6. **[SAML でシングル サインオンをセットアップします]** ページの **[SAML 署名証明書]** セクションで、**[ダウンロード]** をクリックして要件のとおりに指定したオプションからの**証明書 (Base64)** をダウンロードして、お使いのコンピューターに保存します。

    ![証明書のダウンロードのリンク](common/certificatebase64.png)

7. **[Palo Alto Networks - Aperture の設定]** セクションで、要件に従って適切な URL をコピーします。

    ![構成 URL のコピー](common/copy-configuration-urls.png)

    a. ログイン URL

    b. Azure AD 識別子

    c. ログアウト URL

### <a name="configure-palo-alto-networks---aperture-single-sign-on"></a>Palo Alto Networks - Aperture のシングル サインオンの構成

1. 別の Web ブラウザー ウィンドウで、Palo Alto Networks - Aperture に管理者としてログインします。

2. 上部のメニュー バーで **[設定]** をクリックします。

    ![[設定] タブ](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_settings.png)

3. **[アプリケーション]** に移動し、メニューの左にある **[認証]** をクリックします。

    ![[認証] タブ](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_auth.png)
    
4. **[認証]** ページで、次の手順を実行します。
    
    ![[認証] タブ](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_singlesignon.png)

    a. **[Single Sign-On]\(シングル サインオン\)** フィールドの **[Enable Single Sign-On(Supported SSP Providers are Okta, Onelogin)]\(シングル サインオンを有効にする (サポートされている SSP プロバイダーは Okta、Onelogin)\)** をオンにします。

    b. **[Identity Provider ID]\(ID プロバイダー ID\)** ボックスに、Azure portal からコピーした **[Azure AD 識別子]** の値を貼り付けます。

    c. **[ファイルの選択]** をクリックして、Azure AD からダウンロードした証明書を **[ID プロバイダー証明書]** フィールドにアップロードします。

    d. **[Identity Provider SSO URL]\(ID プロバイダーの SSO URL\)** ボックスに、Azure portal からコピーした **[ログイン URL]** の値を貼り付けます。

    e. **[Aperture 情報]** セクションで IdP 情報を確認し、**[Aperture キー]** フィールドから証明書をダウンロードします。

    f. **[Save]** をクリックします。

### <a name="create-an-azure-ad-test-user"></a>Azure AD のテスト ユーザーの作成 

このセクションの目的は、Azure Portal で Britta Simon というテスト ユーザーを作成することです。

1. Azure portal の左側のウィンドウで、**[Azure Active Directory]**、**[ユーザー]**、**[すべてのユーザー]** の順に選択します。

    ![[ユーザーとグループ] と [すべてのユーザー] リンク](common/users.png)

2. 画面の上部にある **[新しいユーザー]** を選択します。

    ![[新しいユーザー] ボタン](common/new-user.png)

3. [ユーザーのプロパティ] で、次の手順を実行します。

    ![[ユーザー] ダイアログ ボックス](common/user-properties.png)

    a. **[名前]** フィールドに「**BrittaSimon**」と入力します。
  
    b. **[ユーザー名]** フィールドに「**brittasimon@yourcompanydomain.extension**」と入力します。  
    たとえば、BrittaSimon@contoso.com のように指定します。

    c. **[パスワードを表示]** チェック ボックスをオンにし、[パスワード] ボックスに表示された値を書き留めます。

    d. **Create** をクリックしてください。

### <a name="assign-the-azure-ad-test-user"></a>Azure AD テスト ユーザーの割り当て

このセクションでは、Britta Simon に Palo Alto Networks - Aperture へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

1. Azure portal で **[エンタープライズ アプリケーション]** を選択し、**[すべてのアプリケーション]** を選択してから、**[Palo Alto Networks - Aperture]** を選択します。

    ![[エンタープライズ アプリケーション] ブレード](common/enterprise-applications.png)

2. アプリケーションの一覧で **[Palo Alto Networks - Aperture]** を選択します。

    ![アプリケーションの一覧の [Palo Alto Networks - Aperture] リンク](common/all-applications.png)

3. 左側のメニューで **[ユーザーとグループ]** を選びます。

    ![[ユーザーとグループ] リンク](common/users-groups-blade.png)

4. **[ユーザーの追加]** をクリックし、**[割り当ての追加]** ダイアログで **[ユーザーとグループ]** を選択します。

    ![[割り当ての追加] ウィンドウ](common/add-assign-user.png)

5. **[ユーザーとグループ]** ダイアログの [ユーザー] の一覧で **[Britta Simon]** を選択し、画面の下部にある **[選択]** ボタンをクリックします。

6. SAML アサーション内に任意のロール値が必要な場合、**[ロールの選択]** ダイアログでユーザーに適したロールを一覧から選択し、画面の下部にある **[選択]** をクリッします。

7. **[割り当ての追加]** ダイアログで、**[割り当て]** ボタンをクリックします。

### <a name="create-palo-alto-networks---aperture-test-user"></a>Palo Alto Networks - Aperture テスト ユーザーの作成

このセクションでは、Palo Alto Networks - Aperture で Britta Simon というユーザーを作成します。 [Palo Alto Networks - Aperture Client サポート チーム](https://live.paloaltonetworks.com/t5/custom/page/page-id/Support)と協力し合い、Palo Alto Networks - Aperture プラットフォームにユーザーを追加します。 シングル サインオンを使用する前に、ユーザーを作成し、有効化する必要があります。

### <a name="test-single-sign-on"></a>シングル サインオンのテスト 

このセクションでは、アクセス パネルを使用して Azure AD のシングル サインオン構成をテストします。

アクセス パネルで [Palo Alto Networks - Aperture] タイルをクリックすると、SSO を設定した Palo Alto Networks - Aperture に自動的にサインインします。 アクセス パネルの詳細については、[アクセス パネルの概要](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)に関する記事を参照してください。

## <a name="additional-resources"></a>その他のリソース

- [SaaS アプリと Azure Active Directory を統合する方法に関するチュートリアルの一覧](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Azure Active Directory の条件付きアクセスとは](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

