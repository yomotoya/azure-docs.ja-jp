---
title: 最小限のダウンタイムでの Azure Database for PostgreSQL - Single Server への移行
description: この記事では、Azure Database Migration Service を使用して、PostgreSQL データベースを Azure Database for PostgreSQL - Single Server に最小限のダウンタイムで移行する方法について説明します。
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: conceptual
ms.date: 5/6/2019
ms.openlocfilehash: 93cd390889c023adf1c30a8470e1c2298598439e
ms.sourcegitcommit: 509e1583c3a3dde34c8090d2149d255cb92fe991
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2019
ms.locfileid: "65067508"
---
# <a name="minimal-downtime-migration-to-azure-database-for-postgresql---single-server"></a>最小限のダウンタイムでの Azure Database for PostgreSQL - Single Server への移行
[Azure Database Migration Service](https://aka.ms/get-dms) (DMS) に新たに導入された**継続的同期機能**を使用すると、最小限のダウンタイムで PostgreSQL を Azure Database for PostgreSQL に移行できます。 この機能で、アプリケーションによって発生するダウンタイムの長さが短くなります。

## <a name="overview"></a>概要
Azure DMS では、オンプレミスから Azure Database for PostgreSQL への初期読み込みを実行してから、アプリケーションは実行中のままで、新しいトランザクションを Azure に継続的に同期します。 データがターゲットの Azure 側に追いついた後、アプリケーションを短時間停止し (最小限のダウンタイム)、データの最後のバッチがターゲットに追いつくまで (アプリケーションを停止してから、アプリケーションが事実上新しいトラフィックを受け取ることができなくなるまで) 待ってから、Azure を指すように接続文字列を更新します。 完了すると、アプリケーションは Azure 上で動作します。

![Azure Database Migration Service での継続的同期](./media/howto-migrate-online/ContinuousSync.png)

## <a name="next-steps"></a>次の手順
- [Microsoft Azure でのアプリケーションの最新化](https://medius.studios.ms/Embed/Video/BRK2102?sid=BRK2102)のビデオをご覧ください。PostgreSQL アプリを Azure Database for PostgreSQL に移行する方法のデモが含まれています。
- 「[DMS を使用して PostgreSQL をオンラインで Azure Database for PostgreSQL に移行する](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online)」のチュートリアルを参照してください。
