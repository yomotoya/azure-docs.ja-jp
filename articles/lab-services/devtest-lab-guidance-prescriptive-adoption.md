---
title: 企業に Azure DevTest Labs を導入する
description: この記事では、企業内で Azure DevTest Labs を使用するための手引きとなるガイダンスを提供します。
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2019
ms.author: spelluru
ms.reviewer: christianreddington,anthdela,juselph
ms.openlocfilehash: 32e828f420d41d7a67e4f41ac8a4a0698711ce2f
ms.sourcegitcommit: 2028fc790f1d265dc96cf12d1ee9f1437955ad87
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2019
ms.locfileid: "64916404"
---
# <a name="devtest-labs-in-the-enterprise"></a>企業内での DevTest Labs
俊敏性、柔軟性、経済性を含む[メリット](/azure/architecture/cloud-adoption/business-strategy/cloud-migration-business-case)を理由に、企業はクラウドを迅速に採用しています。 最初の手順は、多くの場合、開発とテストのワークロードです。 Azure DevTest Labs は、企業にとってメリットとなる[機能](devtest-lab-concepts.md)を提供し、[主要な開発/テスト シナリオ](devtest-lab-guidance-get-started.md)をサポートします。

ワークロードをクラウドに移行する企業にとっての一般的な懸念事項は、次のとおりです。

- [開発/テスト用リソースのセキュリティ保護](devtest-lab-guidance-governance-policy-compliance.md)
- [コストの管理と理解](devtest-lab-guidance-governance-cost-ownership.md)
- エンタープライズ セキュリティとコンプライアンスを損なわない開発者のセルフ サービスの有効化
- 追加のシナリオに対応するための DevTest Labs の自動化および拡張
- [数千ものリソースへの DevTest Labs ベース ソリューションのスケーリング](devtest-lab-guidance-scale.md)
- [DevTest Labs の大規模なデプロイ](devtest-lab-guidance-orchestrate-implementation.md)
- [概念実証の使用の開始](devtest-lab-guidance-orchestrate-implementation.md)

## <a name="intended-audience"></a>対象ユーザー
このドキュメントは、企業でデプロイの設定と確認および操作の監視を担当する IT プランナー、アーキテクト、およびマネージャーを対象にしています。 これらの記事では、全体的なプロセスと推奨される設計原則を強調します。 目標は、安全で安定した開発/テスト環境を促進することです。これによって最終的には、組織内で Azure DevTest Labs の採用が推進されます。

## <a name="enterprise-customers"></a>企業顧客

DevTest Labs の現行の企業顧客の多くは、自社の組織での開発およびワークロードのテストに DevTest Labs をうまく使用しています。 [詳細情報](https://azure.microsoft.com/case-studies/?term=DevTest+labs)。

## <a name="next-steps"></a>次の手順
- [エンタープライズ向け参照アーキテクチャ](devtest-lab-reference-architecture.md)
