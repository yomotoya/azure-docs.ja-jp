---
title: Azure Key Vault に影響を与える Azure サービスの中断が発生した場合の対処方法 - Azure Key Vault | Microsoft Docs
description: Azure Key Vault に影響を与える Azure サービスの中断が発生した場合の対処方法について説明します。
services: key-vault
author: barclayn
manager: barbkess
editor: ''
ms.service: key-vault
ms.topic: conceptual
ms.date: 05/24/2019
ms.author: barclayn
ms.openlocfilehash: dba1fe91a635f467f4a3aeeaa048897065822869
ms.sourcegitcommit: 509e1583c3a3dde34c8090d2149d255cb92fe991
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2019
ms.locfileid: "66236635"
---
# <a name="azure-key-vault-availability-and-redundancy"></a>Azure Key Vault の可用性と冗長性

Azure Key Vault には複数層の冗長性が備わっています。そのため、サービスの個々のコンポーネントで障害が発生した場合でも、アプリケーションでは引き続きキーとシークレットを使用することができます。

Key Vault のコンテンツは、リージョン内と、同じ地域内の 150 マイル (約 241 km) 以上離れたセカンダリ リージョンにレプリケートされます。 これにより、キーとシークレットの高い持続性が保たれます。 特定のリージョン ペアの詳細については、「[Azure のペアになっているリージョン](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)」ドキュメントを参照してください。

Key Vault サービス内の個々のコンポーネントで障害が発生した場合、リージョン内の代替コンポーネントが要求を処理し、機能が低下しないようにします。 この処理をトリガーするために、何かの措置を講じる必要はありません。 ユーザーからは見えないところで自動的に実行されます。

Azure リージョン全体が使用できない場合がまれにありますが、そのような場合でもそのリージョン内の Azure Key Vault に対する要求は自動的にセカンダリ リージョンにルーティング ("*フェールオーバー*") されます。 プライマリ リージョンが再び使用できるようになったときに、要求は再びプライマリ リージョンにルーティング ("*フェールバック*") されます。 この動作も自動的に行われるため、ユーザーによる操作は必要ありません。

この高可用性の設計のおかげで、Azure Key Vault では、メンテナンス アクティビティのためのダウンタイムは必要ありません。

その場合の注意事項をいくつか次に示します。

* リージョン フェールオーバーの場合、サービスのフェールオーバーには数分かかることがあります。 その間に行われた要求は、フェールオーバーが完了するまで失敗する可能性があります。
* フェールオーバーが完了すると、Key Vault は読み取り専用モードになります。 このモードでサポートされる要求は次のとおりです。
  * Key Vault のリスト
  * Key Vault のプロパティの取得
  * シークレットのリスト
  * シークレットの取得
  * キーのリスト
  * キー (のプロパティ) の取得
  * 暗号化
  * 復号化
  * ラップ
  * ラップ解除
  * 確認
  * 署名
  * バックアップ
* フェールオーバーがフェールバックされると、すべての種類の要求 (つまり、読み取り "*および*" 書き込み要求) が可能になります。

