---
title: Azure Cosmos DB での読み取りと書き込みのコストの最適化
description: この記事では、データに対して読み取りおよび書き込み操作を実行する際に Azure Cosmos DB のコストを削減する方法について説明します。
author: rimman
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 05/21/2019
ms.author: rimman
ms.openlocfilehash: 13ce5ee8b0e2a5d9cc84ea1a408ebba152b46050
ms.sourcegitcommit: e9a46b4d22113655181a3e219d16397367e8492d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65967405"
---
# <a name="optimize-reads-and-writes-cost-in-azure-cosmos-db"></a>Azure Cosmos DB の読み取りと書き込みのコストの最適化

この記事では、Azure Cosmos DB からデータを読み取りおよび書き込みするために必要なコストを計算する方法について説明します。 読み取り操作には、アイテムの取得が含まれ、書き込み操作には、アイテムの挿入、置換、削除、およびアップサートが含まれます。  

## <a name="cost-of-reads-and-writes"></a>読み取りと書き込みのコスト

Azure Cosmos DB では、プロビジョニング済みスループット モデルを使用して、スループットと待機時間の観点から予測可能なパフォーマンスを保証します。 プロビジョニング済みスループットは、1 秒あたりの[要求ユニット](request-units.md) (RU/秒) で表されます。 要求ユニット (RU) は、要求を実行するために必要な CPU、メモリ、IO などのコンピューティング リソースを介した論理抽象化です。 プロビジョニング済みスループット (RU) は確保され、ご使用のコンテナーまたはデータベース専用として、予測可能なスループットおよび待機時間を提供します。 プロビジョニング済みスループットにより、Azure Cosmos DB は予測可能で一貫したパフォーマンスを提供でき、どのような規模でも待機時間の短縮と高可用性が保証されます。 要求ユニットは、アプリケーションに必要なリソースの数に関する推論を簡素化する、正規化された通貨を表します。 

読み取りと書き込みの間の要求ユニットの区別について考慮する必要はありません。 要求ユニットの統一された通貨モデルは、読み取りと書き込みの両方に対して同じスループット容量を相互に使用できることで、効率性を実現します。 次の表は、RU/秒の観点から、1 KB -100 KB のサイズのアイテムの読み取りと書き込みのコストを示しています。

|**アイテムのサイズ**  |**1 件の読み取りのコスト** |**1 件の書き込みのコスト**|
|---------|---------|---------|
|1 KB |1 RU |5 RU |
|100 KB |10 RU |50 RU |

1 KB のサイズのアイテムを読み取るには、1 RU のコストがかかります。 1 KB のアイテムを書き込むには、5 RU のコストがかかります。 読み取りと書き込みのコストは、既定のセッションである[一貫性レベル](consistency-levels.md)を使用する場合に適用されます。  RU に関する考慮事項には、アイテムのサイズ、プロパティの数、データの整合性、インデックス付きプロパティ、インデックス作成、クエリのパターンなどがあります。

## <a name="normalized-cost-for-1-million-reads-and-writes"></a>100 万件の読み取りと書き込みに対する正規化されたコスト

1,000 RU/秒のプロビジョニングは 360 万 RU/時間に変換され、その 1 時間のコストは 0.08 ドルになります (米国とヨーロッパの場合)。 1 KB のアイテムでは、このプロビジョニング済みスループットにより、1 時間あたり 360 万件の読み取りまたは 72 万件の書き込みを実行できます (この値は `3.6 million RU / 5` として計算)。 100 万件の読み取りと書き込みに正規化され、コストは 100 万件の読み取りに対して 0.022 ドル (この値は $0.08/360 万件として計算)、100 万件の書き込みに対して 0.111 ドル (この値は $0.08/72 万件として計算) となります。

## <a name="number-of-regions-and-the-request-units-cost"></a>リージョンの数と要求ユニットのコスト

書き込みのコストは、Azure Cosmos アカウントに関連付けられたリージョンの数に関係なく一定です。 つまり、1 KB の書き込みは、アカウントに関連付けられたリージョンの数とは無関係に 5 RU のコストがかかります。 各リージョンでレプリケーション トラフィックのレプリケート、受け入れ、および処理に費やされるリソースの量は、少なくありません。 複数リージョンのコストの最適化の詳細については、[複数リージョンの Cosmos アカウント コストの最適化](optimize-cost-regions.md)に関する記事を参照してください。

## <a name="optimize-the-cost-of-writes-and-reads"></a>書き込みと読み取りのコストを最適化する

書き込み操作を実行するときは、1 秒あたりに必要な書き込みの数をサポートするために十分な容量をプロビジョニングする必要があります。 書き込みの実行前に SDK、ポータル、CLI を使用してプロビジョニング済みスループットを増大させ、書き込みの完了後にスループットを減少させることができます。 書き込み期間中のスループットは、指定されたデータに必要な最小スループットと、他のワークロードが実行されていないと仮定した場合に挿入ワークロードに必要なスループットです。 

クエリ/読み取り/更新/削除など、他のワークロードを同時に実行している場合は、これらの操作に必要な要求ユニットもさらに追加する必要があります。 書き込み操作のレートが制限されている場合は、Azure Cosmos DB SDK を使用して再試行/バックオフ ポリシーをカスタマイズできます。 たとえば、レートが制限される要求がわずかな割合になるまで負荷を増加させることができます。 レート制限が発生した場合、クライアント アプリケーションは、指定された再試行間隔中、レートが制限された要求でバックオフする必要があります。 書き込みを再試行する前に、次の再試行までに最小限の時間間隔が必要です。 再試行ポリシーのサポートは、SQL .NET、Java、Node.js、Python SDK、およびサポートされているすべてのバージョンの .NET Core SDK に含まれます。 

また、[Azure Data Factory](../data-factory/connector-azure-cosmos-db.md) を使用して、Azure Cosmos DB にデータを一括挿入したり、サポートされているソース データ ストアから Azure Cosmos DB にデータをコピーしたりできます。 Azure Data Factory は、データを書き込むときに最適なパフォーマンスを提供できるよう、Azure Cosmos DB Bulk API とネイティブに統合されています。

## <a name="next-steps"></a>次の手順

次は、先に進み、以下の各記事で Azure Cosmos DB でのコストの最適化の詳細について学習することができます。

* [開発とテストのための最適化](optimize-dev-test.md)の詳細について学習します
* [Azure Cosmos DB の課金内容の確認](understand-your-bill.md)の詳細について学習します
* [スループット コストの最適化](optimize-cost-throughput.md)の詳細について学習します
* [ストレージ コストの最適化](optimize-cost-storage.md)の詳細について学習します
* [クエリ コストの最適化](optimize-cost-queries.md)の詳細について学習します
* [複数リージョンの Azure Cosmos アカウント コストの最適化](optimize-cost-regions.md)の詳細について学習します
