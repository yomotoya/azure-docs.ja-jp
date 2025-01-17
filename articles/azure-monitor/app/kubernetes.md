---
title: Application Insights を使用して Azure Kubernetes Service (AKS) またはその他の Kubernetes でホストされたアプリケーション - Azure Monitor | Microsoft Docs
description: Azure Monitor では、Kubernetes クラスター上でサービス メッシュ技術である Istio を利用して、Kubernetes でホストされているアプリケーションに対してアプリケーションの監視を提供しています。 これにより、クラスター内で実行されるポッドでの受信および送信要求に関する Application Insights テレメトリを収集できます。
services: application-insights
author: tokaplan
manager: carmonm
ms.service: application-insights
ms.topic: conceptual
ms.date: 04/25/2019
ms.author: alkaplan
ms.openlocfilehash: c94d589875195207ec6f71c35ad077cac281fda5
ms.sourcegitcommit: 9e8dfa1169a55c3c8af93a6c5f4e0dace4de48b2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2019
ms.locfileid: "65555834"
---
# <a name="zero-instrumentation-application-monitoring-for-kubernetes-hosted-applications"></a>Kubernetes でホストされるアプリケーションに対するゼロ インストルメンテーション アプリケーション監視

> [!IMPORTANT]
> 現在この機能はパブリック プレビュー版です。
> このプレビュー バージョンはサービス レベル アグリーメントなしで提供されています。運用環境のワークロードに使用することはお勧めできません。 特定の機能はサポート対象ではなく、機能が制限されることがあります。
> 詳しくは、[Microsoft Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)に関するページをご覧ください。

現在、Azure Monitor では、Kubernetes クラスターでのサービス メッシュ技術を利用して、Kubernetes でホストされているアプリに対する標準のアプリケーション監視が提供されています。 既定の Application Insight は、依存関係をモデル化するための[アプリケーション マップ](../../azure-monitor/app/app-map.md)、リアルタイムの監視のための [Live Metrics Stream](../../azure-monitor/app/live-stream.md)、[既定のダッシュボード](../../azure-monitor/app/overview-dashboard.md)での強力な視覚化、[メトリックス エクスプローラー](../../azure-monitor/platform/metrics-getting-started.md)、[Workbooks](../../azure-monitor/app/usage-workbooks.md) などの機能を備えています。 この機能は、選択した Kubernetes 名前空間内のすべての Kubernetes ワークロードでパフォーマンスのボトルネックや障害のホットスポットをユーザーが特定するのに役立ちます。 Istio などのテクノロジでの既存のサービス メッシュへの投資を利用することにより、Azure Monitor では、アプリケーションのコードを変更することなく、自動的にインストルメント化されたアプリ監視を実現できます。

> [!NOTE]
> これは、Kubernetes でアプリケーションの監視を実行するさまざまな方法の 1 つです。 [Application Insights SDK](../../azure-monitor/azure-monitor-app-hub.md) を使用することで、サービス メッシュの必要なしに、Kubernetes でホストされているアプリをインストルメント化することもできます。 SDK でアプリケーションをインストルメント化することなく Kubernetes を監視するには、以下の方法を使用できます。

## <a name="prerequisites"></a>前提条件

- [Kubernetes クラスター](https://docs.microsoft.com/azure/aks/concepts-clusters-workloads)。
- *kubectl* を実行するためのクラスターへのコンソール アクセス。
- [Application Insight リソース](create-new-resource.md)
- サービス メッシュを用意します。 クラスターに Istio がデプロイされていない場合は、[Azure Kubernetes Service に Istio をインストールして使用する](https://docs.microsoft.com/azure/aks/istio-install)方法を確認してください。

## <a name="capabilities"></a>機能

Kubernetes でホストされたアプリのゼロ インストルメンテーション アプリケーション監視を使用することで、次のものを使用できます。

- [アプリケーション マップ](../../azure-monitor/app/app-map.md)
- [Live Stream Metrics](../../azure-monitor/app/live-stream.md)
- [ダッシュボード](../../azure-monitor/app/overview-dashboard.md)
- [メトリックス エクスプローラー](../../azure-monitor/platform/metrics-getting-started.md)
- [分散トレース](../../azure-monitor/app/distributed-tracing.md)
- [エンド ツー エンド トランザクション監視](../../azure-monitor/learn/tutorial-performance.md#identify-slow-server-operations)

## <a name="installation-steps"></a>インストール手順

ソリューションを有効にするには、次の手順を実行します。
- アプリケーションをデプロイします (まだデプロイされていない場合)。
- アプリケーションがサービス メッシュの一部であることを確認します。
- 収集されたテレメトリを確認します。

### <a name="configure-your-app-to-work-with-a-service-mesh"></a>サービス メッシュで動作するようにアプリを構成する

Istio では、[ポッドをインストルメント化する](https://istio.io/docs/setup/kubernetes/additional-setup/sidecar-injection/)方法が 2 つサポートされています。
ほとんどの場合は、アプリケーションを含む Kubernetes 名前空間を *istio-injection* ラベルでマークするのが最も簡単な方法です。

```console
kubectl label namespace <my-app-namespace> istio-injection=enabled
```

> [!NOTE]
> サービス メッシュによってデータはワイヤからリフトオフされるので、暗号化されたトラフィックをインターセプトすることはできません。 クラスターから出ないトラフィックの場合は、暗号化されていないプロトコル (HTTP など) を使用します。 暗号化する必要がある外部トラフィックの場合は、イングレス コントローラーで [SSL 終了を設定する](https://kubernetes.io/docs/concepts/services-networking/ingress/#tls)ことを検討します。

サービス メッシュの外部で実行されているアプリケーションには影響ありません。

### <a name="deploy-your-application"></a>アプリケーションをデプロイする

- アプリケーションを *my-app-namespace* 名前空間にデプロイします。 アプリケーションが既にデプロイされていて、上で説明した自動サイドカー インジェクション方法に従っている場合は、Istio がサイドカーを確実に挿入するように、ポッドを作成し直す必要があります。ローリング アップデートを開始するか、または個々のポッドを削除して再作成されるまで待ちます。
- アプリケーションが [Istio の要件](https://istio.io/docs/setup/kubernetes/prepare/requirements/)に準拠していることを確認します。

### <a name="deploy-zero-instrumentation-application-monitoring-for-kubernetes-hosted-apps"></a>Kubernetes でホストされたアプリに対するゼロ インストルメンテーション アプリケーション監視をデプロイする

1. ["*Application Insights アダプター*" のリリース](https://github.com/Microsoft/Application-Insights-Istio-Adapter/releases/)をダウンロードして抽出します。
2. リリース フォルダー内の */src/kubernetes/* に移動します。
3. *application-insights-istio-mixer-adapter-deployment.yaml* を編集します
    - *ISTIO_MIXER_PLUGIN_AI_INSTRUMENTATIONKEY* 環境変数の値を編集し、テレメトリを含むように、Azure portal での Application Insights リソースのインストルメンテーション キーを追加します。
    - 必要な場合は、*ISTIO_MIXER_PLUGIN_WATCHLIST_NAMESPACES* 環境変数の値を編集し、監視を有効にする名前空間のコンマ区切りのリストを追加します。 すべての名前空間を監視する場合は空白のままにします。
4. 以下を実行して、*src/kubernetes/* の下にある "*すべての*" YAML ファイルを適用します (まだ、 */src/kubernetes/* の内部にいる必要があります)。

   ```console
   kubectl apply -f .
   ```

### <a name="verify-deployment"></a>デプロイの確認

- Application Insights アダプターがデプロイされたことを確認します。

  ```console
  kubectl get pods -n istio-system -l "app=application-insights-istio-mixer-adapter"
  ```
> [!NOTE]
> 場合によっては、微調整が必要です。 個々のポッドのテレメトリを収集または除外するには、そのポッドで *appinsights/monitoring.enabled* ラベルを使用します。 これは、名前空間に基づくすべての設定より優先されます。 ポッドを含めるには *appinsights/monitoring.enabled* を *true* に設定し、除外するには *false* に設定します。

### <a name="view-application-insights-telemetry"></a>Application Insights のテレメトリを表示する

- アプリケーションに対してサンプルの要求を生成し、監視が正しく機能していることを確認します。
- 3 - 5 分以内に、Azure portal にテレメトリが表示され始めるはずです。 ポータルで Application Insights リソースの "*アプリケーション マップ*" セクションを確認してください。

## <a name="troubleshooting"></a>トラブルシューティング

以下では、テレメトリが Azure portal に予期したように表示されないときに使用するトラブルシューティングのフローを示します。

1. アプリケーションに負荷がかかっていて、プレーンな HTTP で要求が送受信されていることを確認します。 テレメトリはワイヤからリフトオフされるので、暗号化されたトラフィックはサポートされません。 受信または送信される要求がない場合、それに対応するテレメトリはありません。
2. *application-insights-istio-mixer-adapter-deployment.yaml* の *ISTIO_MIXER_PLUGIN_AI_INSTRUMENTATIONKEY* 環境変数で、正しいインストルメンテーション キーが指定されていることを確認します。 インストルメンテーション キーは、Azure portal の Application Insights リソースの *[概要]* タブで確認できます。
3. *application-insights-istio-mixer-adapter-deployment.yaml* の *ISTIO_MIXER_PLUGIN_WATCHLIST_NAMESPACES* 環境変数で、正しい Kubernetes 名前空間が指定されていることを確認します。 すべての名前空間を監視する場合は空白のままにします。
4. アプリケーションのポッドに Istio によってサイドカーが挿入されていることを確認します。 Istio のサイドカーがポッドごとに存在することを確認します。

   ```console
   kubectl describe pod -n <my-app-namespace> <my-app-pod-name>
   ```
   *istio-proxy* という名前のコンテナーがポッドで実行されていることを確認します。

5. Application Insights アダプターのトレースを表示します。

   ```console
   kubectl get pods -n istio-system -l "app=application-insights-istio-mixer-adapter"
   kubectl logs -n istio-system application-insights-istio-mixer-adapter-<fill in from previous command output>
   ```

   受信テレメトリの項目数は、1 分ごとに更新されます。 1 分ごとに増えていかない場合は、Istio によってアダプターにテレメトリが送信されていません。
   ログでエラーを探します。
6. *Kubernetes 用 Application Insight* アダプターがテレメトリをフィードされていないことが明らかになった場合は、Istio の Mixer ログを調べて、データがアダプターに送信されていない理由を確認します。

   ```console
   kubectl get pods -n istio-system -l "istio=mixer,app=telemetry"
   kubectl logs -n istio-system istio-telemetry-<fill in from previous command output> -c mixer
   ```
   エラーを探します (特に、*applicationinsightsadapter* アダプターとの通信に関連するもの)。

## <a name="faq"></a>FAQ

このプロジェクトの進行状況に関する最新情報については、[Istio Mixer 用 Application Insights アダプター プロジェクトの GitHub](https://github.com/Microsoft/Application-Insights-Istio-Adapter/blob/master/SETUP.md#faq) をご覧ください。

## <a name="uninstall"></a>アンインストール

製品をアンインストールするには、*src/kubernetes/* にある "*すべての*" YAML ファイルについて、以下を実行します。

```console
kubectl delete -f <filename.yaml>
```


## <a name="next-steps"></a>次の手順

Azure Monitor とコンテナーの連携方法について詳しくは、「[コンテナーに対する Azure Monitor の概要](../../azure-monitor/insights/container-insights-overview.md)」をご覧ください