---
title: チュートリアル:LinkedIn Elevate を構成し、Azure Active Directory を使用した自動ユーザー プロビジョニングに対応させる | Microsoft Docs
description: Azure Active Directory を構成して、ユーザー アカウントを LinkedIn Elevate に自動的にプロビジョニング/プロビジョニング解除する方法を説明します。
services: active-directory
documentationcenter: ''
author: ArvindHarinder1
manager: CelesteDG
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2019
ms.author: arvinh
ms.collection: M365-identity-device-management
ms.openlocfilehash: adefb0c88e88a8bfb4b896c0788654e478ff4555
ms.sourcegitcommit: e9a46b4d22113655181a3e219d16397367e8492d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65963691"
---
# <a name="tutorial-configure-linkedin-elevate-for-automatic-user-provisioning"></a>チュートリアル:LinkedIn Elevate を構成し、自動ユーザー プロビジョニングに対応させる

このチュートリアルでは、Azure AD から LinkedIn Elevate にユーザー アカウントを自動的にプロビジョニング/プロビジョニング解除するうえで LinkedIn Elevate と Azure AD で実行する必要がある手順について説明します。

## <a name="prerequisites"></a>前提条件

このチュートリアルで説明するシナリオでは、次の項目があることを前提としています。

* Azure Active Directory テナント
* LinkedIn Elevate テナント
* LinkedIn Account Center へのアクセス許可がある LinkedIn Elevate の管理者アカウント

> [!NOTE]
> Azure Active Directory と LinkedIn Elevate の統合には、[SCIM](http://www.simplecloud.info/) プロトコルが使用されます。

## <a name="assigning-users-to-linkedin-elevate"></a>LinkedIn Elevate へのユーザーの割り当て

Azure Active Directory では、選択されたアプリへのアクセスが付与されるユーザーを決定する際に "割り当て" という概念が使用されます。 自動ユーザー アカウント プロビジョニングのコンテキストでは、Azure AD 内のアプリケーションに "割り当て済み" のユーザーとグループのみが同期されます。

プロビジョニング サービスを構成して有効にする前に、LinkedIn Elevate へのアクセスが必要なユーザーを表す Azure AD 内のユーザーやグループを決定しておく必要があります。 決定し終えたら、次の手順でこれらのユーザーを LinkedIn Elevate に割り当てることができます。

[エンタープライズ アプリケーションにユーザーまたはグループを割り当てる](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-elevate"></a>ユーザーを LinkedIn Elevate に割り当てる際の重要なヒント

* 単一の Azure AD ユーザーを LinkedIn Elevate に割り当てて、プロビジョニングの構成をテストすることをお勧めします。 後でユーザーやグループを追加で割り当てられます。

* ユーザーを LinkedIn Elevate に割り当てるときに、割り当てのダイアログで**ユーザー** ロールを選択する必要があります。 "既定のアクセス" ロールはプロビジョニングでは使えません。

## <a name="configuring-user-provisioning-to-linkedin-elevate"></a>LinkedIn Elevate へのユーザー プロビジョニングの構成

このセクションでは、Azure AD を LinkedIn Elevate の SCIM のユーザー アカウント プロビジョニング API に接続する手順のほか、プロビジョニング サービスを構成して、Azure AD のユーザーとグループの割り当てに基づいて割り当て済みのユーザー アカウントを LinkedIn Elevate で作成、更新、無効化する手順を説明します。

**ヒント:** LinkedIn Elevate では SAML ベースのシングル サインオンを有効にすることもできます。これを行うには、[Azure portal](https://portal.azure.com) で説明されている手順に従ってください。 シングル サインオンは自動プロビジョニングとは別に構成できますが、これらの 2 つの機能は相補的な関係にあります。

### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-elevate-in-azure-ad"></a>Azure AD で LinkedIn Elevate への自動ユーザー アカウント プロビジョニングを構成するには

まず最初に、LinkedIn アクセス トークンを取得します。 エンタープライズ管理者の場合は、アクセス トークンをセルフ プロビジョニングできます。 アカウント センターで、**[設定] &gt; [グローバル設定]** をクリックすると、**[SCIM セットアップ]** パネルが開きます。

> [!NOTE]
> リンクからではなく、アカウント センターに直接アクセスしている場合は、次の手順を使用してアクセスできます。

1. アカウント センターにサインインします。

2. **[管理者] &gt; [管理者設定]** を選択します。

3. 左のサイドバーで **[Advanced Integrations] \(詳細な統合)** をクリックします。 アカウント センターにリダイレクトされます。

4. **[+ SCIM 構成を新しく追加]** をクリックし、各フィールドの入力を行って手順に従います。

    > [!NOTE]
    > ライセンスの自動割り当てを有効にしない場合、ユーザー データのみが同期されるということです。

    ![LinkedIn Elevate のプロビジョニング](./media/linkedinelevate-provisioning-tutorial/linkedin_elevate1.PNG)

    > [!NOTE]
    > ライセンスの自動割り当てを有効にする場合、アプリケーション インスタンスとライセンスの種類に注意する必要があります。 ライセンスは、すべてのライセンスが取得されるまで、先着順で割り当てられます。

    ![LinkedIn Elevate のプロビジョニング](./media/linkedinelevate-provisioning-tutorial/linkedin_elevate2.PNG)

5. **[トークンの生成]** をクリックします。 **[アクセス トークン]** フィールドの下に、アクセス トークンが表示されます。

6. ページを離れる前に、クリップボードまたはコンピューターにアクセス トークンを保存します。

7. 次に、[Azure Portal](https://portal.azure.com) にサインインし、**[Azure Active Directory] > [エンタープライズ アプリ] > [すべてのアプリケーション]** セクションに移動します。

8. シングル サインオンのために LinkedIn Elevate を既に構成している場合は、検索フィールドで LinkedIn Elevate のインスタンスを検索します。 構成していない場合は、**[追加]** を選択してアプリケーション ギャラリーで **LinkedIn Elevate** を検索します。 検索結果から LinkedIn Elevate を選択してアプリケーションの一覧に追加します。

9. LinkedIn Elevate のインスタンスを選択してから、**[プロビジョニング]** タブを選択します。

10. **[プロビジョニング モード]** を **[自動]** に設定します。

    ![LinkedIn Elevate のプロビジョニング](./media/linkedinelevate-provisioning-tutorial/linkedin_elevate3.PNG)

11. **[管理者資格情報]** の下で、以下のフィールドを入力します。

    * **[テナント URL]** フィールドに、「`https://api.linkedin.com`」と入力します。

    * **[シークレット トークン]** フィールドに、手順 1 で生成したアクセス トークンを入力し、**[テスト接続]** をクリックします。

    * ポータルの右上に成功通知が表示されます。

12. プロビジョニングのエラー通知を受け取るユーザーまたはグループの電子メール アドレスを **[通知用メール]** フィールドに入力して、下のチェック ボックスをオンにします。

13. **[Save]** をクリックします。

14. **[属性マッピング]** セクションで、Azure AD から LinkedIn Elevate に同期するユーザーおよびグループ属性を確認します。 **[Matching (照合)]** プロパティとして選択されている属性は、更新処理で LinkedIn Elevate のユーザー アカウントおよびグループとの照合に使用されることに注意してください。 [保存] ボタンをクリックして変更をコミットします。

    ![LinkedIn Elevate のプロビジョニング](./media/linkedinelevate-provisioning-tutorial/linkedin_elevate4.PNG)

15. LinkedIn Elevate に対して Azure AD プロビジョニング サービスを有効にするには、**[設定]** セクションで **[プロビジョニング状態]** を **[オン]** に変更します。

16. **[Save]** をクリックします。

これで、[ユーザーとグループ] セクションで LinkedIn Elevate に割り当てたユーザーやグループの初期同期が開始されます。 初期同期は後続の同期よりも実行に時間がかかることに注意してください。後続の同期は、サービスが実行されている限り約 40 分ごとに実行されます。 **[同期の詳細]** セクションを使用すると、進行状況を監視できるほか、リンクをクリックしてプロビジョニング アクティビティ ログを取得できます。このログには、プロビジョニング サービスによって LinkedIn Elevate アプリに対して実行されたすべてのアクションが記載されています。

Azure AD プロビジョニング ログの読み取りの詳細については、「[自動ユーザー アカウント プロビジョニングについてのレポート](../manage-apps/check-status-user-account-provisioning.md)」をご覧ください。

## <a name="additional-resources"></a>その他のリソース

* [エンタープライズ アプリのユーザー アカウント プロビジョニングの管理](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](../manage-apps/what-is-single-sign-on.md)
