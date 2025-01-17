---
title: Azure AD エンタイトルメント管理 (プレビュー) をトラブルシューティングする - Azure Active Directory
description: Azure Active Directory エンタイトルメント管理 (Preview) をトラブルシューティングする際に確認しておくべき事項について説明します。
services: active-directory
documentationCenter: ''
author: rolyon
manager: mtillman
editor: markwahl-msft
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.subservice: compliance
ms.date: 04/25/2019
ms.author: rolyon
ms.reviewer: mwahl
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8ca7955186d6c6fb1dff2acd6a2d5badd1cedaef
ms.sourcegitcommit: 9ad75f83bbf0fc4623b7995794f33bbf823b31c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2019
ms.locfileid: "64540666"
---
# <a name="troubleshoot-azure-ad-entitlement-management-preview"></a>Azure AD エンタイトルメント管理 (プレビュー) をトラブルシューティングする

> [!IMPORTANT]
> Azure Active Directory (Azure AD) エンタイトルメント管理は現在、パブリック プレビュー段階です。
> このプレビュー バージョンはサービス レベル アグリーメントなしで提供されています。運用環境のワークロードに使用することはお勧めできません。 特定の機能はサポート対象ではなく、機能が制限されることがあります。
> 詳しくは、[Microsoft Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)に関するページをご覧ください。

この記事では、Azure Active Directory (Azure AD) エンタイトルメント管理 (Preview) をトラブルシューティングする際に確認しておくべき事項について説明します。

## <a name="checklist-for-entitlement-management-administration"></a>エンタイトルメント管理のチェックリスト

* エンタイトルメント管理の構成時に、アクセスが拒否されたというメッセージが表示された場合、自分がグローバル管理者であるときは、ディレクトリに [Azure AD Premium P2 (または EMS E5) ライセンス](entitlement-management-overview.md#prerequisites)があることを確認してください。  
* アクセス パッケージの作成中または表示中に、アクセスが拒否されたというメッセージが表示された場合、自分がカタログ作成者グループのメンバーであるときは、最初のアクセス パッケージを作成する前にカタログを作成する必要があります。

## <a name="checklist-for-adding-a-resource"></a>リソースを追加する場合のチェックリスト

* アクセス パッケージで管理するリソースにユーザーが既に割り当てられている場合は、適切なポリシーを使用してユーザーがアクセス パッケージに割り当てられていることを確認します。 たとえば、既にユーザーがいるグループをアクセス パッケージに含めるとよいでしょう。 グループ内のこれらのユーザーが引き続きアクセスを必要とする場合、これらのユーザーは、アクセス パッケージに対する適切なポリシーを持ち、グループへのアクセスが不可能にならないようにする必要があります。 アクセス パッケージを割り当てるには、そのリソースを含むアクセス パッケージを要求するようにユーザーに依頼するか、またはアクセス パッケージにユーザーを直接割り当てます。 詳細については、[既存のアクセス パッケージの編集および管理に関するページ](entitlement-management-access-package-edit.md)を参照してください。

## <a name="checklist-for-request-issues"></a>要求を発行する場合のチェックリスト

* ユーザーがアクセス パッケージへのアクセスを要求する必要がある場合は、アクセス パッケージの**マイ アクセス ポータル リンク**をユーザーが使用していることを確認します。 詳細については、「[Copy My Access portal link (マイ アクセス ポータル リンクのコピー)](entitlement-management-access-package-edit.md#copy-my-access-portal-link)」を参照してください。

* ユーザーがアクセス パッケージを要求するためにマイ アクセス ポータルにサインインする場合は、ユーザー認証に組織のアカウントが使用されることを確認します。 組織のアカウントとして使用できるのは、リソース ディレクトリ内のアカウント、またはアクセス パッケージのいずれかのポリシーに含まれるディレクトリ内のアカウントです。 ユーザーのアカウントが組織のアカウントでない場合、またはディレクトリがポリシーに含まれていない場合は、ユーザーにアクセス パッケージが表示されません。 詳細については、[アクセス パッケージへのアクセスの要求に関するページ](entitlement-management-request-access.md)を参照してください。

* リソース ディレクトリへのサインインがブロックされた場合、ユーザーは、マイ アクセス ポータルでアクセスを要求できなくなります。 ユーザーがアクセスを要求できるようにするには、ユーザーのプロファイルからサインインのブロックを削除する必要があります。 サインインのブロックを削除するには、Azure portal 内で **[Azure Active Directory]** 、 **[ユーザー]** をクリックし、ユーザーをクリックしてから **[プロファイル]** をクリックします。 **[設定]** セクションを編集し、 **[サインインのブロック]** を **[いいえ]** に変更します。 詳細については、「[Azure Active Directory を使用してユーザーのプロファイル情報を追加または更新する](../fundamentals/active-directory-users-profile-azure-portal.md)」を参照してください。

* マイ アクセス ポータルの場合、ユーザーが要求者と承認者を兼ねているときは、 **[承認]** ページにアクセス パッケージの要求が表示されません。 これは、ユーザーが自分の要求を承認できないようにするための動作です。 ユーザーが要求しているアクセス パッケージで、別の承認者がポリシーに基づいて構成されていることを確認します。 詳細については、「[Edit an existing policy (既存のポリシーの編集)](entitlement-management-access-package-edit.md#edit-an-existing-policy)」を参照してください。

* ディレクトリにまだサインインしていない新規の外部ユーザーが、SharePoint Online サイトを含むアクセス パッケージを受信した場合、このアクセス パッケージは、ユーザーのアカウントが SharePoint Online でプロビジョニングされるまで、配信未完了として表示されます。

## <a name="next-steps"></a>次の手順

- [エンタイトルメント管理でユーザーがアクセス権をどのように取得したかについてのレポートを確認する](entitlement-management-reports.md)
