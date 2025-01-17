---
title: Azure Cost Management を使用してクラウドへの投資を最適化する | Microsoft Docs
description: この記事は、クラウドへの投資から最大限の価値を得て、コストを削減し、コストのかかる部分を評価するのに役立ちます。
services: cost-management
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 05/21/2019
ms.topic: conceptual
ms.service: cost-management
manager: vitavor
ms.custom: seodec18
ms.openlocfilehash: 7c562e6f0a1358d16b9abef08a5e582e4ff84472
ms.sourcegitcommit: 13cba995d4538e099f7e670ddbe1d8b3a64a36fb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2019
ms.locfileid: "66002038"
---
# <a name="how-to-optimize-your-cloud-investment-with-azure-cost-management"></a>Azure Cost Management を使用してクラウドへの投資を最適化する方法

Azure Cost Management には、クラウドへの投資を最大化するために支出を計画、分析、削減するツールが用意されています。 このドキュメントでは、コスト管理のための系統的なアプローチを示し、組織のコストに関する課題に対処するために使用できるツールについて説明します。 Azure では、クラウド ソリューションを簡単に構築してデプロイすることができます。 しかし、組織のコストを最小限に抑えるために、それらのソリューションが最適化されていることが重要です。 このドキュメントで概説されている原則に従い、ツールを使用することは、組織が成功するための準備ができていることを確認するのに役立ちます。

## <a name="methodology"></a>手法

コスト管理は組織的な問題であり、クラウド リソースにコストをかける前に開始される継続的なプラクティスである必要があります。 コスト管理を適切に実装し、コストを最適化するには、組織で次のことが必要になります。

- 成功するための適切なツールを準備する
- コストに責任を持つ
- 支出を最適化するために適切なアクションを実行する

コストを適切に管理していることを確認するには、以下に示す 3 つの主要なグループを組織内に配置する必要があります。

- **財務/会計** - クラウド支出の予測に基づいて、組織全体で予算要求を承認する担当者。 対応する請求書の支払いを行い、さまざまなチームにコストを割り当て、アカウンタビリティを促します。
- **マネージャー** - 最適な支出結果を求めるためにクラウド支出について理解する必要がある、組織内におけるビジネス意思決定者。
- **アプリ チーム** - 組織のニーズに合わせてサービスを開発し、日常的にクラウド リソースを管理するエンジニア。 これらのチームには、定義された予算で最大の価値を提供する柔軟性が必要です。

### <a name="key-principles"></a>基本原則

以下に示す原則を使用して、クラウド コストを適切に管理するために組織を位置付けます。

#### <a name="planning"></a>計画

包括的な事前計画により、特定のビジネス要件に合わせてクラウドの使用を調整することができます。 次のことを確認してください。

- 解決するビジネス上の問題
- 自分のリソースからの予想される使用パターン

これらを確認することは、適切なオファリングを選択するのに役立ちます。 これにより、使用するインフラストラクチャと、Azure の効率を最大化するためのその使用方法が決まります。

#### <a name="visibility"></a>表示

適切に構造化されている場合、Cost Management は、担当者に自分が責任を負うべき Azure のコストや自分の支出について知らせるのに役立ちます。 Azure には、コストのかかる*部分* に関する分析情報を得るために設計されているサービスがあります。 これらのツールを利用します。 これらは、使用されていないリソースを見つけ、無駄をなくし、コスト削減の機会を最大化するのに役立ちます。

#### <a name="accountability"></a>アカウンタビリティ

担当者に所属チームの支出に対する責任を確実に持たせるために、組織におけるコストの帰属を明らかにします。 組織の Azure 支出を完全に理解するには、リソースを整理して、コスト属性についての分析情報を最大限に活用する必要があります。 適切に整理することは、コストの管理と削減、および組織における効率的な支出について担当者に責任を持たせるのに役立ちます。

#### <a name="optimization"></a>最適化

支出の削減を行います。 コストの可視性の計画および向上によって得られる結果に基づいて最大限に活用します。 インフラストラクチャ デプロイの変更と共に、購入およびライセンスの最適化を検討してください。これについては、このドキュメントの後半で詳しく説明します。

#### <a name="iteration"></a>反復

組織内のすべての人が、コスト管理のライフサイクルに関与する必要があります。 コストを最適化するには、継続的に関与する必要があります。 この反復的なプロセスについては厳密である必要があります。これは組織における責任あるクラウド ガバナンスの基本理念と見なしてください。

![表示、アカウンタビリティ、および最適化を示す基本原則の図](./media/cost-mgt-best-practices/principles.png)

## <a name="plan-with-cost-in-mind"></a>コストを考慮して計画する

クラウド リソースをデプロイする前に、次の項目を評価します。

- ニーズに最適な Azure プラン
- 使用を計画しているリソース
- どれくらいのコストがかかるのか

Azure には、評価プロセスに役立つツールが用意されています。 このツールを使用することで、ワークロードを有効にするのに必要な投資を把握できます。 その後、状況に応じて最適な構成を選択できます。

### <a name="azure-onboarding-options"></a>Azure のオンボード オプション

Cost Management 内でのエクスペリエンスを最大化する最初の手順は、最適な Azure プランを調べて決定することです。 今後 Azure をどのように使用する計画なのかを考えてみます。 また、課金モデルの構成方法を検討します。 決定する際に、次の質問を検討します。

- Azure をどれくらいの期間使用する計画なのか。 テストを行うのか、あるいは長期インフラストラクチャの構築を計画しているのか。
- Azure の支払いはどのように行うのか。 前払いで割引を受けるのか、月末に請求を受けるのか。

さまざまなオプションの詳細については、[Azure の購入方法](https://azure.microsoft.com/pricing/purchase-options/)に関するページを参照してください。 最も一般的な課金モデルをいくつか以下に示します。

#### <a name="freehttpsazuremicrosoftcomfree"></a>[Free](https://azure.microsoft.com/free/)

- 12 か月間の人気の無料サービス
- $200 のクレジットで 30 日間サービス群をじっくり検討
- 25 個以上のサービスがいつでも無料

#### <a name="pay-as-you-gohttpsazuremicrosoftcomoffersms-azr-0003p"></a>[従量課金制](https://azure.microsoft.com/offers/ms-azr-0003p)

- 最低支払金額や付帯条件なし
- 有利な価格設定
- 使用した分だけお支払い
- いつでもキャンセル可能

#### <a name="enterprise-agreementhttpsazuremicrosoftcompricingenterprise-agreement"></a>[マイクロソフトエンタープライズ契約](https://azure.microsoft.com/pricing/enterprise-agreement/)

- 前払いの年額コミットメントに関するオプション
- Azure の割引価格を利用

## <a name="estimate-the-cost-of-your-solution"></a>ソリューションのコストを見積もる

インフラストラクチャをデプロイする前に、ソリューションのコストを評価します。 この評価は、事前に組織でのワークロードに関する予算を作成するのに役立ちます。 その後、予算の時系列比較を使用して、初期見積もりの有効性についてベンチマークを実行することができます。 また、デプロイしたソリューションの実際のコストと比較することができます。

### <a name="azure-pricing-calculator"></a>Azure 料金計算ツール

Azure 料金計算ツールを使用することで、さまざまな Azure サービスを組み合わせてコストの見積もりを表示できます。 Azure でさまざまな方法を使用して、ソリューションを実装することができます。各方法が支出全体に影響する可能性があります。 クラウド デプロイのすべてのインフラストラクチャ ニーズについて、早い段階で検討することは、ツールを最も効果的に使用するのに役立ちます。 Azure での推定支出を確実に見積もるのに役立つ場合があります。

詳細については、[Azure の料金計算ツール](https://azure.microsoft.com/pricing/calculator)に関するページをご覧ください。

### <a name="azure-migrate"></a>Azure Migrate

Azure Migrate は、オンプレミス データセンターでの組織の現在のワークロードを評価するサービスです。 Azure の代替ソリューションに求められることについての分析情報が得られます。 最初に、Migrate ではオンプレミス コンピューターを分析して、移行が可能かどうかを判断します。 次に、パフォーマンスを最大化するために Azure での VM のサイズ変更を推奨します。 最後に、Azure ベースのソリューションに関するコスト見積もりも作成します。

詳細については、[Azure Migrate](../migrate/migrate-overview.md) に関するページを参照してください。

## <a name="analyze-and-manage-your-costs"></a>コストを分析して管理する

時間の経過と共に組織のコストがどのように変化するかを常に把握します。 次の手法を使用して、支出を正しく理解して管理します。

### <a name="organize-and-tag-your-resources"></a>リソースを整理してタグを付ける

コストを考慮してリソースを整理します。 サブスクリプションとリソース グループを作成する際に、関連コストの担当チームについて考えます。 組織を考慮してレポートしていることを確認します。 サブスクリプションとリソース グループでは、組織全体の支出を整理して属性付けるために適切なバケットが提供されます。 タグはコストを属性付ける優れた方法です。 タグをフィルターとして使用できます。 データを分析してコストを調べる際に、このタグを使用してグループ化できます。 Enterprise Agreement のお客様は、部門を作成し、そこにサブスクリプションを配置することもできます。 Azure でのコストベースの整理は、組織内の担当者にチームの支出削減に対して責任を持たせるのに役立ちます。

### <a name="use-cost-analysis"></a>コスト分析を使用する

コスト分析では、標準的なリソース プロパティを使用するコストのスライスとダイスにより、組織のコストを詳細に分析できます。 分析に関するガイドとして、次の一般的な質問を検討してください。 定期的にこれらの質問に答えることは、常により多くの情報を入手し、よりコスト重視の意思決定を行うのに役立ちます。

- **今月の推定コスト** – 今月はこれまでにどれくらいコストが発生したか。 予算内に収まるか。
- **異常の調査** – コストが通常の使用の妥当な範囲内に収まることを定期的に確認します。 どのような傾向があるか。 外れ値はあるか。
- **請求書の調整** - 最新の請求額が前の月より多くなっているか。 前月比の支出傾向はどのように変化したか。
- **内部チャージバック** - 自分に対する課金額と、所属組織でのその金額の分類方法を把握しているか。

詳細については、[コスト分析](quick-acm-cost-analysis.md)に関するページを参照してください。

### <a name="export-billing-data-on-a-schedule"></a>スケジュールに従って課金データをエクスポートする

ダッシュボードや財務システムなどの外部システムに課金データをインポートする必要はありますか。 Azure Storage への自動エクスポートを設定して、毎月手動でファイルをダウンロードしなくて済むようにします。 その後は、他のシステムによる自動統合を簡単に設定して、課金データを継続的に同期できます。

課金データのエクスポートの詳細については、[データのエクスポートと管理](tutorial-export-acm-data.md)に関するページを参照してください。

### <a name="create-budgets"></a>予算を作成する

支出パターンを特定して分析した後、自分自身と所属チームに関する制限の設定を開始することが重要です。 Azure Budgets では、多くのしきい値とアラートを使用してコストまたは使用量ベースの予算を設定することができます。 予算バーンダウンの進行状況を表示し、必要に応じて変更するために定期的に作成する予算を必ず確認してください。 Azure Budgets では、指定された予算しきい値に達したときの自動トリガーを構成することもできます。 たとえば、VM をシャットダウンするようにサービスを構成することができます。 または、予算トリガーに応じて、インフラストラクチャを別の価格レベルに移動することができます。

詳細については、[Azure Budgets](tutorial-acm-create-budgets.md) に関するページを参照してください。

予算ベースの自動化の詳細については、[予算ベースの自動化](../billing/billing-cost-management-budget-scenario.md)に関するページを参照してください。

## <a name="act-to-optimize"></a>最適化を行う
次の方法を使用して支出を最適化します。

### <a name="cut-out-waste"></a>無駄をなくす

Azure でインフラストラクチャをデプロイしたら、それが使用されていることを確認することが重要です。 すぐに節約を始める最も簡単な方法は、使用されていないリソースを確認して削除することです。 そこで、リソースが可能な限り効率的に使用されているかどうかを判断する必要があります。

#### <a name="azure-advisor"></a>Azure Advisor

Azure Advisor は、特に、CPU またはネットワーク使用量の観点から使用率が低い仮想マシンを識別するサービスです。 そこで、マシンの実行を継続するために推定コストに基づいてマシンをシャットダウンするかサイズ変更するかを決定できます。 Advisor では、予約インスタンス購入に関する推奨事項も提供されます。 推奨事項は、仮想マシンの過去 30 日間の使用量に基づいています。 推奨事項に従って作業を行うことは、支出の削減に役立ちます。

詳細については、[Azure Advisor](../advisor/advisor-overview.md) に関するページを参照してください。

### <a name="size-your-vms-properly"></a>VM のサイズを適切に変更する

VM のサイズ変更は、Azure の全体的なコストに大きく影響します。 Azure で必要な VM の数は、オンプレミス データセンターに現在デプロイしているのと同じではない可能性があります。 必ず、実行を計画しているワークロードに適したサイズを選んでください。

詳細については、「[Azure IaaS: proper sizing and cost](https://azure.microsoft.com/resources/videos/azurecon-2015-azure-iaas-proper-sizing-and-cost/)」 (Azure IaaS: 適切なサイズ変更とコスト) を参照してください。

### <a name="use-purchase-discounts"></a>購買割引を使用する

Azure には、組織でコストの削減のために利用できる数多くの割引が用意されています。

#### <a name="azure-reservations"></a>Azure の予約

Azure の予約では、仮想マシンまたは SQL Database の計算キャパシティについて、1 年単位または 3 年単位で前払いすることができます。 前払いすると、使用するリソースの割り引きを受けることができます。 Azure の予約では、仮想マシンまたは SQL Database のコンピューティング コストを大幅に削減できます。割引率は、従量課金制の料金に対し、1 年間または 3 年間の前払い契約で最大 72% となります。 予約は課金割引を提供するもので、仮想マシンまたは SQL Database の実行時の状態には影響しません。

詳細については、「[What are Azure Reservations?](../billing/billing-save-compute-costs-reservations.md)」 (Azure の予約とは) を参照してください。

#### <a name="use-azure-hybrid-benefit"></a>Azure ハイブリッド特典を利用する

オンプレミス デプロイで Windows Server または SQL Server のライセンスが既にある場合は、Azure ハイブリッド特典プログラムを使用して Azure でのコストを削減できます。 Windows Server を利用した場合、各ライセンスに OS のコストが含まれ (最大 2 台の仮想マシンが対象)、お客様が支払うのは基本的なコンピューティング コストのみとなります。 既存の SQL Server ライセンスを使用すれば、仮想コアベースの SQL Database オプションで最大 55% の節約となります。 オプションには、Azure 仮想マシン内の SQL Server と、SQL Server Integration Services が含まれます。

詳細については、「[Azure Hybrid Benefit 節約額計算ツール](https://azure.microsoft.com/pricing/hybrid-benefit/)」を参照してください。

### <a name="other-resources"></a>その他のリソース

Azure には、料金割引のために Azure の余剰容量を活用するサービスを構築できるようにするサービスもあります。 詳細については、「[Use low priority VMs with Batch](../batch/batch-low-pri-vms.md)」 (優先順位の低い VM で Batch を使用する) を参照してください。

## <a name="next-steps"></a>次の手順
- Cost Management を初めてご利用の場合は、「[Azure Cost Management とは](overview-cost-mgt.md)」をお読みになり、Azure の支出を監視して制御するのにどのように役立つかと、リソースの使用の最適化について確認してください。
