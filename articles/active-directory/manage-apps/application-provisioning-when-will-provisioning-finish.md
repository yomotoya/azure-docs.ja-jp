---
title: 長時間を要する Azure AD ギャラリー アプリケーションへのユーザー プロビジョニング | Microsoft Docs
description: アプリケーションへのプロビジョニングを実行する理由を理解する方法は、想像以上に時間がかかる可能性があります。
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
ms.reviewer: asteen
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8622a7bbd913710a2173399048baab7067d2fae7
ms.sourcegitcommit: 36c50860e75d86f0d0e2be9e3213ffa9a06f4150
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2019
ms.locfileid: "65783798"
---
# <a name="user-provisioning-to-an-azure-ad-gallery-application-is-taking-hours-or-more"></a>長時間を要する Azure AD ギャラリー アプリケーションへのユーザー プロビジョニング

最初にアプリケーションの自動プロビジョニングを有効にすると、初回の同期には 20 分～数時間かかることがあります。この時間は Azure AD のディレクトリ サイズと、プロビジョニングの範囲内にいるユーザー数によって異なります。 

初回同期後に両方のシステムの状態を表すウォーターマークがプロビジョニング サービスに保存されるため、後続の同期はより速くなり、パフォーマンスが改善されます。

## <a name="how-to-improve-provisioning-performance"></a>プロビジョニングのパフォーマンスを改善する方法

初回の同期に数時間以上かかる場合、パフォーマンスを改善するために実行できる方法の 1 つが、

-   **ユーザーのスコープ フィルター**です。 スコープ フィルターによって、ユーザーが特定の属性値に基づいてフィルター処理され、プロビジョニング サービスが Azure AD から抽出するデータを細かく調整できるようになります。 スコープ フィルターの詳細については、「[スコープ フィルターを使用した属性ベースのアプリケーション プロビジョニング](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters)」を参照してください。

## <a name="next-steps"></a>次の手順
[Azure Active Directory による SaaS アプリへのユーザー プロビジョニングとプロビジョニング解除の自動化](user-provisioning.md)

