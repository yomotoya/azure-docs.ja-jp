---
title: インクルード ファイル
description: インクルード ファイル
services: event-grid
author: tfitzmac
ms.service: event-grid
ms.topic: include
ms.date: 07/05/2018
ms.author: tomfitz
ms.custom: include file
ms.openlocfilehash: c3677e7897498aa06d7bd547988ad4dc0326f39b
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66150449"
---
## <a name="enable-event-grid-resource-provider"></a>Event Grid リソース プロバイダーを有効にする

Azure サブスクリプションで Event Grid を使用したことがない場合は、Event Grid リソース プロバイダーを登録する必要がある可能性があります。

Azure Portal で次の操作を行います。

1. **[サブスクリプション]** を選択します。
1. Event Grid に使用するサブスクリプションを選択します。
1. **[設定]** で、**[リソース プロバイダー]** を選択します。
1. **Microsoft.EventGrid** を探します。
1. 登録されていない場合は、**[登録]** を選択します。 

登録完了まで少し時間がかかることがあります。 **[最新の情報に更新]** を選択して、状態を更新します。 **[状態]** が **[登録済み]** に になったら、次に進めることができます。