---
title: Azure Monitor でのアクティビティ ログ アラート
description: アクティビティ ログで特定のイベントが発生した場合に、SMS、Webhook、電子メールなどで通知を受け取ります。
author: msvijayn
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 09/17/2018
ms.author: vinagara
ms.subservice: alerts
ms.openlocfilehash: 5d0819f71405b1bf1d4bef57a8b93d57bc879087
ms.sourcegitcommit: 509e1583c3a3dde34c8090d2149d255cb92fe991
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2019
ms.locfileid: "66244979"
---
# <a name="alerts-on-activity-log"></a>アクティビティ ログ アラート 

## <a name="overview"></a>概要
アクティビティ ログ アラートは、アラートに指定した条件と一致する新しいアクティビティのログ イベントが発生したときにアクティブになるアラートです。 これらは Azure リソースであり、Azure Resource Manager テンプレートを使用して作成できます。 これらは、Azure Portal で作成、更新、削除することもできます。 この記事では、アクティビティ ログ アラートの背後の概念について説明します。 その後、Azure Portal を使用してアクティビティ ログのイベントにアラートを設定する方法について説明します。 使用方法の詳細については、[アクティビティ ログ アラートの作成と管理](alerts-activity-log.md)に関するページをご覧ください。

> [!NOTE]
> アクティビティ ログのアラートのカテゴリに含まれるイベントに対して、アラートを作成することは**できません**。

通常、アクティビティ ログ アラートを作成して、通知を受け取るのは次の場合です。

* Azure サブスクリプションでリソースに特定の操作が発生した場合。多くの場合、特定のリソース グループまたはリソースを対象とします。 たとえば、myProductionResourceGroup 内の仮想マシンが削除されたときに通知を受け取ることができます。 また、サブスクリプション内のユーザーに新しい役割が割り当てられた場合に通知を受け取ることもできます。
* サービス正常性イベントが発生した場合。 サービス正常性イベントには、サブスクリプション内のリソースに適用されるインシデント イベントとメンテナンス イベントの通知が含まれます。

アクティビティ ログに対してアラート ルールを作成する状況を簡単にたとえるとすれば、[Azure portal のアクティビティ ログ](activity-log-view.md#azure-portal)でイベントを探索したりフィルター処理したりするのに似ています。 Azure Monitor のアクティビティ ログでは、必要なイベントを検索またはフィルター処理した後、 **[アクティビティ ログ アラートの追加]** ボタンを使用することでアラートを作成できます。

いずれの場合でも、アクティビティ ログ アラートでは、アラートが作成されたサブスクリプション内のイベントのみが監視されます。

JSON オブジェクトの任意の最上位プロパティに基づいて、アクティビティ ログ イベントのアクティビティ ログ アラートを構成できます。 詳細については、[Azre アクティビティ ログの概要](./activity-logs-overview.md#categories-in-the-activity-log)に関する記事を参照してください。 サービス正常性イベントについて詳しくは、[サービス通知のアクティビティ ログ アラートの受け取り](./alerts-activity-log-service-notifications.md)に関する記事をご覧ください。 

アクティビティ ログ アラートには、次のような一般的なオプションがいくつか用意されています。

- **[カテゴリ]** : [管理]、[サービス正常性]、[自動スケール]、[セキュリティ]、[ポリシー]、[推奨]。 
- **[スコープ]** : アクティビティ ログのアラートを定義する対象となる個々のリソースまたはリソースのセット。 アクティビティ ログ アラートのスコープは、さまざまなレベルで定義できます。
    - リソース レベル:特定の仮想マシンなど
    - リソース グループ レベル:特定のリソース グループ内のすべての仮想マシンなど
    - サブスクリプション レベル:サブスクリプション内のすべての仮想マシンや、サブスクリプション内のすべてのリソースなど
- **[リソース グループ]** : 既定では、アラート ルールは、[スコープ] での定義対象となっているのと同じリソース グループに保存されます。 ユーザーは、アラート ルールを格納するリソース グループを定義することもできます。
- **[リソースの種類]** :アラートの対象として、Resource Manager で定義されている名前空間。

- **[操作名]** : Resource Manager のロールベースのアクセス制御の操作名。
- **[レベル]** : イベントの重大度レベル ([詳細]、[情報]、[警告]、[エラー]、[重大])。
- **[状態]** : イベントの状態 (通常は [開始]、[失敗]、または [成功])。
- **[イベント開始者]** : "呼び出し元" とも呼ばれます。 操作を実行したユーザーの電子メール アドレスまたは Azure Active Directory 識別子。

> [!NOTE]
> 1 つのサブスクリプション内では、1 つのリソース レベル、リソース グループ内のすべてのリソース レベル、またはサブスクリプション レベル全体というスコープのアクティビティについて、最大 100 個のアラート ルールを作成できます。

アクティビティ ログ アラートがアクティブになると、アクションまたは通知の生成にアクション グループが使用されます。 アクション グループは、通知レシーバー (電子メール アドレス、webhook URL、または SMS の電話番号) の再利用可能なセットです。 これらのレシーバーは、複数のアラートから参照でき、通知チャネルの一元管理とグループ化を行うことができます。 アクティビティ ログ アラートを定義するときには 2 つの方法があります。 次のようにすることができます。

* アクティビティ ログ アラートで既存のアクション グループを使用します。
* 新しいアクション グループを作成できます。

アクション グループの詳細については、「[Azure Portal でのアクション グループの作成および管理](action-groups.md)」を参照してください。


## <a name="next-steps"></a>次の手順
- [アラートの概要](alerts-overview.md)について把握します。
- [アクティビティ ログ アラートの作成と変更](alerts-activity-log.md)について学習します。
- [アクティビティ ログ アラート webhook スキーマ](activity-log-alerts-webhook.md)を確認します。
- [サービス正常性の通知](service-notifications.md)について学習します。


