---
title: 利用規約 - Azure Active Directory | Microsoft Docs
description: アクセス前に従業員やゲストに対して情報を提示する Azure Active Directory の利用規約を使用して開始する方法について説明します。
services: active-directory
author: rolyon
manager: mtillman
editor: ''
ms.assetid: d55872ef-7e45-4de5-a9a0-3298e3de3565
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.subservice: compliance
ms.date: 05/15/2019
ms.author: rolyon
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8659ecab649216650403f3a992cc6e356e5de5d0
ms.sourcegitcommit: be9fcaace62709cea55beb49a5bebf4f9701f7c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65823591"
---
# <a name="azure-active-directory-terms-of-use-feature"></a>Azure Active Directory Terms of Use 機能
Azure AD Terms of use は、エンド ユーザーに情報を提示するために使うことができる簡単な方法を提供します。 この方法で情報を提示することにより、法律上やコンプライアンス上の要件を満たすうえで重要な免責事項が確実にユーザーに表示されます。 この記事では、利用規約の使用を開始する方法について説明します。

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-intro-sentence.md)]

## <a name="overview-videos"></a>概要ビデオ

次のビデオでは、利用規約の概要を簡単に説明します。

>[!VIDEO https://www.youtube.com/embed/tj-LK0abNao]

その他のビデオについては、以下を参照してください。
- [How to deploy Terms of use in Azure Active Directory (Azure Active Directory で利用規約を展開する方法)](https://www.youtube.com/embed/N4vgqHO2tgY)
- [How to roll out Terms of use in Azure Active Directory (Azure Active Directory で利用規約をロールアウトする方法)](https://www.youtube.com/embed/t_hA4y9luCY)

## <a name="what-can-i-do-with-terms-of-use"></a>Terms of use を使用してできること
Azure AD Terms of use では、以下のことができます。
- 従業員やゲストに、アクセス前に利用規約への同意を求める。
- 従業員やゲストに、すべてのデバイスでアクセス前に利用規約への同意を求める。
- 従業員やゲストに、定期的に利用規約への同意を求める。
- 組織内のすべてのユーザーに一般的な使用条件を提示する。
- ユーザーの属性 (例: [動的グループ](../users-groups-roles/groups-dynamic-membership.md)を使用して、医師と看護師や、国内従業員と国際従業員など) に基づいて特定の使用条件を提示する。
- ビジネスへの影響が大きいアプリケーション (Salesforce など) にアクセスする際に特定の使用条件を提示する。
- 使用条件を異なる言語で提示する。
- 利用規約に同意したユーザーと同意していないユーザーを一覧表示する。
- プライバシー規制の順守に役立つ。
- コンプライアンスおよび監査のために利用規約アクティビティのログを表示する。
- [Microsoft Graph API](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/agreement) を使用して利用規約を作成および管理する (現在プレビューの段階)。

## <a name="prerequisites"></a>前提条件
Azure AD Terms of use を使用および構成するには、以下が必要です。

- Azure AD Premium P1、P2、EMS E3、EMS E5 のいずれかのサブスクリプション。
    - これらのサブスクリプションをお持ちでない場合は、[Azure AD Premium を入手する](../fundamentals/active-directory-get-started-premium.md)か、[Azure AD Premium 試用版を有効にする](https://azure.microsoft.com/trial/get-started-active-directory/)ことができます。
- 構成するディレクトリに対する次のいずれかの管理者アカウント。
    - グローバル管理者
    - セキュリティ管理者
    - 条件付きアクセス管理者

## <a name="terms-of-use-document"></a>使用条件のドキュメント

Azure AD Terms of use は、PDF 形式で内容を提示します。 この PDF はどのような内容でもよく (既存の契約ドキュメントなど)、エンド ユーザーのサインイン時にユーザーの同意を得ることができます。 モバイル デバイスのユーザーをサポートする場合、PDF の推奨フォント サイズは 24 ポイントです。

## <a name="add-terms-of-use"></a>使用条件の追加
使用条件のドキュメントが完成した後は、次の手順を使って追加します。

1. Azure にグローバル管理者、セキュリティ管理者、または条件付きアクセス管理者としてサインインします。

1. [https://aka.ms/catou](https://aka.ms/catou) から **[使用条件]** に移動します。

    ![[使用条件] ブレード](./media/terms-of-use/tou-blade.png)

1. **[新しい条件]** をクリックします。

    ![TOU の追加](./media/terms-of-use/new-tou.png)

1. **[名前]** ボックスに、Azure portal で使用する利用規約の名前を入力します。

1. **[表示名]** ボックスに、ユーザーがサインインしたときに表示されるタイトルを入力します。

1. **[Terms of use document]\(利用規約のドキュメント)** で、完成した利用規約の PDF を参照して選びます。

1. 利用規約のドキュメントの言語を選択します。 言語オプションを使用して、言語が異なる複数の使用条件をアップロードできます。 エンド ユーザーに表示される使用条件のバージョンは、ブラウザーの設定に基づきます。

1. エンド ユーザーが同意する前に利用規約を表示しなければならないようにする場合、 **[ユーザーは利用規約を展開する必要があります]** を **[On]\(オン)** にします。

1. エンド ユーザーがアクセスするすべてのデバイスで利用規約に同意しなければならないようにする場合、 **[各デバイスでユーザーによる同意が必要]** を **[On]\(オン)** にします。 詳しくは、[デバイスごとの利用規約](#per-device-terms-of-use)をご覧ください。

1. 定期的に利用規約への同意を期限切れにする場合、 **[期限切れの同意]** を **[On]\(オン)** にします。 オンに設定すると、2 つのスケジュール設定が追加表示されます。

    ![期限切れの同意](./media/terms-of-use/expire-consents.png)

1. **[Expire starting on]\(期限切れの開始日)** および **[Frequency]\(頻度)** 設定を使用して、利用規約の期限切れのスケジュールを指定します。 次の表に、いくつかの設定例とその結果を示します。

    | 期限切れの開始日 | 頻度 | 結果 |
    | --- | --- | --- |
    | 今日の日付  | 月単位 | ユーザーは本日から利用規約に同意する必要があります。また、毎月再同意する必要があります。 |
    | 未来の日付  | 月単位 | ユーザーは本日から利用規約に同意する必要があります。 未来の日付が来ると、同意の有効期限が切れ、ユーザーは毎月再同意する必要があります。  |

    たとえば、期限切れの開始日を **1 月 1 日**に設定し、頻度で **[月単位]** を選んだ場合、2 人のユーザーの有効期限は次のようになります。

    | User | 最初の同意日 | 最初に有効期限が切れる日付 | 2 回目に有効期限が切れる日付 | 3 回目に有効期限が切れる日付 |
    | --- | --- | --- | --- | --- |
    | Alice | 1 月 1 日 | 2 月 1 日 | 3 月 1 日 | 4 月 1 日 |
    | Bob | 1 月 15 日 | 2 月 1 日 | 3 月 1 日 | 4 月 1 日 |

1. **[Duration before re-acceptance requires (days)]\(再同意を要求するまでの日数)** 設定を使用して、ユーザーが利用規約に再同意する必要があるまでの日数を指定します。 これにより、ユーザーに個別のスケジュールを適用することができます。 たとえば、日数に **30** 日を指定すると、2 人のユーザーの有効期限切れは次のようになります。

    | User | 最初の同意日 | 最初に有効期限が切れる日付 | 2 回目に有効期限が切れる日付 | 3 回目に有効期限が切れる日付 |
    | --- | --- | --- | --- | --- |
    | Alice | 1 月 1 日 | 1 月 31 日 | 3 月 2 日 | 4 月 1 日 |
    | Bob | 1 月 15 日 | 2 月 14 日 | 3 月 16 日 | 4 月 15 日 |

    **[期限切れの同意]** と **[Duration before re-acceptance requires (days)]\(再同意を要求するまでの日数)** の両方の設定を使用することもできますが、通常はどちらか一方を使用します。

1. **[条件付きアクセス]** の下にある **[Enforce with conditional access policy template]\(条件付きアクセス ポリシーのテンプレートの適用)** リストを使用して、利用規約を適用するテンプレートを選択します。

    ![条件付きアクセス テンプレート](./media/terms-of-use/conditional-access-templates.png)

    | Template | 説明 |
    | --- | --- |
    | **クラウド アプリへのアクセス (すべてのゲスト用)** | すべてのゲストとすべてのクラウド アプリに対して条件付きアクセス ポリシーが作成されます。 このポリシーは、Azure portal に影響します。 これが作成された後、サインアウトしてサインインし直さなければならないことがあります。 |
    | **クラウド アプリへのアクセス (すべてのユーザー用)** | すべてのユーザーとすべてのクラウド アプリに対して条件付きアクセス ポリシーが作成されます。 このポリシーは、Azure portal に影響します。 これが作成された後、サインアウトしてサインインし直す必要があります。 |
    | **カスタム ポリシー** | この利用規約が適用されるユーザー、グループ、およびアプリを選択します。 |
    | **後で条件付きアクセス ポリシーを作成する** | この利用規約は、条件付きアクセス ポリシーを作成するときに、制御の許可一覧に表示されます。 |

    >[!IMPORTANT]
    >条件付きアクセス ポリシー規制 (使用条件を含む) は、サービス アカウントに対する強制をサポートしていません。 サービス アカウントはすべて、条件付きアクセス ポリシーから除外することをお勧めします。

     カスタム条件付きアクセス ポリシーを使うと、特定のクラウド アプリケーションやユーザー グループまで、きめ細かい使用条件を有効にできます。 詳細については、[クイック スタートのクラウド アプリにアクセスする前に利用規約への同意を要求する](require-tou.md)を参照してください。

1. **Create** をクリックしてください。

    カスタム条件付きアクセス テンプレートを選んだ場合、表示される新しい画面でカスタム条件付きアクセス ポリシーを作成できます。

    ![カスタム ポリシー](./media/terms-of-use/custom-policy.png)

    新しい使用条件が表示されるようになります。

    ![TOU の追加](./media/terms-of-use/create-tou.png)

## <a name="view-report-of-who-has-accepted-and-declined"></a>同意したユーザーと拒否したユーザーのレポートの表示
[使用条件] ブレードには、同意したユーザーと拒否したユーザーの数が表示されます。 これらの数および同意したユーザーと拒否したユーザーは、使用条件が有効な間、保存されます。

1. Azure にサインインし、[https://aka.ms/catou](https://aka.ms/catou) から **[使用条件]** に移動します。

    ![[使用条件] ブレード](./media/terms-of-use/view-tou.png)

1. 利用規約について、 **[同意]** または **[拒否]** の下に表示される数値をクリックすると、現在のユーザーの状態が表示されます。

    ![利用規約の同意](./media/terms-of-use/accepted-tou.png)

1. 個々のユーザーの履歴を表示するには、省略記号ボタン ( **...** )、 **[履歴の表示]** の順にクリックします。

    ![履歴の表示メニュー](./media/terms-of-use/view-history-menu.png)

    履歴の表示ウィンドウでは、すべての同意、拒否、および有効期限切れの履歴を確認できます。

    ![履歴の表示ウィンドウ](./media/terms-of-use/view-history-pane.png)

## <a name="view-azure-ad-audit-logs"></a>Azure AD 監査ログの表示
追加のアクティビティを確認できるように、Azure AD Terms of use には監査ログが用意されています。 ユーザーが同意するたびに、イベントがトリガーされます。そのイベントは、監査ログに記録され、**30 日間**保存されます。 これらのログはポータルで表示することや、.csv ファイルとしてダウンロードすることができます。

Azure AD 監査ログを使い始める手順は次のとおりです。

1. Azure にサインインし、[https://aka.ms/catou](https://aka.ms/catou) から **[使用条件]** に移動します。

1. 利用規約を選択します。

1. **[監査ログの表示]** をクリックします。

    ![[使用条件] ブレード](./media/terms-of-use/audit-tou.png)

1. Azure AD の [監査ログ] 画面では、リストを使って情報をフィルターし、特定の監査ログ情報だけを対象にすることができます。

    **[ダウンロード]** をクリックして、.csv ファイルで情報をダウンロードしてローカルに使うこともできます。

    ![監査ログ](./media/terms-of-use/audit-logs-tou.png)

    ログをクリックすると、追加のアクティビティの詳細を含むウィンドウが表示されます。

    ![アクティビティの詳細](./media/terms-of-use/audit-log-activity-details.png)

## <a name="what-terms-of-use-looks-like-for-users"></a>ユーザーに表示される使用条件の外観
使用条件を作成して適用すると、対象ユーザーにはサインイン時に次の画面が表示されます。

![ユーザーの Web サインイン](./media/terms-of-use/user-tou.png)

ユーザーは利用規約を表示し、必要な場合はボタンを使用して拡大/縮小できます。

![ズーム ボタンを使って利用規約を表示する](./media/terms-of-use/zoom-buttons.png)

次の画面は、使用条件がモバイル デバイス上でどのように表示されるかを示しています。

![ユーザーのモバイル サインイン](./media/terms-of-use/mobile-tou.png)

ユーザーは、利用規約に 1 回だけ同意すればよく、以降のサインインで利用規約が再び表示されることはありません。

### <a name="how-users-can-review-their-terms-of-use"></a>ユーザーが使用条件を確認する方法
ユーザーは、以下の手順を使用して、同意した使用条件を確認できます。

1. [https://myapps.microsoft.com](https://myapps.microsoft.com) にサインインします。

1. 右上隅に表示される自分の名前をクリックし、 **[プロファイル]** を選択します。

    ![プロファイル](./media/terms-of-use/tou14.png)

1. [プロファイル] ページで、 **[使用条件の確認]** をクリックします。

    ![プロファイル - 利用規約の確認](./media/terms-of-use/tou13a.png)

1. そこから同意した使用条件を確認できます。

## <a name="edit-terms-of-use-details"></a>利用規約の詳細を編集する
利用規約の詳細の一部を編集できますが、既存のドキュメントを変更することはできません。 詳細の編集方法を次の手順で説明します。

1. Azure にサインインし、[https://aka.ms/catou](https://aka.ms/catou) から **[使用条件]** に移動します。

1. 編集する利用規約を選択します。

1. **[条件の編集]** をクリックします。

1. [利用規約の編集] ウィンドウで、[名前]、[表示名]、または [require users to expand values]\(値の展開をユーザーに要求する\) を変更します。

    PDF ドキュメント、各デバイスでユーザーによる同意が必要、期限切れの同意、再同意までの日数、条件付きアクセス ポリシーなど、その他の設定も変更したい場合は、新しい利用規約を作成する必要があります。

    ![利用規約の編集](./media/terms-of-use/edit-tou.png)

1. **[保存]** をクリックして変更を保存します。

    変更を保存しても、ユーザーは編集した利用規約に再度同意する必要はありません。

## <a name="add-a-terms-of-use-language"></a>利用規約の言語を追加する
利用規約の言語を追加する方法を次の手順で説明します。

1. Azure にサインインし、[https://aka.ms/catou](https://aka.ms/catou) から **[使用条件]** に移動します。

1. 編集する利用規約を選択します。

1. [詳細] ウィンドウで、 **[言語]** タブをクリックします。

    ![TOU の追加](./media/terms-of-use/languages-tou.png)

1. **[言語の追加]** をクリックします。

1. [Add terms of use language]\(利用規約の言語の追加\) ウィンドウで、ローカライズされた PDF をアップロードして、言語を選択します。

    ![TOU の追加](./media/terms-of-use/language-add-tou.png)

1. **[追加]** をクリックして、言語を追加します。

## <a name="per-device-terms-of-use"></a>デバイスごとの利用規約

**[各デバイスでユーザーによる同意が必要]** 設定を使用すると、エンド ユーザーがアクセスするすべてのデバイスで利用規約に同意しなければならないようにすることができます。 エンド ユーザーは、デバイスを Azure AD に参加させる必要があります。 デバイスが参加すると、デバイス ID を使用して各デバイスに利用規約が適用されます。

サポートされているプラットフォームとソフトウェアの一覧を示します。

> [!div class="mx-tableFixed"]
> |  | iOS | Android | Windows 10 | その他 |
> | --- | --- | --- | --- | --- |
> | **ネイティブ アプリ** | はい | はい | はい |  |
> | **Microsoft Edge** | はい | はい | はい |  |
> | **Internet Explorer** | はい | はい | はい |  |
> | **Chrome (拡張機能あり)** | はい | はい | はい |  |

デバイスごとの利用規約には、次の制約があります。

- デバイスは、1 つのテナントにのみ参加させることができます。
- ユーザーは、デバイスを参加させるアクセス許可を持っている必要があります。
- Intune Enrollment アプリはサポートされていません。
- Azure AD B2B ユーザーはサポートされていません。

ユーザーのデバイスが参加していない場合、デバイスを参加させる必要があるというメッセージを受け取ります。 操作方法は、プラットフォームとソフトウェアによって異なります。

### <a name="join-a-windows-10-device"></a>Windows 10 デバイスを参加させる

ユーザーが Windows 10 と Microsoft Edge を使用している場合、[デバイスを参加させる](../user-help/user-help-join-device-on-network.md#to-join-an-already-configured-windows-10-device)ための次のようなメッセージを受信します。

![Windows 10 および Microsoft Edge - デバイスの参加プロンプト](./media/terms-of-use/per-device-win10-edge.png)

Chrome を使用している場合、[Windows 10 アカウント拡張機能](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji)のインストールを求められます。

### <a name="browsers"></a>ブラウザー

ユーザーがサポートされていないブラウザーを使用している場合、別のブラウザーを使用するように依頼されます。

![サポートされていないブラウザー](./media/terms-of-use/per-device-browser-unsupported.png)

## <a name="delete-terms-of-use"></a>使用条件の削除
次の手順を使って、古い使用条件を削除できます。

1. Azure にサインインし、[https://aka.ms/catou](https://aka.ms/catou) から **[使用条件]** に移動します。

1. 削除する使用条件を選びます。

1. **[条件の削除]** をクリックします。

1. 続行するかどうかを確認するメッセージが表示されたら、**はい** をクリックします。

    ![使用条件の削除](./media/terms-of-use/delete-tou.png)

    使用条件が表示されなくなります。

## <a name="deleted-users-and-active-terms-of-use"></a>削除されたユーザーとアクティブな使用条件
既定では、削除されたユーザーは Azure AD に 30 日間、削除状態で維持されます。その間は、管理者が必要に応じて復元することができます。 30 日後、そのユーザーは完全に削除されます。 その期間に達していなくても、全体管理者は、Azure Active Directory ポータルを使用して明示的に、[最近削除したユーザーを完全に削除](../fundamentals/active-directory-users-restore.md)することができます。 ユーザーが完全に削除されると、以降そのユーザーに関するデータは、アクティブな使用条件から削除されます。 監査ログには、削除済みユーザーに関する監査情報が維持されます。

## <a name="policy-changes"></a>ポリシーの変更
条件付きアクセス ポリシーは直ちに有効になるためです。 このような場合、管理者には "不適切なクラウド" または "Azure AD トークンの問題" が表示されるようになります。 新しいポリシーを満たすには、管理者はサインアウトしてサインインし直す必要があります。

>[!IMPORTANT]
> 次の場合、新しいポリシーを満たすには、対象ユーザーはいったんサインアウトしてからサインインし直す必要があります。
> - 使用条件で条件付きアクセス ポリシーが有効になった場合
> - または、第 2 の使用条件が作成された場合

## <a name="b2b-guests-preview"></a>B2B ゲスト (プレビュー)

ほとんどの組織は、従業員が組織の利用規約やプライバシーに関する声明に同意するためのプロセスを用意しています。 しかし、Azure AD 企業間 (B2B) ゲストが SharePoint または Teams 経由で追加された際に同じ同意を適用するには、どうすればよいでしょうか? 条件付きアクセスと利用規約を使用すると、B2B ゲスト ユーザーに直接ポリシーを適用できます。 招待の利用フロー中に、ユーザーに対して利用規約が表示されます。 このサポートは現在プレビューの段階です。

利用規約は、ユーザーが Azure AD でゲスト アカウントを持っている場合にのみ表示されます。 現在の SharePoint Online には、ユーザーがゲスト アカウントを持っていなくてもドキュメントまたはフォルダーを共有できる[アドホック外部共有受信者エクスペリエンス](/sharepoint/what-s-new-in-sharing-in-targeted-release)があります。 この場合、利用規約は表示されません。

![すべてのゲスト ユーザー](./media/terms-of-use/b2b-guests.png)

## <a name="support-for-cloud-apps-preview"></a>クラウド アプリのサポート (プレビュー)

利用規約は、Azure Information Protection や Microsoft Intune など、異なるクラウド アプリで使用できます。 このサポートは現在プレビューの段階です。

### <a name="azure-information-protection"></a>Azure Information Protection

Azure Information Protection アプリの条件付きアクセス ポリシーを構成し、ユーザーが保護されたドキュメントにアクセスするときに利用規約を強制します。 これにより、ユーザーが最初に保護されたドキュメントにアクセスする前に、利用規約がトリガーされます。

![Azure Information Protection クラウド アプリ](./media/terms-of-use/cloud-app-info-protection.png)

### <a name="microsoft-intune-enrollment"></a>Microsoft Intune Enrollment

Microsoft Intune Enrollment アプリの条件付きアクセス ポリシーを構成し、Intune にデバイスを登録する前に利用規約を強制することができます。 詳しくは、[組織に適した利用規約ソリューションの選択に関するブログ投稿](https://go.microsoft.com/fwlink/?linkid=2010506&clcid=0x409)をご覧ください。

![Microsoft Intune クラウド アプリ](./media/terms-of-use/cloud-app-intune.png)

> [!NOTE]
> [デバイスごとの利用規約](#per-device-terms-of-use)では、Intune Enrollment アプリはサポートされていません。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

**Q:ユーザーが利用規約に同意したかどうか、および同意した日時を確認するにはどうすればよいですか?**<br />
A:[利用規約] ブレードで **[同意]** の下の数字をクリックします。 Azure AD 監査ログでも同意アクティビティを表示または検索できます。 詳しくは、「同意したユーザーと拒否したユーザーのレポートの表示」および「[Azure AD 監査ログの表示](#view-azure-ad-audit-logs)」をご覧ください。

**Q:情報はどのくらいの期間保存されますか?**<br />
A:利用規約レポートのユーザーの数および同意したユーザーと拒否したユーザーの数は、利用規約が有効な間、保存されます。 Azure AD 監査ログは 30 日間保存されます。

**Q:利用規約レポートの同意数と Azure AD 監査ログの同意数が異なります。**<br />
A:利用規約レポートはその利用規約の有効期間中保存されるのに対し、Azure AD 監査ログは 30 日間保存されます。 また、使用条件レポートには、ユーザーの現在の同意状態のみが表示されます。 たとえば、あるユーザーが拒否してから同意した場合、使用条件レポートにはそのユーザーの同意のみが表示されます。 履歴を確認するには、Azure AD 監視ログを使用できます。

**Q:利用規約の詳細を編集した場合、ユーザーはもう一度同意する必要がありますか?**<br />
A:いいえ。管理者が利用規約の詳細 (名前、表示名、展開必須、または言語の追加) を編集しても、ユーザーが新しい条件に再同意する必要はありません。

**Q:既存の利用規約のドキュメントを更新できますか?**<br />
A:現在、既存の利用規約のドキュメントを更新することはできません。 利用規約のドキュメントを変更するには、新しい利用規約のインスタンスを作成する必要があります。

**Q:ハイパーリンクが利用規約の PDF ドキュメント内にある場合、エンド ユーザーはそれらをクリックできますか?**<br />
A:PDF は既定で JPEG としてレンダリングされるため、ハイパーリンクをクリックすることはできません。 必要に応じて、ユーザーは **[表示に問題がある場合は、ここをクリックします]** を選択できます。ハイパーリンクがサポートされていれば、PDF がネイティブでレンダリングされます。

**Q:利用規約は複数の言語をサポートしていますか?**<br />
A:はい。 現時点では、管理者が 1 つの使用条件に対して構成できる言語が 108 あります。 管理者は、複数の PDF ドキュメントをアップロードして各言語に対応付けることができます (最大 108)。 エンド ユーザーがサインインすると、ブラウザーの言語設定を確認して一致するドキュメントを表示します。 一致しない場合は、既定のドキュメント (最初にアップロードされたドキュメント) が表示されます。

**Q:利用規約はいつトリガーされますか?**<br />
A:利用規約は、サインイン エクスペリエンスの間にトリガーされます。

**Q:どのようなアプリケーションを利用規約の対象にできますか?**<br />
A:最新の認証を使ったエンタープライズ アプリケーションに条件付きアクセス ポリシーを作成できます。 詳細については、[エンタープライズ アプリケーション](./../manage-apps/view-applications-portal.md)に関するページをご覧ください。

**Q:特定のユーザーまたはアプリケーションに複数の利用規約を追加できますか?**<br />
A:はい、そのグループやアプリケーションを対象とする複数の条件付きアクセス ポリシーを作成することで可能です。 複数の利用規約の対象になっているユーザーは、一度に 1 つの利用規約に同意します。

**Q:ユーザーが利用規約を拒否した場合はどうなりますか?**<br />
A:ユーザーは、アプリケーションへのアクセスをブロックされます。 ユーザーは、アクセスするには、もう一度サインインして利用規約に同意する必要があります。

**Q:以前に同意した利用規約の同意を取り消すことはできますか?**<br />
A:[以前に同意した利用規約を確認する](#how-users-can-review-their-terms-of-use)ことはできますが、現在、同意を取り消す方法はありません。

**Q:Intune の利用規約も使用している場合はどうなりますか?**<br />
A:Azure AD の利用規約と [Intune の利用規約](/intune/terms-and-conditions-create)の両方を構成している場合、ユーザーはそれら両方に同意する必要があります。 詳しくは、[組織のブログ投稿に適した使用条件ソリューションの選択](https://go.microsoft.com/fwlink/?linkid=2010506&clcid=0x409)に関する記事をご覧ください。

**Q:利用規約サービスにはどのエンドポイントが認証に使用されますか?**<br />
A:利用規約では、認証に https://tokenprovider.termsofuse.identitygovernance.azure.com と https://account.activedirectory.windowsazure.com のエンドポイントを利用します。 組織に登録用の URL の許可リストがある場合は、サインイン用の Azure AD エンドポイントと共に、これらのエンドポイントを許可リストに追加する必要があります。

## <a name="next-steps"></a>次の手順

- [クイック スタート:クラウド アプリにアクセスする前に利用規約への同意を要求する](require-tou.md)
- [Azure Active Directory の条件付きアクセスのベスト プラクティス](best-practices.md)
