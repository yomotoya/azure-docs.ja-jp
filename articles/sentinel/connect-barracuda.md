---
title: Azure Sentinel Preview に Barracuda データを接続する | Microsoft Docs
description: Azure Sentinel に Barracuda データを接続する方法について説明します。
services: sentinel
documentationcenter: na
author: rkarlin
manager: rkarlin
editor: ''
ms.assetid: 3b33b4aa-7286-4d79-b461-8e1812edc2e1
ms.service: sentinel
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2019
ms.author: rkarlin
ms.openlocfilehash: dd45be69ec29fdcd00710b7366348846f325b151
ms.sourcegitcommit: d73c46af1465c7fd879b5a97ddc45c38ec3f5c0d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2019
ms.locfileid: "65921986"
---
# <a name="connect-your-barracuda-appliance"></a>Barracuda アプライアンスの接続 

> [!IMPORTANT]
> 現在、Azure Sentinel はパブリック プレビュー段階にあります。
> このプレビュー バージョンはサービス レベル アグリーメントなしで提供されています。運用環境のワークロードに使用することはお勧めできません。 特定の機能はサポート対象ではなく、機能が制限されることがあります。 詳しくは、[Microsoft Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)に関するページをご覧ください。

Barracuda Web Application Firewall (WAF) コネクタを使用すると、Azure Sentinel に Barracuda のログを簡単に接続でき、ダッシュ ボードの表示、カスタム アラートの作成、および調査の改善も行うことができます。 これにより、組織のネットワークに関するより詳しい分析情報が得られ、セキュリティ運用機能が向上します。 Azure Sentinel は、**Barracuda** と Microsoft Monitoring Agent の間のネイティブ統合を活用して、シームレスな統合を提供します。 


> [!NOTE]
> データは、Azure Sentinel を実行しているワークスペースの地理的な場所に格納されます。

## <a name="configure-and-connect-barracuda-waf"></a>Barracuda WAF の構成と接続
Barracuda Web アプリケーション ファイアウォールは、Microsoft Monitoring Agent 経由でログを Azure Sentinel に直接統合してエクスポートできます。
1. [Barracuda WAF 構成フロー](https://campus.barracuda.com/product/webapplicationfirewall/doc/73696965/configure-the-barracuda-web-application-firewall-to-integrate-with-the-oms-server-and-export-logs/)に移動し、手順に従って次のパラメーターを使用して接続を設定します。
    - **ワークスペース ID**: Azure Sentinel Barracuda コネクタのページから、ワークスペース ID の値をコピーします。
    - **主キー**: Azure Sentinel Barracuda コネクタのページから、主キーの値をコピーします。
2. Azure Sentinel ポータルで Azure Sentinel をデプロイしたワークスペースに移動し、行の末尾にある省略記号 (...) を選択して、 **[詳細設定]** を選択します。 
1. **[データ]** 、 **[Syslog]** の順に選択します。
1. Barracuda に設定したファシリティが存在することを確認して重大度を設定し、 **[保存]** をクリックします。
6. Log Analytics で Barracuda イベントに関連するスキーマを使用するために、**CommonSecurityLog** を検索します。


## <a name="validate-connectivity"></a>接続の検証

ログが Log Analytics に表示され始めるまで、20 分以上かかる場合があります。 



## <a name="next-steps"></a>次の手順
このドキュメントでは、Barracuda アプライアンスを Azure Sentinel に接続する方法について学びました。 Azure Sentinel の詳細については、次の記事をご覧ください。
- [データと潜在的な脅威を可視化](quickstart-get-visibility.md)する方法についての説明。
- [Azure Sentinel を使用した脅威の検出](tutorial-detect-threats.md)の概要。

