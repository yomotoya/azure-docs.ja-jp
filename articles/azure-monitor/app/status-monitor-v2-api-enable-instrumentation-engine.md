---
title: Azure Status Monitor v2 API リファレンス:インストルメンテーション エンジンを有効にする |Microsoft Docs
description: Status Monitor v2 API リファレンス Enable-InstrumentationEngine。 Web サイトを再デプロイせずに Web サイトのパフォーマンスを監視します。 オンプレミス、VM、または Azure でホストされた ASP.NET Web アプリが対象です。
services: application-insights
documentationcenter: .net
author: MS-TimothyMothra
manager: alexklim
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.topic: conceptual
ms.date: 04/23/2019
ms.author: tilee
ms.openlocfilehash: e993378634262de25449975431c0a9e3145ca9fb
ms.sourcegitcommit: 25a60179840b30706429c397991157f27de9e886
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66255241"
---
# <a name="status-monitor-v2-api-enable-instrumentationengine-v021-alpha"></a>Status Monitor v2 API:Enable-InstrumentationEngine (v0.2.1-alpha)

このドキュメントでは、[Az.ApplicationMonitor PowerShell モジュール](https://www.powershellgallery.com/packages/Az.ApplicationMonitor/)のメンバーとして付属しているコマンドレットについて説明します。

> [!IMPORTANT]
> 現在、Status Monitor v2 はパブリック プレビュー段階にあります。
> このプレビュー バージョンはサービス レベル アグリーメントなしで提供されています。運用環境のワークロードに使用することはお勧めできません。 特定の機能はサポート対象ではなく、機能が制限されることがあります。
> 詳しくは、[Microsoft Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)に関するページをご覧ください。

## <a name="description"></a>説明

このコマンドレットは、いくつかのレジストリ キーを設定することで、インストルメンテーション エンジンを有効にします。
これらの変更を有効にするために IIS を再起動してください。

インストルメンテーション エンジンは、.NET SDK によって収集されたデータを補完できます。
管理されたプロセスの実行を説明するイベントおよびメッセージが収集されます。 依存関係の結果コード、HTTP 動詞、および SQL コマンド テキストが含まれますが、これに限定されません。 

インストルメンテーション エンジンは、次の場合に有効にします。
- Enable コマンドレットを使用して監視を既に有効にしているが、InstrumentationEngine は有効にしていなかった場合。
- .NET SDK を使用してアプリケーションを手動でインストルメント化しており、追加のテレメトリを収集したい場合。

> [!IMPORTANT] 
> このコマンドレットでは、管理者権限の PowerShell セッションが必要です。

> [!NOTE] 
> このコマンドレットでは、ライセンスおよびプライバシーに関する声明を確認して同意する必要があります。

> [!NOTE] 
> インストルメンテーション エンジンはオーバーヘッドを追加します。このエンジンは、既定ではオフになっています。

## <a name="examples"></a>例

```powershell
PS C:\> Enable-InstrumentationEngine
```

## <a name="parameters"></a>parameters 

### <a name="-acceptlicense"></a>-AcceptLicense
**省略可能。** ヘッドレス インストールでライセンスおよびプライバシーに関する声明に同意する場合は、このスイッチを使用します。

### <a name="-verbose"></a>-Verbose
**共通パラメーター**です。 詳細なログを出力する場合はこのスイッチを使用します。

## <a name="output"></a>Output


#### <a name="example-output-from-successfully-enabling-the-instrumentation-engine"></a>インストルメンテーション エンジンが正常に有効化された場合の出力例

```
Configuring IIS Environment for instrumentation engine...
Configuring registry for instrumentation engine...
```

## <a name="next-steps"></a>次の手順

  テレメトリの表示:
 - パフォーマンスと使用状況を監視するための[メトリックを探索](../../azure-monitor/app/metrics-explorer.md)します
- 問題を診断するために[イベントとログを検索](../../azure-monitor/app/diagnostic-search.md)します
- より高度なクエリのために [Analytics](../../azure-monitor/app/analytics.md) を使用します
- [ダッシュボードを作成](../../azure-monitor/app/overview-dashboard.md)します
 
 テレメトリの追加:
 - サイトがライブの状態であることを確認するために [Web テストを作成](monitor-web-app-availability.md)します。
- Web ページ コードからの例外を参照してトレースの呼び出しを挿入するために、[Web クライアント テレメトリ](../../azure-monitor/app/javascript.md)を追加します。
- トレースとログの呼び出しを挿入できるように、[Application Insights SDK をコードに追加](../../azure-monitor/app/asp-net.md)します
 
 Status Monitor v2 の活用:
 - ガイドを使用して、Status Monitor v2 を[トラブルシューティング](status-monitor-v2-troubleshoot.md)します。
 - 設定が正しく記録されたことを確認するために[構成を取得](status-monitor-v2-api-get-config.md)します。
 - 監視を検査するために[状態を取得](status-monitor-v2-api-get-status.md)します。
