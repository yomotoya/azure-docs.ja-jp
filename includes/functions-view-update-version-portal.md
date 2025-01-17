---
title: インクルード ファイル
description: インクルード ファイル
services: functions
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 11/26/2018
ms.author: glenga
ms.custom: include file
ms.openlocfilehash: d06bda1826964b019edb156375885c7f389ca6ec
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66131262"
---
関数アプリで現在使用されているランタイム バージョンを表示して更新するには、次の手順に従います。

1. [Azure portal](https://portal.azure.com) で、関数アプリに移動します。

1. **[構成済みの機能]** で、**[Function App の設定]** を選択します。

    ![[Function App の設定] を選択する](./media/functions-view-update-version-portal/add-update-app-setting.png)

1. **[Function App の設定]** タブで、**[ランタイム バージョン]** を探します。 特定のランタイム バージョンと要求されたメジャー バージョンをメモします。 以下の例では、バージョンが `~2` に設定されています。

   ![[Function App の設定] を選択する](./media/functions-view-update-version-portal/function-app-view-version.png)

1. バージョン 1.x ランタイムに関数アプリを固定するには、**[ランタイム バージョン]** で **[~1]** を選択します。 アプリに関数がある場合、このスイッチは無効です。

1. ランタイム バージョンを変更したときは、**[概要]** タブに戻り、**[再起動]** を選択してアプリを再起動します。  関数アプリがバージョン 1.x ランタイムでの実行を再開します。関数を作成するときは、バージョン 1.x のテンプレートを使用します。