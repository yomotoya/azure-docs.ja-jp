---
title: コンサルティング サービス オファーのオファーの設定を定義する | Azure Marketplace
description: Azure Marketplace の Cloud パートナー ポータルで Azure または Dynamics 365 コンサルティング サービス オファーのオファーの設定を定義します。
services: Azure, Marketplace, Cloud Partner Portal,
author: qianw211
ms.service: marketplace
ms.topic: conceptual
ms.date: 04/23/2019
ms.author: pabutler
ms.openlocfilehash: 601ad62bddd1373742b0cab5a388a55cfd52f4bc
ms.sourcegitcommit: c53a800d6c2e5baad800c1247dce94bdbf2ad324
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2019
ms.locfileid: "64942786"
---
# <a name="offer-settings-tab"></a>[プランの設定] タブ

**[新しいプラン]** 画面では、まずプラン ID を作成します。 オファー ID は、次の 3 つのパーツで構成されます。**プラン ID**、**パブリッシャー ID**、**名前**です。 次の各セクションで、それぞれの要素について説明します。

![新しいコンサルティング サービス オファーの作成 - [プランの設定] タブ](media/consultingoffer-settings-tab.png)


### <a name="offer-id"></a>[オファー ID]*

この ID は、最初にオファーを送信するときに作成する一意の名前です。 小文字の英数字、ハイフン、アンダースコアのみで構成する必要があります。 **オファー ID** は URL に表示され、検索エンジンの結果に影響します。 たとえば、*yourcompanyname_exampleservice* です。

この例を見るとわかるように、**オファー ID** がパブリッシャー ID に追加されて、一意識別子が作成されます。 この一意の識別子は予約可能な固定リンクとして公開され、検索エンジンによってインデックス付けされます。

>[!Note]
>オファーが運用開始になると、その識別子を更新することはできません。


### <a name="publisher-id"></a>[発行元 ID]*

この識別子は、ご自分のアカウントに関連しています。 組織アカウントでサインインすると、ドロップダウン メニューに**パブリッシャー ID** が表示されます。


### <a name="name"></a>[名前]*

この文字列が、AppSource または Azure Marketplace 上で、オファー名として表示されます。 **[名前]** ボックスは 50 文字に制限されています。 オファー名に期間とオファーの種類を付加するために、レビュー担当者がタイトルを編集しなければならない場合があります。

次の例は、オファー名がどのように組み立てられるかを示しています。 

![新しいコンサルティング サービス オファーを作成する](media/cppsampleconsultingoffer.png)

オファー名は、次の 4 つのパーツで構成されます。

-   **期間:** エディターの **[Storefront Details]\(ネットショップの詳細\)** タブで定義します。 期間は、時間、日、週で表現できます。
-   **サービスの種類:** エディターの **[Storefront Details]\(ネットショップの詳細\)** タブで定義します。 サービスの種類は、`Assessment`、`Briefing`、`Implementation`、`Proof of concept`、`Workshop` です。
-   **前置詞:** レビュー担当者によって挿入されます。
-   **[名前]:** **[プランの設定]** ページで定義します。

>[!Note]
>**[名前]** ボックスは 50 文字に制限されています。 オファー名に期間とオファーの種類を付加するために、レビュー担当者がタイトルを編集しなければならない場合があります。

以下の一覧で適切なオファー名を示します。

-   プロフェッショナル サービスの要点: 1 時間のブリーフィング
-   クラウド移行プラットフォーム: 1 時間のブリーフィング
-   PowerApps および Microsoft Flow: 1 日のワークショップ
-   Azure Machine Learning サービス: 3 週間の PoC
-   ブリック アンド クリック小売りソリューション: 1 時間のブリーフィング
-   データ持ち込み: 1 週間のワークショップ
-   クラウド分析:3 日間のワークショップ
-   Power BI トレーニング: 3 日間のワークショップ
-   セールス管理ソリューション: 1 週間の実装
-   CRM クイック スタート: 1 日のワークショップ
-   Dynamics 365 for Sales: 2 日間の評価

**[プランの設定]** タブの入力が完了したら、送信内容を保存します。 オファー名はエディターの上に表示されるようになり、 **[すべてのプラン]** にも表示されます。

## <a name="next-steps"></a>次の手順

これで、[ネットショップの詳細を入力し、Azure Marketplace と AppSource のどちらで発行するかを決定](./cpp-consulting-service-storefront-details.md)できるようになりました。
