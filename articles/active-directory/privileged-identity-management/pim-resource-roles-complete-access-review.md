---
title: PIM で Azure リソース ロールのアクセス レビューを完了する - Azure Active Directory | Microsoft Docs
description: Azure AD Privileged Identity Management (PIM) で Azure リソース ロールのアクセス レビューを完了する方法を説明します。
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.subservice: pim
ms.date: 04/02/2018
ms.author: rolyon
ms.custom: pim
ms.collection: M365-identity-device-management
ms.openlocfilehash: aee8ac3c2638ede559f8a1f9c51f2d6e62604998
ms.sourcegitcommit: 6ea7f0a6e9add35547c77eef26f34d2504796565
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2019
ms.locfileid: "65602238"
---
# <a name="complete-an-access-review-of-azure-resource-roles-in-pim"></a>PIM で Azure リソース ロールのアクセス レビューを完了する
[アクセス レビューが開始](pim-resource-roles-start-access-review.md)されると、特権ロール管理者は特権アクセスの状況を確認できるようになります。 Azure Active Directory (Azure AD) Privileged Identity Management (PIM) によって、ユーザーに自分のアクセスをレビューするよう求めるメールが自動的に送信されます。 電子メールが届かなかったユーザーがいる場合は、[アクセス レビューを実行する方法](pim-resource-roles-perform-access-review.md)に関する手順を送信できます。

アクセス レビューの期間が終わった後、またはすべてのユーザーが自己レビューを完了した後に、この記事に記載されている手順に従って、レビューを管理し、結果を表示することができます。

## <a name="manage-access-reviews"></a>アクセス レビューを管理する
1. [Azure ポータル](https://portal.azure.com/)にアクセスします。 その後、ダッシュボードで、**Azure リソース** アプリケーションを選択します。

2. リソースを選択します。

3. ダッシュボードの **[アクセス レビュー]** セクションをクリックします。
![アクセス レビュー](media/pim-resource-roles-complete-access-review/rbac-access-review-home-list.png)

4. 管理するアクセス レビューを選択します。

アクセス レビューの [詳細] ブレードには、このレビューを管理するためのオプションが多数あります。 次のようなオプションがあります。

![レビューを管理するためのオプション](media/pim-resource-roles-complete-access-review/rbac-access-review-menu.png)

### <a name="stop"></a>Stop
すべてのアクセス レビューには終了日が設定されていますが、 **[停止]** ボタンを使用するとレビューを早期に終了することができます。 この時点でレビューを完了していないすべてのユーザーは、レビューを停止した後に完了することはできません。 レビューを停止した後に再開することはできません。

### <a name="reset"></a>Reset
アクセス レビューをリセットして、それに対して行われたすべての決定を削除できます。 アクセス レビューをリセットすると、すべてのユーザーは、再度レビューを行っていないユーザーとしてマークされます。 

### <a name="apply"></a>適用
アクセス レビューを完了したら、**[適用]** ボタンを使用して、レビューの結果を実装します。 レビューでユーザーのアクセスが拒否された場合は、この手順によりそのユーザーのロール割り当てが削除されます。  

### <a name="delete"></a>削除
そのレビューが今後も必要なければ、削除します。 **[削除]** ボタンをクリックすると、レビューが PIM アプリケーションから削除されます。

## <a name="results"></a>結果
**[結果]** タブで、レビュー結果の表示とダウンロードを行います。 
![[結果]](media/pim-resource-roles-complete-access-review/rbac-access-review-results.png) タブ

## <a name="reviewers"></a>レビュー担当者
既存のアクセス レビューの表示とレビュー担当者の追加を行います。 レビュー担当者にレビューを完了するように伝えます。
![レビュー担当者の追加](media/pim-resource-roles-complete-access-review/rbac-access-review-reviewers.png)

## <a name="next-steps"></a>次の手順

- [PIM で Azure リソース ロールのアクセス レビューを開始する](pim-resource-roles-start-access-review.md)
- [PIM で自分の Azure リソース ロールのアクセス レビューを実行する](pim-resource-roles-perform-access-review.md)
