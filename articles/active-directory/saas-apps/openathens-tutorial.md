---
title: チュートリアル:Azure Active Directory と OpenAthens の統合 | Microsoft Docs
description: Azure Active Directory と OpenAthens の間でシングル サインオンを構成する方法について説明します。
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: barbkess
ms.assetid: dd4adfc7-e238-41d5-8b25-1811f08078b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 1/4/2019
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3eca6fc3ab788ee7085c0df5f6c9770858af29ba
ms.sourcegitcommit: 67625c53d466c7b04993e995a0d5f87acf7da121
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2019
ms.locfileid: "65891709"
---
# <a name="tutorial-azure-active-directory-integration-with-openathens"></a>チュートリアル:Azure Active Directory と OpenAthens の統合

このチュートリアルでは、OpenAthens と Azure Active Directory (Azure AD) を統合する方法について説明します。
OpenAthens と Azure AD の統合には、次の利点があります。

* OpenAthens にアクセスするユーザーを Azure AD で制御できます。
* ユーザーが自分の Azure AD アカウントで OpenAthens に自動的にサインイン (シングル サインオン) するように設定できます。
* 1 つの中央サイト (Azure Portal) でアカウントを管理できます。

SaaS アプリと Azure AD の統合の詳細については、「 [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)」を参照してください。
Azure サブスクリプションをお持ちでない場合は、開始する前に[無料アカウントを作成](https://azure.microsoft.com/free/)してください。

## <a name="prerequisites"></a>前提条件

OpenAthens と Azure AD の統合を構成するには、次のものが必要です。

* Azure AD サブスクリプション。 Azure AD の環境がない場合は、[こちら](https://azure.microsoft.com/pricing/free-trial/)から 1 か月の評価版を入手できます
* OpenAthens でのシングル サインオンが有効なサブスクリプション

## <a name="scenario-description"></a>シナリオの説明

このチュートリアルでは、テスト環境で Azure AD のシングル サインオンを構成してテストします。

* OpenAthens では、**IDP** によって開始される SSO がサポートされます

* OpenAthens では、**Just-In-Time** ユーザー プロビジョニングがサポートされます

## <a name="adding-openathens-from-the-gallery"></a>ギャラリーからの OpenAthens の追加

Azure AD への OpenAthens の統合を構成するには、ギャラリーから管理対象 SaaS アプリの一覧に OpenAthens を追加する必要があります。

**ギャラリーから OpenAthens を追加するには、次の手順に従います。**

1. **[Azure Portal](https://portal.azure.com)** の左側のナビゲーション ウィンドウで、**[Azure Active Directory]** アイコンをクリックします。

    ![Azure Active Directory のボタン](common/select-azuread.png)

2. **[エンタープライズ アプリケーション]** に移動し、**[すべてのアプリケーション]** オプションを選択します。

    ![[エンタープライズ アプリケーション] ブレード](common/enterprise-applications.png)

3. 新しいアプリケーションを追加するには、ダイアログの上部にある **[新しいアプリケーション]** をクリックします。

    ![[新しいアプリケーション] ボタン](common/add-new-app.png)

4. 検索ボックスに「**OpenAthens**」と入力し、結果パネルで **[OpenAthens]** を選択し、**[追加]** をクリックして、アプリケーションを追加します。

     ![結果一覧の OpenAthens](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD シングル サインオンの構成とテスト

このセクションでは、**Britta Simon** というテスト ユーザーに基づいて、OpenAthens で Azure AD のシングル サインオンを構成し、テストします。
シングル サインオンを機能させるには、Azure AD ユーザーと OpenAthens 内の関連ユーザーとの間にリンク関係が確立されている必要があります。

OpenAthens で Azure AD のシングル サインオンを構成してテストするには、次の構成要素を完了する必要があります。

1. **[Azure AD シングル サインオンの構成](#configure-azure-ad-single-sign-on)** - ユーザーがこの機能を使用できるようにします。
2. **[OpenAthens のシングル サインオンの構成](#configure-openathens-single-sign-on)** - アプリケーション側でシングル サインオン設定を構成します。
3. **[Azure AD のテスト ユーザーの作成](#create-an-azure-ad-test-user)** - Britta Simon で Azure AD のシングル サインオンをテストします。
4. **[Azure AD テスト ユーザーの割り当て](#assign-the-azure-ad-test-user)** - Britta Simon が Azure AD シングル サインオンを使用できるようにします。
5. **[OpenAthens テスト ユーザーの作成](#create-openathens-test-user)** - OpenAthens で Britta Simon に対応するユーザーを作成し、Azure AD の Britta Simon にリンクさせます。
6. **[シングル サインオンのテスト](#test-single-sign-on)** - 構成が機能するかどうかを確認します。

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD シングル サインオンの構成

このセクションでは、Azure portal 上で Azure AD のシングル サインオンを有効にします。

OpenAthens で Azure AD シングル サインオンを構成するには、次の手順に従います。

1. [Azure portal](https://portal.azure.com/) の **OpenAthens** アプリケーション統合ページで、**[シングル サインオン]** を選択します。

    ![シングル サインオン構成のリンク](common/select-sso.png)

2. **[シングル サインオン方式の選択]** ダイアログで、**[SAML/WS-Fed]** モードを選択して、シングル サインオンを有効にします。

    ![シングル サインオン選択モード](common/select-saml-option.png)

3. **[SAML でシングル サインオンをセットアップします]** ページで、**[編集]** アイコンをクリックして **[基本的な SAML 構成]** ダイアログを開きます。

    ![基本的な SAML 構成を編集する](common/edit-urls.png)

5. **[基本的な SAML 構成]** セクションで、**サービス プロバイダー メタデータ ファイル**をアップロードします。この手順については、後からこのチュートリアルの中で説明します。

    a. **[メタデータ ファイルをアップロードします]** をクリックします。

    ![OpenAthens (メタデータのアップロード)](common/upload-metadata.png)

    b. **フォルダー ロゴ**をクリックしてメタデータ ファイルを選択し、**[アップロード]** をクリックします。

    ![OpenAthens (アップロードするメタデータの参照)](common/browse-upload-metadata.png)

    c. メタデータ ファイルが正常にアップロードされると、**識別子**の値が、**[基本的な SAML 構成]** セクションのテキスト ボックスに自動的に設定されます。

    ![[OpenAthens のドメインと URL] のシングル サインオン情報](common/idp-identifier.png)

6. **[SAML でシングル サインオンをセットアップします]** ページの **[SAML 署名証明書]** セクションで、**[ダウンロード]** をクリックして、要件のとおりに指定したオプションから**フェデレーション メタデータ XML** をダウンロードして、お使いのコンピューターに保存します。

    ![証明書のダウンロードのリンク](common/metadataxml.png)

### <a name="configure-openathens-single-sign-on"></a>OpenAthens のシングル サインオンの構成

1. 別の Web ブラウザー ウィンドウで、OpenAthens 企業サイトに管理者としてログインします。

2. **[管理]** タブの一覧から **[接続]** を選択します。 

    ![Configure single sign-on](./media/openathens-tutorial/tutorial_openathens_application1.png)

3. **[SAML 1.1/2.0]** を選択し、**[構成]** を選択します。

    ![Configure single sign-on](./media/openathens-tutorial/tutorial_openathens_application2.png)
    
4. 構成を追加するには、**[参照]** を選択して Azure Portal からダウンロードしたメタデータ .xml ファイルをアップロードし、**[追加]** を選択します。

    ![Configure single sign-on](./media/openathens-tutorial/tutorial_openathens_application3.png)

5. **[詳細]** タブで、次の手順を実行します。

    ![Configure single sign-on](./media/openathens-tutorial/tutorial_openathens_application4.png)

    a. **[Display name mapping]\(表示名マッピング\)** で、**[Use attribute]\(属性の使用\)** を選択します。

    b. **[Display name attribute]\(表示名属性\)** ボックスに、値「`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`」を入力します。
    
    c. **[Unique user mapping]\(一意のユーザー マッピング\)** で、**[Use attribute]\(属性の使用\)** を選択します。

    d. **[Display name attribute]\(一意のユーザ属性\)** ボックスに、値「`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`」を入力します。

    e. **[状態]** で、3 つのチェック ボックスすべてをオンにします。

    f. **[Create local accounts]\(ローカル アカウントの作成\)** で、**[automatically]\(自動\)** を選択します。

    g. **[変更の保存]** を選択します。

    h. **[</> Relying Party]\(</> 証明書利用者\)** タブで、**[Metadata URL]\(メタデータ URL\)** をコピーし、その URL をブラウザーで開いて **SP メタデータ XML** ファイルをダウンロードします。 Azure AD の **[基本的な SAML 構成]** セクションで、この SP メタデータ ファイルをアップロードします。

    ![Configure single sign-on](./media/openathens-tutorial/tutorial_openathens_application5.png)

### <a name="create-an-azure-ad-test-user"></a>Azure AD のテスト ユーザーの作成 

このセクションの目的は、Azure Portal で Britta Simon というテスト ユーザーを作成することです。

1. Azure portal の左側のウィンドウで、**[Azure Active Directory]**、**[ユーザー]**、**[すべてのユーザー]** の順に選択します。

    ![[ユーザーとグループ] と [すべてのユーザー] リンク](common/users.png)

2. 画面の上部にある **[新しいユーザー]** を選択します。

    ![[新しいユーザー] ボタン](common/new-user.png)

3. [ユーザーのプロパティ] で、次の手順を実行します。

    ![[ユーザー] ダイアログ ボックス](common/user-properties.png)

    a. **[名前]** フィールドに「**BrittaSimon**」と入力します。
  
    b. **[User name]\(ユーザー名\)** フィールドに「**brittasimon\@yourcompanydomain.extension**」と入力します。  
    たとえば、BrittaSimon@contoso.com のように指定します。

    c. **[パスワードを表示]** チェック ボックスをオンにし、[パスワード] ボックスに表示された値を書き留めます。

    d. **Create** をクリックしてください。

### <a name="assign-the-azure-ad-test-user"></a>Azure AD テスト ユーザーの割り当て

このセクションでは、Britta Simon に OpenAthens へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

1. Azure portal 上で **[エンタープライズ アプリケーション]** を選択し、**[すべてのアプリケーション]** を選択してから、**[OpenAthens]** を選択します。

    ![[エンタープライズ アプリケーション] ブレード](common/enterprise-applications.png)

2. アプリケーションの一覧で、「**OpenAthens**」と入力して選択します。

    ![アプリケーションの一覧の OpenAthens のリンク](common/all-applications.png)

3. 左側のメニューで **[ユーザーとグループ]** を選びます。

    ![[ユーザーとグループ] リンク](common/users-groups-blade.png)

4. **[ユーザーの追加]** をクリックし、**[割り当ての追加]** ダイアログで **[ユーザーとグループ]** を選択します。

    ![[割り当ての追加] ウィンドウ](common/add-assign-user.png)

5. **[ユーザーとグループ]** ダイアログの [ユーザー] の一覧で **[Britta Simon]** を選択し、画面の下部にある **[選択]** ボタンをクリックします。

6. SAML アサーション内に任意のロール値が必要な場合、**[ロールの選択]** ダイアログでユーザーに適したロールを一覧から選択し、画面の下部にある **[選択]** をクリッします。

7. **[割り当ての追加]** ダイアログで、**[割り当て]** ボタンをクリックします。

### <a name="create-openathens-test-user"></a>OpenAthens のテスト ユーザーの作成

このセクションでは、Britta Simon というユーザーを OpenAthens に作成します。 OpenAthens では、**Just-In-Time ユーザー プロビジョニング**がサポートされています。この設定は既定で有効になっています。 このセクションでは、ユーザー側で必要な操作はありません。 OpenAthens にユーザーがまだ存在していない場合は、認証後に新規に作成されます。

### <a name="test-single-sign-on"></a>シングル サインオンのテスト 

このセクションでは、アクセス パネルを使用して Azure AD のシングル サインオン構成をテストします。

アクセス パネル上で [OpenAthens] タイルをクリックすると、SSO を設定した OpenAthens に自動的にサインインします。 アクセス パネルの詳細については、[アクセス パネルの概要](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)に関する記事を参照してください。

## <a name="additional-resources"></a>その他のリソース

- [SaaS アプリと Azure Active Directory を統合する方法に関するチュートリアルの一覧](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Azure Active Directory の条件付きアクセスとは](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

