---
author: SnehaGunda
ms.service: cosmos-db
ms.topic: include
ms.date: 11/09/2018
ms.author: sngun
ms.openlocfilehash: 99dddd86c9348c9791d3012b382298bb020e63c9
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66154567"
---
**1.SDK の提供終了は顧客にどのような方法で通知されますか。**

サポートされる SDK に速やかに移行できるように、提供終了となる SDK のサポート終了は 12 か月前に通知されます。 さらに、Microsoft Azure 管理ポータル、デベロッパー センター、ブログ投稿、担当サービス管理者への直接連絡など、さまざまな連絡手段で顧客に通知されます。

**2.顧客は、その 12 か月間、提供終了 "予定" の Azure Cosmos DB SDK でアプリケーションを作成できますか。** 

はい。顧客には、12 か月の猶予期間中、提供終了 "予定" の Azure Cosmos DB SDK でアプリケーションを作成、デプロイ、変更するためのすべてのアクセス権が付与されます。 顧客には、この 12 か月の猶予期間中、適宜、新しくサポートされるバージョンの Azure Cosmos DB SDK に移行することが推奨されます。

**3.顧客は、12 か月の通知期間が過ぎたら、提供終了となった Azure Cosmos DB SDK でアプリケーションを作成したり、変更したりすることができますか。**

12 か月の通知期間後、SDK は提供終了となります。 提供終了となった SDK で Azure Cosmos DB にアクセスすることは Azure Cosmos DB プラットフォームにより禁止されます。 さらに、提供終了となった SDK にはカスタマー サポートが提供されません。

**4.顧客が実行しているアプリケーションで、サポートされていないバージョンの Azure Cosmos DB SDK が使用されている場合はどうなりますか。**

提供終了となったバージョンの SDK で Azure Cosmos DB サービスに接続を試みても拒否されます。 

**5.新しい機能は、提供終了ではないあらゆる SDK に適用されますか。**

新しい機能は新しいバージョンにのみ追加されます。 提供終了ではない古いバージョンの SDK を利用している場合、Azure Cosmos DB への要求は以前のように機能しますが、新しい機能にはアクセスできません。  

**6.期限前にアプリケーションを更新できない場合、どうすればよいですか。**

可能な限り早く最新の SDK にアップグレードすることが推奨されます。 ある SDK が提供終了予定の場合、アプリケーションを更新するために 12 か月が与えられます。 何らかの理由から、その時間枠内にアプリケーションを更新できない場合、期限前に [Cosmos DB チーム](mailto:askcosmosdb@microsoft.com)にお問い合わせいただき、サポートをご要請ください。

