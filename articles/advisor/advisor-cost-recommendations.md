---
title: Azure Advisor を使用してサービスのコストを削減する | Microsoft Docs
description: Azure Advisor を使用して、Azure のデプロイにかかるコストを最適化します。
services: advisor
documentationcenter: NA
author: kasparks
ms.service: advisor
ms.topic: article
ms.date: 01/29/2019
ms.author: kasparks
ms.openlocfilehash: fef7b82e6969de16d1815250d2373c99021b0e86
ms.sourcegitcommit: 25a60179840b30706429c397991157f27de9e886
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66254719"
---
# <a name="reduce-service-costs-using-azure-advisor"></a>Azure Advisor を使用してサービス コストを削減する

Advisor は、アイドル状態にあるリソースや活用されていないリソースを識別することによって Azure を最適化し、総合的な Azure の支出を削減します。 コストに関する推奨事項は、Advisor ダッシュボードの **[コスト]** タブで取得できます。

## <a name="optimize-virtual-machine-spend-by-resizing-or-shutting-down-underutilized-instances"></a>使用率が低いインスタンスをサイズ変更またはシャットダウンして仮想マシンの支出を最適化する 

特定のアプリケーション シナリオでは、設計によっては使用率が低くなる場合がありますが、多くの場合、仮想マシンのサイズと数を管理することによってコストを削減できます。 Advisor は、仮想マシンの使用状況を 7 日間にわたって監視して、使用率が低い仮想マシンを識別します。 仮想マシンは、CPU 使用率が 5% 以下およびネットワーク使用率が 2% 以下の場合、または現在のワークロードがより小さい仮想マシン サイズで対応できる場合に、使用率が低いと見なされます。

Advisor には、そのような仮想マシンの使用を継続した場合の推定コストが示され、シャット ダウンまたはサイズ変更を選択できます。

使用率が低い仮想マシンを積極的に特定する場合は、サブスクリプションごとに平均 CPU 使用率ルールを調整できます。

## <a name="reduce-costs-by-eliminating-unprovisioned-expressroute-circuits"></a>プロビジョニングが解除された ExpressRoute 回線を排除してコストを削減する

Advisor は、プロバイダーの状態が 1 か月以上 "*未プロビジョニング*" である ExpressRoute 回線を特定し、接続プロバイダーを使用してその回線をプロビジョニングする予定がない場合は回線を削除するよう勧めます。

## <a name="reduce-costs-by-deleting-or-reconfiguring-idle-virtual-network-gateways"></a>アイドル状態の仮想ネットワーク ゲートウェイを削除または再構成してコストを削減する

Advisor は、90 日以上アイドル状態にあった仮想ネットワークのゲートを特定します。 これらのゲートウェイは 1 時間単位で課金されるので、もう使用しない予定の場合は、再構成または削除を検討する必要がありあす。 

## <a name="buy-reserved-virtual-machine-instances-to-save-money-over-pay-as-you-go-costs"></a>従量課金のコストより費用を節約するために、予約された仮想マシン インスタンスを購入する

Advisor は、過去 30 日間の仮想マシンの使用率を確認し、Azure Reservation を購入することでコストを節約できるかどうかを判断します。 Advisor は、最も節約できる可能性がある領域とサイズを示し、Reservation を購入することによって見込める節約を示します。 Azure Reservation では、お使いの仮想マシンの基本コストを事前購入できます。 割引は、Reservation と同じサイズと領域の新しいまたは既存の VM に自動適用されます。 [Azure Reserved VM Instances の詳細を参照してください。](https://azure.microsoft.com/pricing/reserved-vm-instances/)

Advisor では、予約インスタンスについて、残り 30 日で有効期限が切れることも通知されます。 従量課金制での支払いを避けるために、新しい予約インスタンスを購入することが推奨されます。

## <a name="delete-unassociated-public-ip-addresses-to-save-money"></a>関連付けられていないパブリック IP アドレスのコスト節約のための削除

Advisor は、ロード バランサーまたは仮想マシンなどの Azure リソースに現在関連付けられていないパブリック IP アドレスを識別します。 これらのパブリック IP アドレスには、わずかな料金がかかります。 それらを使用する予定がない場合は、削除するとコスト削減につながります。

## <a name="delete-azure-data-factory-pipelines-that-are-failing"></a>障害が発生している Azure Data Factory パイプラインを削除する

Azure Advisor は、繰り返し障害が発生している Azure Data Factory パイプラインを検出し、その問題を解決するか、または障害が発生しているパイプラインを必要なくなっている場合は削除することを推奨します。 障害発生中にサービスが提供されていない場合でも、これらのパイプラインに対して課金されます。 

## <a name="use-standard-snapshots-for-managed-disks"></a>マネージド ディスクに Standard スナップショットを使用する
コストの 60% を節約するために、親ディスクのストレージの種類には関係なく、スナップショットを Standard Storage に格納することをお勧めします。 これは、マネージド ディスクのスナップショットの既定オプションです。 Azure Advisor は、Premium Storage に格納されているスナップショットを識別し、スナップショットを Premium Storage から Standard Storage に移行することを推奨します。 [マネージド ディスクの価格](https://aka.ms/aa_manageddisksnapshot_learnmore)の詳細を確認してください。

## <a name="how-to-access-cost-recommendations-in-azure-advisor"></a>Azure Advisor のコストに関する推奨事項にアクセスする方法

1. [Azure Portal](https://portal.azure.com) にサインインし、[Advisor](https://aka.ms/azureadvisordashboard) を開きます。

2.  Advisor ダッシュボードで、 **[コスト]** タブをクリックします。

## <a name="next-steps"></a>次の手順

Advisor の推奨事項の詳細については、以下を参照してください。
* [Advisor 入門](advisor-overview.md)
* [作業の開始](advisor-get-started.md)
* [Advisor のパフォーマンスに関する推奨事項](advisor-cost-recommendations.md)
* [Advisor の高可用性に関する推奨事項](advisor-cost-recommendations.md)
* [Advisor のセキュリティに関する推奨事項](advisor-cost-recommendations.md)
