---
title: Azure Monitor で使用するデータのソース | Microsoft Docs
description: Azure リソースとそれらで実行されているアプリケーションの正常性とパフォーマンスを監視するために使用できるデータについて説明します。
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.service: azure-monitor
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2019
ms.author: bwren
ms.openlocfilehash: b77fb3ab5651147c59b9f0afd22a2d6d0159c90e
ms.sourcegitcommit: 8e76be591034b618f5c11f4e66668f48c090ddfd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66357449"
---
# <a name="sources-of-monitoring-data-for-azure-monitor"></a>Azure Monitor で使用する監視データのソース
Azure Monitor は、[ログ](data-platform-logs.md)と[メトリック](data-platform-metrics.md)を含む[一般的な監視データ プラットフォーム](data-platform.md)をベースにしています。 このプラットフォームにデータを収集すれば、Azure Monitor にある共通のツール一式を使用して、複数のリソースからのデータをまとめて分析することができます。 特定のシナリオに対応するために監視データは他の場所に送信されることがあるほか、一部のリソースについては、他の場所に書き込まれた後で、ログやメトリックに収集されることもあります。

この記事では、Azure リソースによって作成される監視データのほかにも、Azure Monitor によって収集されるさまざまな監視データのソースについて説明します。 このデータをさまざまな場所で収集するために必要な構成について、詳しい情報が書かれているページへのリンクを掲載しています。

## <a name="application-tiers"></a>アプリケーション層

Azure アプリケーションの監視データのソースは階層に分類できます。最上位の階層はアプリケーション自体で、その下にある各階層は Azure プラットフォームのコンポーネントです。 階層によって、データへのアクセス方法が異なります。 以下の表にアプリケーションの各階層をまとめ、それぞれの階層の監視データのソースを後続のセクションで取り上げます。 それぞれのデータの場所とそのアクセス方法の説明については、[Azure における監視データの場所](data-locations.md)に関するページを参照してください。


![監視の階層](../media/overview/overview.png)


### <a name="azure"></a>Azure
Azure に固有のアプリケーションの階層について、次の表で簡単に説明します。 リンクを辿って、後続のセクションに示されているそれぞれの詳細を確認してください。

| レベル | 説明 | 収集方法 |
|:---|:---|:---|
| [Azure テナント](#azure-tenant) | Azure Active Directory など、テナント レベルの Azure サービスの操作に関するデータ。 | AAD データをポータルで確認するか、テナントの診断設定を使用して Azure Monitor への収集を構成します。 |
| [Azure サブスクリプション](#azure-subscription) | Azure サブスクリプションにおけるリソース横断的なサービス (Resource Manager、Service Health など) の正常性と管理に関連するデータ。 | ポータルで確認するか、ログ プロファイルを使用して Azure Monitor への収集を構成します。 |
| [Azure リソース](#azure-resources) |  各 Azure リソースの運用とパフォーマンスに関するデータ。 | 自動的に収集されたメトリックをメトリックス エクスプローラーで確認します。<br>Azure Monitor でログを収集するように診断設定を構成します。<br>各種の監視ソリューションと Insights を利用すれば、特定の種類のリソースをさらに詳しく監視することができます。 |

### <a name="azure-other-cloud-or-on-premises"></a>Azure やその他のクラウド、またはオンプレミス 
Azure やその他のクラウド、またはオンプレミスに存在する可能性のあるアプリケーションの階層について、次の表で簡単に説明します。 リンクを辿って、後続のセクションに示されているそれぞれの詳細を確認してください。

| レベル | 説明 | 収集方法 |
|:---|:---|:---|
| [オペレーティング システム (ゲスト)](#operating-system-guest) | オペレーティング システムのコンピューティング リソースに関するデータ。 | Log Analytics エージェントをインストールして Azure Monitor にクライアント データ ソースを収集すると共に、Dependency Agent をインストールして Azure Monitor for VMs をサポートする依存関係を収集します。<br>Azure 仮想マシンについては、Azure Diagnostics 拡張機能をインストールして、ログとメトリックを Azure Monitor に収集します。 |
| [アプリケーション コード](#application-code) | 実際のアプリケーションとコードのパフォーマンスと機能に関するデータ (パフォーマンス トレース、アプリケーション ログ、ユーザー テレメトリを含む)。 | Application Insights にデータを収集するためにコードをインストルメント化します。 |
| [カスタム ソース](#custom-sources) | 外部サービスからのデータや、他のコンポーネントまたはデバイスからのデータ。 | 任意の REST クライアントからログまたはメトリック データを Azure Monitor に収集します。 |

## <a name="azure-tenant"></a>Azure テナント
Azure テナントに関連するテレメトリは、Azure Active Directory などのテナント全体のサービスから収集されます。

![Azure テナントの収集](media/data-sources/tenant.png)

### <a name="azure-active-directory-audit-logs"></a>Azure Active Directory 監査ログ
[Azure Active Directory レポート](../../active-directory/reports-monitoring/overview-reports.md)には、サインイン アクティビティの履歴と、特定のテナント内で行われた変更の監査証跡が含まれています。 

| 宛先 | 説明 | リファレンス |
|:---|:---|:---|
| Azure Monitor ログ | Azure AD ログを Azure Monitor で収集して他の監視データと共に分析するように構成します。 | [Azure AD ログを Azure Monitor ログと統合する (プレビュー)](../../active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics.md) |
| Azure Storage | アーカイブのために Azure AD ログを Azure Storage にエクスポートします。 | [チュートリアル:Azure AD ログを Azure ストレージ アカウントにアーカイブする (プレビュー)](../../active-directory/reports-monitoring/quickstart-azure-monitor-route-logs-to-storage-account.md) |
| イベント ハブ | Event Hubs を使用して Azure AD ログを他の場所にストリーム配信します。 | [チュートリアル:Azure Active Directory ログを Azure イベント ハブにストリーム配信する (プレビュー)](../../active-directory/reports-monitoring/tutorial-azure-monitor-stream-logs-to-event-hub.md)。 |



## <a name="azure-subscription"></a>Azure サブスクリプション
Azure サブスクリプションの正常性と運用に関連したテレメトリです。

![Azure サブスクリプション](media/data-sources/azure-subscription.png)

### <a name="azure-activity-log"></a>Azure アクティビティ ログ 
[Azure アクティビティ ログ](activity-logs-overview.md)には、サービスの正常性レコードのほか、ご自分の Azure サブスクリプションのリソースに対して行われた構成の変更に関するレコードが含まれています。 アクティビティ ログは、すべての Azure リソースについて記録されます。このログはリソースの _外部_  ビューを表します。

| 宛先 | 説明 | リファレンス |
|:---|:---|
| アクティビティ ログ | アクティビティ ログは、その独自のデータ ストアに収集されます。それを Azure Monitor のメニューから表示したり、それを使ってアクティビティ ログ アラートを作成したりできます。 | [Azure portal でアクティビティ ログに対してクエリを実行する](activity-log-view.md#azure-portal) |
| Azure Monitor ログ | アクティビティ ログを収集して他の監視データと共に分析するように Azure Monitor ログを構成します。 | [Azure Monitor の Log Analytics ワークスペースで Azure アクティビティ ログを収集して分析する](activity-log-collect.md) |
| Azure Storage | アーカイブのためにアクティビティ ログを Azure Storage にエクスポートします。 | [アクティビティ ログをアーカイブする](activity-log-export.md#archive-activity-log)  |
| Event Hubs | Event Hubs を使用してアクティビティ ログを他の場所にストリーム配信します。 | [アクティビティ ログをイベント ハブにストリーム配信する](activity-log-export.md#stream-activity-log-to-event-hub)。 |

### <a name="azure-service-health"></a>Azure Service Health
[Azure Service Health](../../service-health/service-health-overview.md) は、アプリケーションとリソースが依存するサブスクリプション内の Azure サービスの正常性に関する情報を提供します。

| 宛先 | 説明 | リファレンス |
|:---|:---|:---|
| アクティビティ ログ<br>Azure Monitor ログ | Service Health のレコードは、Azure のアクティビティ ログに保存されるため、Azure portal で表示したり、アクティビティ ログを使って実行できる他のあらゆるアクティビティを実行したりすることができます。 | [Azure Portal を使用したサービス正常性通知の表示](service-notifications.md) |


## <a name="azure-resources"></a>Azure リソース
メトリックおよびリソース レベルの診断ログは、Azure リソースの_内部_操作に関する情報を提供します。 これらはほとんどの Azure サービスで利用できます。また、特定のサービスについては、さらに詳しいデータが監視ソリューションおよび Insights によって収集されます。

![Azure リソースの収集](media/data-sources/azure-resources.png)


### <a name="platform-metrics"></a>プラットフォームのメトリック 
ほとんどの Azure サービスからは、そのパフォーマンスと操作を反映する[プラットフォーム メトリック](data-platform-metrics.md)が直接メトリック データベースに送信されます。 [リソースの種類によってメトリックは異なります](metrics-supported.md)。 

| 宛先 | 説明 | リファレンス |
|:---|:---|:---|
| Azure Monitor メトリック | プラットフォームのメトリックは、何も構成しなくても、Azure Monitor メトリック データベースに書き込まれます。 プラットフォームのメトリックには、メトリックス エクスプローラーからアクセスします。  | [Azure メトリックス エクスプローラーの概要](metrics-getting-started.md)<br>[Azure Monitor のサポートされるメトリック](metrics-supported.md) |
| Azure Monitor ログ | プラットフォームのメトリックをログにコピーし、Log Analytics を使用して傾向分析など各種の分析を実行します。 | [Azure Diagnostics から Log Analytics に直接](collect-azure-metrics-logs.md#azure-diagnostics-direct-to-log-analytics) |
| Event Hubs | Event Hubs を使用してメトリックを他の場所にストリーム配信します。 |[外部ツールで使用する Azure 監視データのイベント ハブへのストリーミング](stream-monitoring-data-event-hubs.md) |

### <a name="diagnostic-logs"></a>診断ログ
[診断ログ](diagnostic-logs-overview.md)からは、Azure リソースの "_内部_" 操作に関する分析情報が得られます。  既定では、診断ログは有効になっていません。 明示的にそれらを有効にし、リソースごとに宛先を指定する必要があります。 

診断ログの構成要件と内容はリソースの種類によって異なり、まだ診断ログの作成に対応していないサービスもあります。 それぞれのサービスについての詳細と詳しい構成手順へのリンクについては、「[Azure 診断ログでサポートされているサービス、スキーマ、カテゴリ](diagnostic-logs-schema.md)」を参照してください。 この記事に掲載されていないサービスは現在、診断ログへの書き込みに対応していません。

| 宛先 | 説明 | リファレンス |
|:---|:---|:---|
| Azure Monitor ログ | 診断ログを Azure Monitor ログに送信して、収集された他のログ データと共に分析します。 Azure Monitor に直接書き込むことのできるリソースと、ストレージ アカウントに書き込んでから Log Analytics ワークスペースにインポートするリソースがあります。 | [Azure Monitor の Log Analytics ワークスペースに Azure 診断ログをストリーム配信する](diagnostic-logs-stream-log-store.md)<br>[Azure portal を使用して Azure Storage からログを収集する](azure-storage-iis-table.md#use-the-azure-portal-to-collect-logs-from-azure-storage)  |
| Storage | アーカイブのために診断ログを Azure Storage に送信します。 | [Azure 診断ログのアーカイブ](archive-diagnostic-logs.md) |
| Event Hubs | Event Hubs を使用して診断ログを他の場所にストリーム配信します。 |[Azure 診断ログをイベント ハブにストリーム配信する](diagnostic-logs-stream-event-hubs.md) |

## <a name="operating-system-guest"></a>オペレーティング システム (ゲスト)
Azure、他のクラウド、オンプレミスのコンピューティング リソースには、監視対象のゲスト オペレーティング システムがあります。 1 つ以上のエージェントがインストールされている場合、ゲストからのテレメトリを Azure Monitor に収集し、Azure サービス本体と同じ監視ツールを使用して分析することができます。

![Azure コンピューティング リソースの収集](media/data-sources/compute-resources.png)

### <a name="azure-diagnostic-extension"></a>Azure 診断の拡張機能
Azure 仮想マシンに対して Azure Diagnostics 拡張機能を有効にすると、Azure Cloud Services (クラシック) の Web ロールと worker ロール、Virtual Machines、仮想マシン スケール セット、Service Fabric など、Azure コンピューティング リソースのゲスト オペレーティング システムからログとメトリックを収集することができます。

| 宛先 | 説明 | リファレンス |
|:---|:---|:---|
| Storage | Diagnostics 拡張機能を有効にした場合、その書き込み先は、既定ではストレージ アカウントになります。 | [Azure Storage への診断データの保存と表示](diagnostics-extension-to-storage.md) |
| Azure Monitor メトリック | パフォーマンス カウンターを収集するように Diagnostics 拡張機能を構成した場合、それらは Azure Monitor メトリック データベースに書き込まれます。 | [Windows 仮想マシンの Resource Manager テンプレートを使用してゲスト OS メトリックを Azure Monitor メトリック ストアに送信する](collect-custom-metrics-guestos-resource-manager-vm.md) |
| Application Insights のログ | アプリケーションをサポートするコンピューティング リソースからログとパフォーマンス カウンターを収集して、他のアプリケーション データと共に分析します。 | [Cloud Services、Virtual Machines、または Service Fabric の診断データを Application Insights に送信する](diagnostics-extension-to-application-insights.md) |
| Event Hubs | Event Hubs を使用して他の場所にデータをストリーム配信するように Diagnostics 拡張機能を構成します。  | [Event Hubs を利用してホット パスの Azure Diagnostics データをストリーム配信する](diagnostics-extension-stream-event-hubs.md) |

### <a name="log-analytics-agent"></a>Log Analytics エージェント 
Windows 仮想マシンまたは Linux 仮想マシンを包括的に監視および管理するには、Log Analytics エージェントをインストールします。 仮想マシンは Azure、別のクラウド、またはオンプレミスで実行できます。

| 宛先 | 説明 | リファレンス |
|:---|:---|:---|
| Azure Monitor ログ | Log Analytics エージェントは、Azure Monitor に直接接続するか、System Center Operations Manager を経由して接続します。エージェントを使用すると、自分が構成したデータ ソースのほか、仮想マシン上で実行されているアプリケーションについての追加の分析情報が得られる監視ソリューションから、データを収集することができます。 | [Azure Monitor のエージェント データ ソース](agent-data-sources.md)<br>[Operations Manager を Azure Monitor に接続する](om-agents.md) |


### <a name="azure-monitor-for-vms"></a>VM に対する Azure Monitor 
[Azure Monitor for VMs](../insights/vminsights-overview.md) は、仮想マシン用にカスタマイズされた監視エクスペリエンスを備え、サービスの状態や VM の正常性など、Azure Monitor の主要機能を超える機能が用意されています。 Windows 仮想マシンおよび Linux 仮想マシンには Dependency Agent が必要となります。これが Log Analytics エージェントと統合されて、仮想マシン上で実行されているプロセスや外部プロセスの依存関係について検出されたデータを収集します。

| 宛先 | 説明 | リファレンス |
|:---|:---|:---|
| Azure Monitor ログ | プロセスや依存関係についてのデータをエージェントに格納します。 | [Azure Monitor for VMs (プレビュー) のマップを使用してアプリケーション コンポーネントを把握する](../insights/vminsights-maps.md) |
| VM ストレージ | Azure Monitor for VMs は、正常性状態情報をカスタムの場所に格納します。 これは、[Azure Resource Health REST API](/rest/api/resourcehealth/) のほか、Azure portal の Azure Monitor for VMs からのみ利用することができます。 | [Azure 仮想マシンの正常性を把握する](../insights/vminsights-health.md)<br>[Azure Resource Health REST API](https://docs.microsoft.com/rest/api/resourcehealth/) |



## <a name="application-code"></a>アプリケーション コード
Azure Monitor における詳しいアプリケーションの監視は、さまざまなプラットフォーム上で動作するアプリケーションからデータを収集する [Application Insights](https://docs.microsoft.com/azure/application-insights/) を通じて行われます。 アプリケーションは Azure、別のクラウド、またはオンプレミスで実行できます。

![アプリケーション データの収集](media/data-sources/applications.png)


### <a name="application-data"></a>アプリケーション データ
インストルメンテーション パッケージをインストールすることでアプリケーションに対して有効にした Application Insights は、アプリケーションのパフォーマンスおよび操作に関連するメトリックとログを収集します。 Application Insights によって収集されたデータは、他のデータ ソースによって使用されるのと同じ Azure Monitor データ プラットフォームに格納されます。 このデータを分析するためのさまざまなツールが用意されていますが、メトリックス エクスプローラーや Log Analytics などのツールを使用して、他のソースのデータと共に分析を行うこともできます。

| 宛先 | 説明 | リファレンス |
|:---|:---|:---|
| Azure Monitor ログ | アプリケーションについての運用データ (ページ ビュー、アプリケーション要求、例外、トレースなど)。 | [Azure Monitor でログ データを分析する](../log-query/log-query-overview.md) |
|                    | アプリケーション マップとテレメトリの関連付けをサポートするアプリケーション コンポーネント間の依存関係情報。 | [Application Insights におけるテレメトリの相関付け](../app/correlation.md) <br> [アプリケーション マップ](../app/app-map.md) |
|            | パブリック インターネット上のさまざまな場所からアプリケーションの可用性と応答性をテストする可用性テストの結果。 | [Web サイトの可用性と応答性の監視](../app/monitor-web-app-availability.md) |
| Azure Monitor メトリック | Application Insights は、アプリケーションに定義されたカスタム メトリックに加え、アプリケーションのパフォーマンスと動作を表すメトリックを Azure Monitor メトリック データベースに収集します。 | [Application Insights のログベースのメトリックと事前に集計されたメトリック](../app/pre-aggregated-metrics-log-metrics.md)<br>[カスタムのイベントとメトリックのための Application Insights API](../app/api-custom-events-metrics.md) |
| Azure Storage | アーカイブのためにアプリケーション データを Azure Storage に送信します。 | [Application Insights からのテレメトリのエクスポート](../app/export-telemetry.md) |
|            | 可用性テストの詳細は Azure Storage に格納されます。 Azure portal で Application Insights を使用してダウンロードし、ローカル分析を行います。 可用性テストの結果は Azure Monitor ログに格納されます。 | [Web サイトの可用性と応答性の監視](../app/monitor-web-app-availability.md) |
|            | プロファイラーのトレース データは Azure Storage に格納されます。 Azure portal で Application Insights を使用してダウンロードし、ローカル分析を行います。  | [Application Insights を使用した Azure のプロファイル運用アプリケーション](../app/profiler-overview.md) 
|            | 例外のサブセットを得るためにキャプチャされたデバッグのスナップショット データは、Azure Storage に格納されます。 Azure portal で Application Insights を使用してダウンロードし、ローカル分析を行います。  | [スナップショットのしくみ](../app/snapshot-debugger.md#how-snapshots-work) |

## <a name="monitoring-solutions-and-insights"></a>監視ソリューションと Insights
[監視ソリューション](../insights/solutions.md)と [Insights](../insights/insights-overview.md) は、データを収集して、特定のサービスやアプリケーションの操作に関する追加の分析情報を提供します。 アプリケーションのさまざまな階層 (場合によっては複数の階層) に存在するリソースに対応することもできます。

### <a name="monitoring-solutions"></a>監視ソリューション

| 宛先 | 説明 | リファレンス
|:---|:---|:---|
| Azure Monitor ログ | 監視ソリューションは、データを Azure Monitor ログに収集します。そこで、クエリ言語や、通常はソリューションに含まれている[ビュー](view-designer.md)を使用して、そのデータを分析できます。 | [Azure における監視ソリューションのデータ収集の詳細](../insights/solutions-inventory.md) |


### <a name="azure-monitor-for-containers"></a>Azure Monitor for Containers
[Azure Monitor for Containers](../insights/container-insights-overview.md) は、[Azure Kubernetes Service (AKS)](/azure/aks/) 用にカスタマイズされた監視エクスペリエンスを備えています。 次の表に示すリソースについての追加データが収集されます。

| 宛先 | 説明 | リファレンス |
|:---|:---|:---|
| Azure Monitor ログ | インベントリ、ログ、イベントといった AKS の監視データを格納します。 ポータルでログの分析機能を活用するために、メトリック データはログにも格納されます。 | [コンテナーの Azure Monitor を使用して AKS クラスターのパフォーマンスを把握する](../insights/container-insights-analyze.md) |
| Azure Monitor メトリック | メトリック データはメトリック データベースに格納されて、可視化とアラートの源泉となります。 | [メトリックス エクスプローラーでコンテナーのメトリックを表示する](../insights/container-insights-analyze.md#view-container-metrics-in-metrics-explorer) |
| Azure Kubernetes Service | ほぼリアルタイムのエクスペリエンスを実現するために、Azure Monitor for Containers は、Azure Kubernetes Service から直接 Azure portal にデータを提示します。 | [コンテナー用 Azure Monitor でコンテナー ログをリアルタイムで表示する方法 (プレビュー)](../insights/container-insights-live-logs.md) |

### <a name="azure-monitor-for-vms"></a>VM に対する Azure Monitor
[Azure Monitor for VMs](../insights/vminsights-overview.md) は、仮想マシンの監視用にカスタマイズされたエクスペリエンスを備えています。 Azure Monitor for VMs によって収集されるデータについては、前出の「[オペレーティング システム (ゲスト)](#operating-system-guest)」セクションで説明しています。

## <a name="custom-sources"></a>カスタム ソース
アプリケーションの標準的な階層に加え、他のデータ ソースで収集できないテレメトリがある他のリソースを監視することが必要な場合があります。 これらのリソースについては、Azure Monitor API を使用してこのデータをメトリックまたはログに書き込んでください。

![カスタムの収集](media/data-sources/custom.png)

| 宛先 | Method | 説明 | リファレンス |
|:---|:---|:---|:---|
| Azure Monitor ログ | データ コレクター API | ログ データを任意の REST クライアントから収集して、Log Analytics ワークスペースに格納します。 | [HTTP データ コレクター API を使用して Azure Monitor にログ データを送信する (パブリック プレビュー)](data-collector-api.md) |
| Azure Monitor メトリック | カスタム メトリックス API | メトリック データを任意の REST クライアントから収集して、Azure Monitor メトリック データベースに格納します。 | [REST API を使用して Azure リソースのカスタム メトリックを Azure Monitor メトリック ストアに送信する](metrics-store-custom-rest-api.md) |


## <a name="other-services"></a>その他のサービス
Azure のその他のサービスでは、Azure Monitor データ プラットフォームにデータが書き込まれます。 そのため、これらのサービスによって収集されたデータは、Azure Monitor によって収集されるデータと一緒に分析でき、同じ分析ツールと可視化ツールを活用することができます。

| Service | 宛先 | 説明 | リファレンス |
|:---|:---|:---|:---|
| [Azure Security Center](/azure/security-center/) | Azure Monitor ログ | Azure Security Center によって収集されたセキュリティ データは Log Analytics ワークスペースに格納され、Azure Monitor によって収集される他のログ データと一緒に分析することができます。  | [Azure Security Center でのデータ収集](../../security-center/security-center-enable-data-collection.md) |
| [Azure Sentinel](/azure/sentinel/) | Azure Monitor ログ | Azure Sentinel によってさまざまなデータ ソースから収集されたデータは Log Analytics ワークスペースに格納され、Azure Monitor によって収集される他のログ データと一緒に分析することができます。  | [データ ソースの接続](/azure/sentinel/quickstart-onboard) |


## <a name="next-steps"></a>次の手順

- [Azure Monitor によって収集される監視データの種類](data-platform.md)と、このデータを表示および分析する方法の詳細を確認します。
- [Azure リソースからのデータが格納されるさまざまな場所](data-locations.md)とそのアクセス方法を列挙します。 
