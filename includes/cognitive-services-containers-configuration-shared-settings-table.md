---
author: diberry
ms.author: diberry
ms.service: cognitive-services
ms.topic: include
ms.date: 05/15/2019
ms.openlocfilehash: c4abc5fa89b48b6fc55637e9ff3b259387d0d410
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66116741"
---
このコンテナーには、次の構成設定があります。

|必須|Setting|目的|
|--|--|--|
|はい|[ApiKey](#apikey-configuration-setting)|課金情報の追跡に使用されます。|
|いいえ |[ApplicationInsights](#applicationinsights-setting)|[Azure Application Insights](https://docs.microsoft.com/azure/application-insights) テレメトリ サポートをお客様のコンテナーに追加できます。|
|はい|[Billing](#billing-configuration-setting)|Azure 上のサービス リソースのエンドポイント URI を指定します。|
|はい|[Eula](#eula-setting)| コンテナーのライセンスに同意していることを示します。|
|いいえ |[Fluentd](#fluentd-settings)|ログと (必要に応じて) メトリック データを Fluentd サーバーに書き込みます。|
|いいえ |Http Proxy|送信要求を行うために、HTTP プロキシを構成します。|
|いいえ |[Logging](#logging-settings)|ASP.NET Core のログ サポートをお客様のコンテナーに提供します。 |
|いいえ |[Mounts](#mount-settings)|ホスト コンピューターからコンテナーに、またコンテナーからホスト コンピューターにデータを読み取ったり書き込んだりします。|
