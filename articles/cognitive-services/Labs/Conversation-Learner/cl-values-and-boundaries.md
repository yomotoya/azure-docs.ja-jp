---
title: Conversation Learner の既定の構成 - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Conversation Learner の既定の構成について説明します。
services: cognitive-services
author: nitinme
manager: nolachar
ms.service: cognitive-services
ms.subservice: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: nitinme
ms.openlocfilehash: ebdc1e1c100329e95bd19359408cb138d233b1c2
ms.sourcegitcommit: 3d4121badd265e99d1177a7c78edfa55ed7a9626
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2019
ms.locfileid: "66385438"
---
# <a name="default-values-and-boundaries"></a>既定値と境界

このドキュメントでは、Conversation Learner の既定の構成と主なサービスの境界を説明します。

## <a name="default-configuration"></a>既定の構成

パラメーター | Default value
--- | --- 
セッションのタイムアウトの既定値 | 30 分

## <a name="boundaries"></a>境界

パラメーター | 制限
--- | --- 
オーサリング API、1 か月あたりの HTTP 呼び出しの最大数 | 5 M
オーサリング API、1 秒あたりの HTTP 呼び出しの最大数 | 25
セッション API、1 か月あたりの HTTP 呼び出しの最大数 | 500K
セッション API、1 秒あたりの HTTP 呼び出しの最大数 | 10
モデルあたりのカスタム (非プログラマティック) エンティティの最大数 | [LUIS の境界に関するドキュメント](https://docs.microsoft.com/azure/cognitive-services/luis/luis-boundaries)を参照してください。実際の数は、ドキュメントに記載の数よりも少なくなることがあります。
モデルあたりの作成済みのエンティティの最大数 | [LUIS の境界に関するドキュメント](https://docs.microsoft.com/azure/cognitive-services/luis/luis-boundaries)を参照してください。
モデルあたりのエンティティの最大数 (合計数) | 100
モデルあたりのアクションの最大数 | 32
モデルあたりのトレーニング会話の最大数 | 1,000
トレーニング ダイアログあたりのユーザーのターンの最大数 | 100
モデルあたりのログ会話の最大数 | 制限は設定されていません。ログ ダイアログは一定期間のみ保持され、その期間が経過すると破棄されます。  また、Conversation Learner UI では一度に 100 件のログ ダイアログが表示されます。 
ユーザーあたりのモデルの最大数 | 制限は設定されていません。
連続した非待機アクションの最大数 | 5 (*)

(*) 非待機アクションが 5 回連続して発生すると、非待機アクションがすべてマスクされ、Conversation Learner により利用可能な待機アクションが選択されます。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [Conversation Learner を使ってみる](./quickstart.md)
