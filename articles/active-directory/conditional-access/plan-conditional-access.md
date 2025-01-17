---
title: Azure Active Directory の条件付きアクセス ポリシーを計画する | Microsoft Docs
description: この記事では、Azure Active Directory の条件付きアクセス ポリシーを計画する方法について説明します。
services: active-directory
author: MicrosoftGuyJFlo
manager: daveba
tags: azuread
ms.service: active-directory
ms.subservice: conditional-access
ms.topic: conceptual
ms.workload: identity
ms.date: 01/25/2019
ms.author: joflore
ms.reviewer: martincoetzer
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e277f31dcf2627959b88d58f325fb4dad024a00
ms.sourcegitcommit: 13cba995d4538e099f7e670ddbe1d8b3a64a36fb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2019
ms.locfileid: "66001185"
---
# <a name="how-to-plan-your-conditional-access-deployment-in-azure-active-directory"></a>方法:Azure Active Directory の条件付きアクセスの展開を計画する

組織内のアプリやリソースに必要なアクセス戦略を確実に達成するには、条件付きアクセスの展開を計画することが重要です。 選択した条件下でユーザーに対してアクセスの許可またはブロックを行うために必要なさまざまなポリシーを設計するには、展開の計画段階にほとんどの時間を費やす必要があります。 このドキュメントでは、安全で効果的な条件付きアクセス ポリシーを実装するために必要な手順について説明します。 始める前に、[条件付きアクセス](overview.md)のしくみとその使用するタイミングを理解しておく必要があります。


## <a name="what-you-should-know"></a>知っておくべきこと

条件付きアクセスは、スタンドアロンの機能ではなく、組織のアプリやリソースへのアクセスを制御できるようにするフレームワークと考えてください。 そのため、一部の条件付きアクセス設定では、追加機能を構成する必要があります。 たとえば、特定の[サインイン リスク レベル](../identity-protection/howto-sign-in-risk-policy.md#what-is-the-sign-in-risk-policy)に応答するポリシーを構成できます。 ただし、サインイン リスク レベルに基づくポリシーでは、[Azure Active Directory の ID 保護](../identity-protection/overview.md)を有効にする必要があります。

追加機能が必要な場合、関連するライセンスの取得が必要になることもあります。 たとえば、条件付きアクセスは Azure AD Premium P1 の機能ですが、ID 保護には Azure AD Premium P2 ライセンスが必要です。

条件付きアクセス ポリシーには、ベースラインと標準の 2 種類があります。 [ベースライン ポリシー](baseline-protection.md)は、事前に定義された条件付きアクセス ポリシーです。 これらのポリシーの目標は、少なくともベースライン レベルのセキュリティを有効にすることです。 ベースライン ポリシー。 ベースライン ポリシーは Azure AD のすべてのエディションで使用できます。限られたカスタマイズ オプションのみを利用できます。 さらに柔軟性が必要なシナリオの場合は、ベースライン ポリシーを無効にして、カスタム標準ポリシーで要件を実装します。

標準の条件付きアクセス ポリシーでは、すべての設定をカスタマイズして、ビジネス要件に合わせてポリシーを調整することができます。 標準ポリシーには Azure AD Premium P1 ライセンスが必要です。




## <a name="draft-policies"></a>ドラフト ポリシー

Azure Active Directory の条件付きアクセスを使用すると、クラウド アプリの保護を新たなレベルに引き上げることができます。 この新しいレベルでは、クラウド アプリケーションにアクセスする方法は、静的アクセス構成ではなく動的ポリシー評価に基づいています。 条件付きアクセス ポリシーでは、アクセス条件 (**これが発生した場合**) への応答 (**これを実行する**) を定義します。

![理由と応答](./media/plan-conditional-access/10.png)

この計画モデルを使用して実装するすべての条件付きアクセス ポリシーを定義します。 この計画の演習では以下を行います。

- 各ポリシーに対する応答と条件の概要をまとめます。
- 組織に合わせて文書化した条件付きアクセス ポリシー カタログを完成させます。 

このカタログを使用して、ポリシーの実装が組織のビジネス要件を反映しているかどうかを評価できます。 

組織の条件付きアクセス ポリシーを作成するには、次のサンプル テンプレートを使用します。

|"*これ*" が発生した場合:|"*これ*" を実行する:|
|-|-|
|以下のアクセスの試行が行われた場合:<br>- クラウド アプリに対する *<br>- ユーザーおよびグループによる*<br>以下を使用する:<br>- 条件 1 (たとえば、会社のネットワーク外)<br>- 条件 2 (たとえば、デバイスのプラットフォーム)|アプリケーションへのアクセスをブロックする|
|以下のアクセスの試行が行われた場合:<br>- クラウド アプリに対する *<br>- ユーザーおよびグループによる*<br>以下を使用する:<br>- 条件 1 (たとえば、会社のネットワーク外)<br>- 条件 2 (たとえば、デバイスのプラットフォーム)|次の条件でアクセスを付与する (AND):<br>- 要件 1 (たとえば、MFA)<br>- 要件 2 (たとえば、デバイス コンプライアンス)|
|以下のアクセスの試行が行われた場合:<br>- クラウド アプリに対する *<br>- ユーザーおよびグループによる*<br>以下を使用する:<br>- 条件 1 (たとえば、会社のネットワーク外)<br>- 条件 2 (たとえば、デバイスのプラットフォーム)|次の条件でアクセスを付与する (OR):<br>- 要件 1 (たとえば、MFA)<br>- 要件 2 (たとえば、デバイス コンプライアンス)|

少なくとも「**これが発生した場合**」では、クラウド アプリへのアクセスを試行する (**何を**) プリンシパル (**だれが**) を定義します。 必要に応じて、アクセス試行の実行**方法**も含めることができます。 条件付きアクセスでは、だれが、何を、そして方法を定義する要素は条件と呼ばれます。 詳細については、「[Azure Active Directory 条件付きアクセスの条件の概要](conditions.md)」を参照してください。 

「**これを実行する**」では、アクセス条件に対するポリシーの応答を定義します。 応答では、多要素認証 (MFA) などの追加要件を使用してアクセスをブロックまたは許可します。 詳細な概要については、「[Azure Active Directory 条件付きアクセスによるアクセス制御の概要](controls.md)」を参照してください。  
 

条件とアクセスの制御の組み合わせによって、条件付きアクセス ポリシーを表現します。

![理由と応答](./media/plan-conditional-access/51.png)


詳細については、「[ポリシーを機能させるために必要なこと](best-practices.md#whats-required-to-make-a-policy-work)」を参照してください。

この時点で、ポリシーの名前付け基準を決めることをお勧めします。 名前付け基準があると、Azure 管理ポータルでポリシーを開かなくても、ポリシーを見つけてその用途を理解することができます。 次を示す名前をポリシーに付けるようにします。

- シーケンス番号
- 適用先のクラウド アプリ
- 応答
- 適用されるユーザー
- いつ適用するか (該当する場合)
 
![名前付け基準](./media/plan-conditional-access/11.png)

わかりやすい名前は条件付きアクセスの実装の概要を保持するに役立ちますが、シーケンス番号は会話でポリシーを参照する必要がある場合に便利です。 たとえば、同僚の管理者と電話で話す場合、問題を解決するためにポリシー EM063 を開いてほしいと頼むことができます。



たとえば、次の名前は、Dynamics CRP アプリを使用して外部ネットワーク上のユーザーのマーケティングのために、このポリシーに MFA が必須であることを示しています。

`CA01 - Dynamics CRP: Require MFA For marketing When on external networks`


また、アクティブ ポリシーに加えて、[機能停止/緊急状況のシナリオでセカンダリの回復性があるアクセスの制御](../authentication/concept-resilient-controls.md)として機能する停止時のポリシーも実装することをお勧めします。 コンティンジェンシー ポリシーの命名規則には、さらにいくつかの項目を含める必要があります。 

- 他のポリシーから名前が目立つようにするため、先頭に `ENABLE IN EMERGENCY`。

- 適用する必要のある中断の名前。

- 管理者がポリシーを有効にする順序を理解できるようにするための、順序シーケンス番号。 


たとえば、次の名前は、このポリシーが MFA の中断時に有効にする必要がある 4 つのポリシーのうちの最初のポリシーであることを示します。

`EM01 - ENABLE IN EMERGENCY, MFA Disruption[1/4] - Exchange SharePoint: Require hybrid Azure AD join For VIP users`







## <a name="plan-policies"></a>ポリシーの計画

条件付きアクセス ポリシー ソリューションを計画するときは、次の結果を達成するためにポリシーを作成する必要があるかどうかを評価します。 


### <a name="block-access"></a>アクセスのブロック

次の理由のため、アクセスをブロックするオプションは強力です。

- ユーザーの他のどの割り当てよりも優先される

- 組織全体がテナントにサインオンできなくなるようにする機能がある
 
すべてのユーザーのアクセスをブロックする場合は、少なくとも 1 人のユーザー (通常は緊急アクセス アカウント) をポリシーから除外する必要があります。 詳細については、[ユーザーとグループの選択](block-legacy-authentication.md#select-users-and-cloud-apps)に関する記事を参照してください。  
    

### <a name="require-mfa"></a>Require MFA (MFA が必須)

ユーザーのサインイン エクスペリエンスを簡易化するために、ユーザー名とパスワードを使用してクラウド アプリにサインインできるようにすることができます。 ただし、通常、より強力な形式のアカウント検証を必須にすることが推奨されるシナリオが少なくとも数個あります。 条件付きアクセス ポリシーを使用すると、MFA の要件を特定のシナリオに限定できます。 

MFA を必要とする一般的なユースケースはアクセスです。

- [管理者による](howto-baseline-protect-administrators.md)
- [特定のアプリに対する](app-based-mfa.md) 
- [信頼していないネットワークの場所から](untrusted-networks.md)。


### <a name="respond-to-potentially-compromised-accounts"></a>侵害された可能性があるアカウントへの応答

条件付きアクセス ポリシーを使用すると、侵害された可能性がある ID からのサインインに対する自動応答を実装できます。 アカウントが侵害された可能性は、リスク レベルの形で表現されます。 ID 保護によって計算される 2 つのリスク レベルがあります。サインイン リスクとユーザー リスクです。 サインイン リスクへの応答を実装するには、2 つの選択肢があります。

- 条件付きアクセス ポリシー内の[サインイン リスク条件](conditions.md#sign-in-risk)
- ID 保護内の[サインイン リスク ポリシー](../identity-protection/howto-sign-in-risk-policy.md) 

条件としてサインイン リスクに対処する方法は、カスタマイズ オプションが多いため、推奨されます。

ID 保護では、ユーザー リスク レベルは[ユーザー リスク ポリシー](../identity-protection/howto-user-risk-policy.md)としてのみ使用できます。 

詳細については、「[Azure Active Directory Identity Protection とは](../identity-protection/overview.md)」を参照してください。 


### <a name="require-managed-devices"></a>マネージド デバイスを必須にする

クラウド リソースへのアクセスでサポートされるデバイスの急増は、ユーザーの生産性の向上に役立ちます。 その一方で、環境内の特定のリソースは、保護レベルが不明なデバイスからアクセスされるのは望ましくない可能性があります。 影響を受けるリソースについては、ユーザーがマネージド デバイスを使用してのみアクセスできることを要求する必要があります。 詳細については、[条件付きアクセスを使用してクラウド アプリへのアクセスにマネージド デバイスを要求する方法](require-managed-devices.md)に関するページを参照してください。 

### <a name="require-approved-client-apps"></a>承認済みクライアント アプリを必須にする

自分のデバイスを持ち込む (BYOD) シナリオのために必要な最初の決定事項の 1 つは、デバイス全体を管理するか、そのデータのみを管理する必要があるかということです。 従業員は個人的な作業と業務上の作業のどちらにもモバイル デバイスを使用します。 そこで、従業員の生産性を確保しながら、データの損失を防止する必要があります。 Azure Active Directory (Azure AD) の条件付きアクセスを使うと、クラウド アプリへのアクセスを、承認されたクライアント アプリだけに制限して、会社のデータを保護することができます。 詳細については、[条件付きアクセスを使用してクラウド アプリへのアクセスに承認されたクライアント アプリを要求する方法](app-based-conditional-access.md)に関するページを参照してください。


### <a name="block-legacy-authentication"></a>レガシ認証をブロックする

Azure AD では、レガシ認証を含め、最も広く使用されている認証および承認のプロトコルを複数サポートしています。 レガシ認証を使用しているアプリからはテナントのリソースにアクセスできないようにするには、どうしたらいいでしょうか。 お勧めは、単純に条件付きアクセス ポリシーを使用して、それらのアプリをブロックすることです。 必要に応じて、特定のユーザーと特定のネットワークの場所だけに、レガシ認証に基づいたアプリの使用を許可します。 詳細については、[条件付きアクセスを使用して Azure AD へのレガシ認証をブロックする方法](block-legacy-authentication.md)に関するページを参照してください。


## <a name="test-your-policy"></a>ポリシーのテスト

ポリシーを運用環境にロールアウトする前に、予想どおりに動作することを確認します。

1. テスト ユーザーの作成

2. テスト計画の作成

3. ポリシーの構成

4. シミュレートされたサインインを評価する

5. ポリシーのテスト

6. クリーンアップ



### <a name="create-test-users"></a>テスト ユーザーの作成

ポリシーをテストするには、環境内のユーザーと似た一連のユーザーを作成します。 テスト ユーザーを作成すると、実際のユーザーに影響が及び、アプリやリソースへのアクセスが中断される前に、ポリシーが予想どおりに機能することを確認できます。 


この目的のためにテスト テナントを持っている組織もあります。 ただし、ポリシーの結果を完全にテストすることができるすべての条件とアプリをテスト テナントで再現することは困難な場合があります。 

### <a name="create-a-test-plan"></a>テスト計画の作成

テスト計画は、予想される結果と実際の結果を比較するために重要です。 何かをテストする前には、常に予想を用意しておきます。 次の表は、テスト ケースの例の概要です。 実際の CA ポリシーを構成する方法に基づいて、このシナリオと予想される結果を調整します。

|ポリシー |シナリオ |予測される結果 | 結果 |
|---|---|---|---|
|[社外ネットワークからの利用は MFA を要求する](https://docs.microsoft.com/azure/active-directory/conditional-access/untrusted-networks)|承認済みユーザーが信頼できる場所または社内にいるときに "*アプリ*" にサインインする|ユーザーに MFA は求められません| |
|[社外ネットワークからの利用は MFA を要求する](https://docs.microsoft.com/azure/active-directory/conditional-access/untrusted-networks)|承認済みユーザーが信頼できる場所または社内にいないときに "*アプリ*" にサインインする|ユーザーには MFA が求められ、正常にサインインできます| |
|[(管理者に) MFA を要求する](https://docs.microsoft.com/azure/active-directory/conditional-access/baseline-protection#require-mfa-for-admins)|全体管理者が "*アプリ*" にサインインする|管理者に MFA が求められます| |
|[リスクの高いサインイン](https://docs.microsoft.com/azure/active-directory/identity-protection/howto-sign-in-risk-policy)|ユーザーが [Tor ブラウザー](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection-playbook)を使用して "*アプリ*" にサインインする|管理者に MFA が求められます| |
|[デバイス管理](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)|承認済みユーザーが承認済みデバイスからサインインしようとする|アクセスが許可されます| |
|[デバイス管理](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)|承認済みユーザーが承認されていないデバイスからサインインしようとする|アクセスはブロックされます| |
|[危険なユーザーのパスワード変更](https://docs.microsoft.com/azure/active-directory/identity-protection/howto-user-risk-policy)|承認済みユーザーが侵害された資格情報を使用してサインインしようとする (高リスクのサインイン)|ユーザーはパスワードを変更するよう求められるか、ポリシーに基づいてアクセスがブロックされます| |


### <a name="configure-the-policy"></a>ポリシーの構成

条件付きアクセス ポリシーの管理は手動の作業です。 Azure portal では、条件付きアクセス ポリシーを 1 か所 ([条件付きアクセス] ページ) で管理できます。 条件付きアクセス ページのエントリ ポイントの 1 つは、**Active Directory** ナビゲーション ウィンドウの **[セキュリティ]** セクションです。 

![条件付きアクセス](media/plan-conditional-access/03.png)


条件付きアクセス ポリシーの作成方法の詳細については、「[Azure Active Directory の条件付きアクセスを使用して特定のアプリケーションに対して MFA を必要にする](app-based-mfa.md)」を参照してください。 このクイック スタートは、次のために役立ちます。

- ユーザー インターフェイスに慣れる。
- 条件付きアクセスがどのように機能するかについて第一印象を得る。 


### <a name="evaluate-a-simulated-sign-in"></a>シミュレートされたサインインを評価する

条件付きアクセス ポリシーを構成したら、期待どおりに動作しているかどうかを確認してみましょう。 最初の手順として、条件付きアクセスの [What If ポリシー ツール](what-if-tool.md)を使用して、テスト ユーザーのサインインをシミュレートします。 シミュレーションでは、サインインがポリシーに与える影響を推定し、シミュレーション レポートが生成されます。

>[!NOTE]
> シミュレートされた実行で、条件付きアクセス ポリシーが与える影響の印象がわかりますが、実際のテスト実行に代わるものではありません。


### <a name="test-your-policy"></a>ポリシーのテスト

テスト計画に従ってテスト ケースを実行します。 この手順では、テスト ユーザーが各ポリシーのエンド ツー エンド テストを実行し、各ポリシーが正しく動作することを確認します。 上記で作成したシナリオを使用して各テストを実行します。

ポリシーの除外条件を確実にテストすることが重要です。 たとえば、MFA を必要とするポリシーからユーザーまたはグループを除外することができます。 そのため、他のポリシーの組み合わせでは除外されたユーザーに MFA が必要な場合があるので、除外されたユーザーに MFA を求めるプロンプトが表示されるかどうかをテストする必要があります。


### <a name="cleanup"></a>クリーンアップ

クリーンアップ手続きは次の手順で構成されます。

1. ポリシーを無効にする。

2. 割り当てられたユーザーとグループを削除する。

3. テスト ユーザーを削除する。  




## <a name="move-to-production"></a>運用環境に移行する

新しいポリシーを環境で使用する準備が整ったら、段階的に展開します。

- エンド ユーザーに内部的な変更通知を提供します。

- 少数のユーザーから始めて、ポリシーが想定どおりに動作することを確認します。

- より多くのユーザーが含まれるようにポリシーを拡げます。このとき、すべての管理者は引き続き除外します。 管理者を除外することで、変更が必要になった場合に、だれかがポリシーにアクセスできるようにします。

- 必要な場合にのみ、すべてのユーザーにポリシーを適用します。

ベスト プラクティスとして、次のようなユーザー アカウントを少なくとも 1 つ作成します。

- ポリシー管理専用である

- すべてのポリシーから除外されている

 



## <a name="rollback-steps"></a>手順をロールバックする

新しく実装したポリシーをロールバックする必要がある場合は、次のオプションの 1 つ以上を使用してロールバックします。

1. **ポリシーを無効にする** - ポリシーを無効にすると、ユーザーがサインインしようとしたときに適用されなくなります。 いつでも戻って使用したいポリシーを有効にすることができます。

    ![ポリシーの無効化](media/plan-conditional-access/07.png)

2. **ポリシーからユーザー/グループを除外する** - ユーザーがアプリにアクセスできない場合、ユーザーをポリシーから除外することができます

    ![ユーザーの除外](media/plan-conditional-access/08.png)

    >[!NOTE]
    > このオプションは、ユーザーを信頼できる状態でのみ、控えめに使用してください。 ユーザーはできるだけ早くポリシーまたはグループに追加し直す必要があります。

3. **ポリシーを削除する** - ポリシーが不要になった場合は削除します。

## <a name="next-steps"></a>次の手順

使用できる情報の概要については、「[Azure AD の条件付きアクセスのドキュメント](index.yml)」を参照してください。
