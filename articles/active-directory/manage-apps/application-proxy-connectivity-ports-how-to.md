---
title: アプリケーション プロキシ アプリケーションに必要なファイアウォール ポートを開く方法 | Microsoft Docs
description: Azure AD アプリケーション プロキシを正しく動作させるために開くポートを確認します
services: active-directory
documentationcenter: ''
author: msmimart
manager: CelesteDG
ms.assetid: ''
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: mimart
ms.reviewer: asteen
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3e69f2e5049ca290a17c058c9d18dc7c6ec91f49
ms.sourcegitcommit: 36c50860e75d86f0d0e2be9e3213ffa9a06f4150
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2019
ms.locfileid: "65783557"
---
# <a name="how-to-open-the-firewall-ports-required-for-an-application-proxy-application"></a>アプリケーション プロキシ アプリケーションに必要なファイアウォール ポートを開く方法

必要なポートと各ポートの機能を網羅したリストについては、[アプリケーション プロキシに関するドキュメント](application-proxy-add-on-premises-application.md)の前提条件のセクションを参照してください。 アプリケーション プロキシでは送信ポートのみを使用する点に注意してください。

オンプレミスのネットワークから[コネクタ ポート テスト ツール](https://aadap-portcheck.connectorporttest.msappproxy.net/)を開き、必要なすべてのポートが開いているかどうかを確認することもできます。 緑色のチェックマークが多いほど、回復性が高いことになります。 

## <a name="app-proxy-regions"></a>アプリ プロキシのリージョン

お客様にとってどのリージョンに緑色のチェックマークが必要かという点については、今後お伝えできるように準備を進めています。 当面は、すべてのリージョンにチェックマークが付いていることを確認してください。 お住まいのリージョンとは無関係に、米国中部も必要なリージョンとなります。

ツールで正しい結果が得られるようにするには、以下の点に注意してください。

-   コネクタをインストールしたサーバーからブラウザーでツールを開く。

-   コネクタに適用されるプロキシまたはファイアウォールが、このページにも適用されるようにする。 これを設定するため、Internet Explorer で、**[設定]** -&gt; **[インターネット オプション]** -&gt; **[接続]** -&gt; **[LAN の設定]** の順に移動します。 このページに、[LAN にプロキシ サーバーを使用する] フィールドがあります。 このボックスをオンにし、[アドレス] フィールドにプロキシ アドレスを入力します。

## <a name="next-steps"></a>次の手順
[Azure AD アプリケーション プロキシ コネクタについて](application-proxy-connectors.md)
