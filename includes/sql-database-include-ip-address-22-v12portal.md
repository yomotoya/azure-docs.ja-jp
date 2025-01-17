---
title: サーバーレベルのファイアウォール規則
description: サーバーレベルのファイアウォール規則
keywords: sql 接続,接続文字列
services: sql-database
author: dalechen
manager: craigg
ms.service: sql-database
ms.custom: develop apps
ms.topic: include
ms.date: 07/13/2018
ms.author: ninarn
ms.openlocfilehash: 8d0f9899dbb7599340b8d15ca010a0157011fb9e
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66164295"
---
1. [Azure Portal](https://portal.azure.com/) にサインインします。

2. 左側の一覧で、**[すべてのサービス]** を選びます。

3. スクロールして、**[SQL Server]** を選びます。

    ![ポータルで Azure SQL Database サーバーを見つける][b21-FindServerInPortal]
5. フィルター テキスト ボックスで、サーバーの名前の入力を開始します。 行が表示されます。

6. お使いのサーバーの行を選びます。 サーバー用のブレードが表示されます。

7. お使いのサーバーのブレードで、**[設定]** を選びます。

8. **[ファイアウォール]** を選びます。

    ![[設定] > [ファイアウォール] を選ぶ][b31-SettingsFirewallNavig]
9. **[クライアント IP の追加]** を選びます。 最初のテキスト ボックスに、新しい規則の名前を入力します。

10. 有効にする範囲の IP アドレスの値を入力します。

    * 低い方の値の最後を **.0**、高い方の値の最後を **.255** にしておくと便利です。

11. **[保存]** を選択します。

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
