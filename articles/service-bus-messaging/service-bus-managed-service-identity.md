---
title: Azure Service Bus での Azure リソースのマネージド ID (プレビュー) | Microsoft Docs
description: Azure Service Bus で Azure リソースのマネージド ID を使用する
services: service-bus-messaging
documentationcenter: na
author: axisc
manager: timlt
editor: spelluru
ms.assetid: ''
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/01/2018
ms.author: aschhab
ms.openlocfilehash: 8477ff8c8ff0bc1629ff4cdc61f7c28c6eed778c
ms.sourcegitcommit: 59fd8dc19fab17e846db5b9e262a25e1530e96f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65978795"
---
# <a name="managed-identities-for-azure-resources-with-service-bus"></a>Azure Service Bus での Azure リソースのマネージド ID 

[Azure リソースのマネージド ID](../active-directory/managed-identities-azure-resources/overview.md) は、デプロイに関連付けられ、その下でアプリケーション コードが実行されるセキュリティ保護された ID を作成できる Azure 間機能です。 この ID は、アプリケーションに必要な特定の Azure リソースにアクセスするためのカスタム アクセス許可を付与するアクセス制御ロールに関連付けることができます。

マネージド ID では、Azure プラットフォームがこのランタイム ID を管理します。 ID 自体やアクセスする必要のあるリソース用に、アクセス キーをアプリケーション コードや構成に保存して保護する必要はありません。 Azure リソース サポートに対してマネージド エンティティが有効にされている Azure App Service アプリケーション内または仮想マシンで実行されている Service Bus クライアント アプリは、SAS ルールと SAS キーや、その他のアクセス トークンを処理する必要はありません。 クライアント アプリに必要なのは、Service Bus メッセージング名前空間のエンドポイント アドレスだけです。 アプリが接続すると、Service Bus はこの記事で後述する例に示す操作で、マネージド エンティティのコンテキストをクライアントにバインドします。 マネージド ID に関連付けられると、Service Bus クライアントは承認済みのすべての操作を実行できます。 マネージド エンティティを Service Bus のロールに関連付けることによって承認が付与されます。 

## <a name="service-bus-roles-and-permissions"></a>Service Bus のロールとアクセス許可

マネージド ID は、Service Bus 名前空間の "Service Bus データ所有者" ロールに追加できます。 これにより、名前空間のすべてのエンティティに対する (管理およびデータの操作の) フル コントロールが ID に付与されます。

>[!IMPORTANT]
> 以前は、マネージド ID を **"所有者"** または **"共同作成者"** ロールに追加することをサポートしていました。
>
> しかし、 **"所有者"** と **"共同作成者"** ロールのデータ アクセス特権は受け入れられなくなります。 **"所有者"** または **"共同作成者"** ロールを使用していた場合、 それらは **"Service Bus データ所有者"** ロールを利用するように変更する必要があります。

新しい組み込みのロールを使用するには、次の手順を実行してください。

1. [Azure portal](https://portal.azure.com) に移動します
2. 現在 "所有者" または "共同作成者" ロールを設定している Service Bus 名前空間に移動します。
3. 左側のウィンドウのメニューで [アクセス制御 (IAM)] をクリックします。
4. 次のように進めて、新しいロールの割り当てを追加します

    ![](./media/service-bus-role-based-access-control/ServiceBus_RBAC_SBDataOwner.png)

5. [保存] をクリックして、新しいロールの割り当てを保存します。

## <a name="use-service-bus-with-managed-identities-for-azure-resources"></a>Azure リソースのマネージド ID による Service Bus の使用

以下のセクションでは、マネージド ID で実行されるサンプル アプリケーションを作成してデプロイするために必要な手順、その ID に Service Bus メッセージング名前空間へのアクセス権を付与する方法、アプリケーションがその ID を使用して Service Bus エンティティとやり取りするしくみについて説明します。

この概要では、[Azure App Service](https://azure.microsoft.com/services/app-service/) でホストされる Web アプリケーションについて説明します。 VM でホストされるアプリケーションに必要な手順もほぼ同じです。

### <a name="create-an-app-service-web-application"></a>App Service Webアプリケーションを作成する

まず、App Service ASP.NET アプリケーションを作成します。 Azure でこれを行う方法がわからない場合は、[こちらのチュートリアル](../app-service/app-service-web-get-started-dotnet-framework.md)に従ってください。 ただし、チュートリアルで示す MVC アプリケーションを作成する代わりに、Web フォーム アプリケーションを作成してください。

### <a name="set-up-the-managed-identity"></a>マネージド ID を設定する

アプリケーションを作成したら、Azure Portal で新しく作成された Web アプリに移動し (チュートリアルにも示されています)、 **[管理対象サービス ID]** ページに移動してこの機能を有効にします。 

![](./media/service-bus-managed-service-identity/msi1.png)

機能を有効にすると、Azure Active Directory に新しいサービス ID が作成され、App Service ホストに構成されます。

### <a name="create-a-new-service-bus-messaging-namespace"></a>新しい Service Bus メッセージング名前空間を作成する

次に、[Service Bus メッセージング名前空間を作成します](service-bus-create-namespace-portal.md)。 

ポータルで名前空間の **[アクセス制御 (IAM)]** ページに移動し、 **[ロールの割り当ての追加]** をクリックして、マネージド ID を**所有者**ロールに追加します。 そのためには、 **[アクセス許可の追加]** パネルの **[選択]** フィールドで Web アプリケーションの名前を検索し、エントリをクリックします。 その後、 **[保存]** をクリックします。

これで、Web アプリケーションのマネージド ID は、Service Bus 名前空間と以前に作成したキューにアクセスできるようになりました。 

### <a name="run-the-app"></a>アプリの実行

次に、作成した ASP.NET アプリケーションの既定のページを変更します。 [こちらの GitHub リポジトリ](https://github.com/Azure-Samples/app-service-msi-servicebus-dotnet)の Web アプリケーション コードを使用します。  

Default.aspx ページはランディング ページです。 コードは Default.aspx.cs ファイルにあります。 いくつかの入力フィールドと、Service Bus に接続してメッセージを送受信するための **send** ボタンおよび **receive** ボタンを備えた最小限の Web アプリケーションが作成されます。

[MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) オブジェクトを初期化する方法に注意してください。 共有アクセス トークン (SAS) トークン プロバイダーを使用するのではなく、コードで `TokenProvider.CreateManagedServiceIdentityTokenProvider(ServiceAudience.ServiceBusAudience)` を呼び出してマネージド ID のトークン プロバイダーを作成します。 そのため、保持および使用するシークレットはありません。 マネージド ID コンテキストから Service Bus へのフローと承認ハンドシェイクは、トークン プロバイダーによって自動的に処理されます。 これは SAS を使用するよりも単純なモデルです。

これらの変更を行ったら、アプリケーションを発行して実行します。 適切な発行データを簡単に取得するには、Visual Studio で発行プロファイルをダウンロードしてインポートします。

![](./media/service-bus-managed-service-identity/msi3.png)
 
メッセージを送受信するには、名前空間の名前と作成したエンティティの名前を入力します。 次に、 **[send]** または **[receive]** をクリックします。


> [!NOTE]
> - マネージド ID は、Azure 環境内の App Services、Azure VM、およびスケール セットでのみ機能します。 .NET アプリケーションの場合は、Service Bus NuGet パッケージで使用される Microsoft.Azure.Services.AppAuthentication ライブラリがこのプロトコルの抽象化を提供し、ローカル開発エクスペリエンスをサポートします。 このライブラリを使うと、Visual Studio、Azure CLI 2.0、または Active Directory 統合認証のユーザー アカウントを使って、開発用マシン上でローカルにコードをテストすることもできます。 このライブラリでのローカル開発オプションの詳細については、「[Service-to-service authentication to Azure Key Vault using .NET](../key-vault/service-to-service-authentication.md)」 (.NET を使用した Azure Key Vault に対するサービス間認証) を参照してください。  
> 
> - 現在、マネージド ID は、App Service デプロイ スロットでは機能しません。

## <a name="next-steps"></a>次の手順

Service Bus メッセージングの詳細については、次のトピックをご覧ください。

* [Service Bus のキュー、トピック、サブスクリプション](service-bus-queues-topics-subscriptions.md)
* [Service Bus キューの使用](service-bus-dotnet-get-started-with-queues.md)
* [Service Bus のトピックとサブスクリプションの使用方法](service-bus-dotnet-how-to-use-topics-subscriptions.md)
