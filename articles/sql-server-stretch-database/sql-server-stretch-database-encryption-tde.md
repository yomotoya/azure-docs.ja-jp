---
title: Stretch Database に対する Transparent Data Encryption の有効化 - Azure | Microsoft Docs
description: Azure での SQL Server Stretch Database に対する Transparent Data Encryption (TDE) の有効化
services: sql-server-stretch-database
documentationcenter: ''
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 06/14/2016
author: blazem-msft
ms.author: blazem
ms.reviewer: jroth
manager: jroth
ms.openlocfilehash: 61f556476958484b78b9c3dff2583eb6db043637
ms.sourcegitcommit: 13cba995d4538e099f7e670ddbe1d8b3a64a36fb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2019
ms.locfileid: "66003035"
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>Azure での Stretch Database に対する Transparent Data Encryption (TDE) の有効化
> [!div class="op_single_selector"]
> * [Azure Portal](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Transparent Data Encryption (TDE) を使用すると、データベース、関連付けられているバックアップ、保管されているトランザクション ログ ファイルの暗号化と暗号化解除をリアルタイムで実行することにより、悪意のあるアクティビティの脅威からデータを保護できます。アプリケーションを変更する必要はありません。

TDE は、データベース暗号化キーと呼ばれる対称キーを使用してデータベース全体のストレージを暗号化します。 データベース暗号化キーは組み込まれているサーバー証明書によって保護されます。 組み込みのサーバー証明書は、Azure サーバーごとに一意です。 Microsoft は、少なくとも 90 日ごとにこれらの証明書を自動的にローテーションします。 TDE の一般的な説明については、「 [透過的なデータ暗号化 (TDE)]」を参照してください。

## <a name="enabling-encryption"></a>暗号化の有効化
Stretch 対応 SQL Server データベースから移行したデータを格納している Azure データベースの TDE を有効にするには、次の操作を行います。

1.  [Azure ポータル](https://portal.azure.com)
2. データベース ブレードで **[設定]** ボタンをクリックします。
3. **[透過的なデータ暗号化]** オプションを選択します ![][1]
4. **[オン]**、**[保存]** の順に選択します。
   ![][2]

## <a name="disabling-encryption"></a>暗号化の無効化
Stretch 対応 SQL Server データベースから移行したデータを格納している Azure データベースの TDE を無効にするには、次の操作を行います。

1.  [Azure ポータル](https://portal.azure.com)
2. データベース ブレードで **[設定]** ボタンをクリックします。
3. **[透過的なデータ暗号化]** オプションを選択します
4. **[オフ]**、**[保存]** の順に選択します

<!--Anchors-->
[透過的なデータ暗号化 (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
