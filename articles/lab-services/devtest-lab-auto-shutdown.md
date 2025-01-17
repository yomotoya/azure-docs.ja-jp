---
title: Azure DevTest Labs で自動シャットダウン ポリシーを管理する | Microsoft Docs
description: 使用されていないときに仮想マシンが自動的にシャットダウンされるように、ラボの自動シャットダウン ポリシーを設定する方法について説明します。
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2019
ms.author: spelluru
ms.openlocfilehash: 9adf8dd4a5a3c469ed130b29308a0d828aee40bf
ms.sourcegitcommit: 4c2b9bc9cc704652cc77f33a870c4ec2d0579451
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65874099"
---
# <a name="manage-autoshutdown-policies-for-a-lab-in-azure-devtest-labs"></a>Azure DevTest Labs でラボの自動シャットダウン ポリシーを管理する
Azure DevTest Labs では、各ラボのポリシー (設定) を管理することで、ラボのコストを制御し、無駄を最小限に抑えることができます。 この記事では、ラボ アカウントに対して自動シャットダウン ポリシーを構成する方法、およびラボ アカウントのラボに対して自動シャットダウンの設定を構成する方法を示します。 すべてのラボ ポリシーを設定する方法については、[Azure DevTest Labs でのラボ ポリシーの定義](devtest-lab-set-lab-policy.md)に関する記事をご覧ください。  

## <a name="set-auto-shutdown-policy-for-a-lab"></a>ラボに自動シャットダウン ポリシーを設定する
ラボ所有者は、ラボ内のすべての VM のシャットダウン スケジュールを構成できます。 これを行うことで、使用中ではない (アイドル状態の) マシンを実行するコストを節約できます。 すべてのラボの VM 上にあるシャットダウン ポリシーを一元的に適用できるだけでなく、ラボ ユーザーが個々のマシンのスケジュールを設定する手間もかかりません。 この機能を利用して、制御権なしから完全な制御権の提供まで、ラボ ユーザーにラボ スケジュール上でのポリシーを設定できます。 ラボ所有者は、次の手順を実行してこのポリシーを構成できます。

1. ラボの [ホーム] ページで、 **[構成とポリシー]** を選択します。
2. 左側のメニューの **[スケジュール]** セクションにある **[自動シャットダウン ポリシー]** を選択します。
3. いずれかのオプションを選択します。 以下のセクションでは、これらのオプションについてさらに詳しく説明します。設定されたポリシーは、ラボで新しく作成される VM に対してのみ適用され、既存の VM には適用されません。 

    ![自動シャットダウン ポリシーのオプション](./media/devtest-lab-set-lab-policy/auto-shutdown-policy-options.png)

## <a name="configure-auto-shutdown-settings"></a>自動シャットダウンの設定を構成する
自動シャットダウン ポリシーでは、このラボの VM をシャットダウンする時刻を指定できるので、ラボの無駄を最小限に抑えるのに役立ちます。

ラボのポリシーを表示 (および変更) するには、次の手順に従います。

1. [Azure Portal](https://portal.azure.com) にサインインします。
2. **[すべてのサービス]** を選択し、一覧の **[DevTest Labs]** を選択します。
3. ラボの一覧で目的のラボを選択します。   
4. **[Configuration and policies (構成とポリシー)]** を選択します。

    ![ポリシー設定ウィンドウ](./media/devtest-lab-set-lab-policy/policies-menu.png)
5. ラボの **[構成とポリシー]** ウィンドウで、 **[スケジュール]** の **[自動シャットダウン]** を選択します。
   
    ![自動シャットダウン](./media/devtest-lab-set-lab-policy/auto-shutdown.png)
6. このポリシーを有効にするには **[オン]** を選択し、無効にするには **[オフ]** を選択します。
7. このポリシーを有効にした場合は、現在のラボのすべての VM をシャットダウンする時刻 (およびタイム ゾーン) を指定します。
8. 指定した自動シャットダウン時刻の 15 分前に通知を送信するオプションに対して、 **[はい]** または **[いいえ]** を指定します。 **[はい]** を選択した場合は、通知が投稿または送信される Webhook URL のエンドポイントまたは電子メール アドレスを入力します。 ユーザーは通知を受信し、シャットダウンを遅らせるオプションが表示されます。 詳しくは、「[通知](#notifications)」セクションをご覧ください。 
9. **[保存]** を選択します。

    このポリシーを有効にすると、既定では現在のラボのすべての VM にこのポリシーが適用されます。 この設定を特定の VM から削除するには、その VM の管理ウィンドウを開いて、 **[自動シャットダウン]** の設定を変更します。

### <a name="user-sets-a-schedule-and-can-opt-out"></a>ユーザーがスケジュールを設定し、オプトアウトできる
ラボをこのポリシーに設定した場合、ラボ ユーザーがラボ スケジュールを上書きまたは無効にできます。 このオプションでは、VM の自動シャットダウン スケジュールの完全な制御権をラボ ユーザーに付与します。 ラボ ユーザーの VM 自動シャットダウン スケジュールのページには、変更は表示されません。

![自動シャットダウン ポリシーのオプション - 1](./media/devtest-lab-set-lab-policy/auto-shutdown-policy-option-1.png)

### <a name="user-sets-a-schedule-and-cannot-opt-out"></a>ユーザーがスケジュールを設定し、オプトアウトできない
ラボをこのポリシーに設定した場合、ラボ ユーザーがラボ スケジュールを上書きできます。 ただし、自動シャットダウン ポリシーは無効にできません。 このオプションでは、ラボ内のすべてのマシンが、自動シャットダウン スケジュール下にあることを保証します。 ラボ ユーザーは、VM の自動シャットダウン スケジュールを更新して、シャットダウンの通知を設定できます。

![自動シャットダウン ポリシーのオプション - 2](./media/devtest-lab-set-lab-policy/auto-shutdown-policy-option-2.png)

### <a name="user-has-no-control-over-the-schedule-set-by-lab-admin"></a>ユーザーはラボ管理者が設定したスケジュールを制御できない
ラボをこのポリシーに設定した場合、ラボ ユーザーがラボ スケジュールを上書きまたは無効にすることはできません。 このオプションでは、ラボ内のすべてのマシンのスケジュールに対する完全な制御権をラボ管理者に付与します。 ラボ ユーザーは、各自の VM の自動シャットダウンの通知を設定できるだけです。

![自動シャットダウン ポリシーのオプション - 3](./media/devtest-lab-set-lab-policy/auto-shutdown-policy-option-3.png)

## <a name="notifications"></a>通知
ラボ所有者が自動シャットダウンを設定すると、影響を受ける VM のユーザーに対し、自動シャットダウンがトリガーされる 15 分前に通知が送信されます。 このオプションにより、ラボ ユーザーはシャットダウンされる前に作業を保存する機会があります。 また、通知では、各 VM に対して次のアクションのためのリンクが提供されます。

- この時間の自動シャットダウンをスキップします
- VM での作業を続けられるように、自動シャットダウンを 1 時間または 2 時間だけ一時停止します。

通知は、構成されている Web hook エンドポイントを介して、または自動シャットダウンの設定でラボ所有者によって指定されたメール アドレスに、送信されます。 Webhook を使用すると、特定のイベントをサブスクライブする統合を構築または設定できます。 これらのイベントのいずれかがトリガーされると、DevTest Labs では、Webhook で構成されている URL に HTTP POST ペイロードが送信されます。 webhook の詳細については、「[webhook または API Azure Function を作成する](../azure-functions/functions-create-a-web-hook-or-api-function.md)」を参照してください。 

さまざまなアプリ (たとえば、Slack、Azure Logic Apps など) で広範にサポートされていて、独自の通知送信方法を実装できるため、Web hook を使うことをお勧めします。 この記事では、例として、Azure Logic Apps を使用してメールで自動シャットダウン通知を受け取る方法を示します。 最初に、ラボで自動シャットダウン通知を有効にする基本的な手順を簡単に見ておきましょう。   

## <a name="create-a-logic-app-that-receives-email-notifications"></a>メール通知を受信するロジック アプリを作成する
[Azure Logic Apps](../logic-apps/logic-apps-overview.md) で提供されている既製のコネクタを使うと、Office 365 や Twitter などの他のクライアントとサービスを簡単に統合できます。 メール通知用にロジック アプリをセットアップする概要レベルの手順は、4 つのフェーズに分類できます。 

- ロジック アプリを作成します。 
- 組み込みのテンプレートを構成します。
- メール クライアントと統合します
- Webhook の URL を取得します。

### <a name="create-a-logic-app"></a>ロジック アプリを作成します
最初に、次の手順を使って Azure サブスクリプションにロジック アプリを作成します。

1. 左側のメニューで **[+ リソースの作成]** を選択し、 **[統合]** 、 **[Logic App]** の順に選択します。 

    ![新しいロジック アプリのメニュー](./media/devtest-lab-auto-shutdown/new-logic-app.png)
2. **[Logic App - 作成]** ページで、次の手順のようにします。 
    1. ロジック アプリの**名前**を入力します。
    2. Azure **サブスクリプション**を選択します。
    3. 新しい**リソース グループ**を作成するか、既存のリソース グループを選択します。 
    4. ロジック アプリの**場所**を選択します。 

        ![新しいロジック アプリ -設定](./media/devtest-lab-auto-shutdown/new-logic-app-page.png)
3. **[通知]** で、通知の **[リソースに移動]** を選択します。 

    ![リソースに移動](./media/devtest-lab-auto-shutdown/go-to-resource.png)
4. **[Deployment Tools]\(展開ツール\)** カテゴリで、 **[ロジック アプリ デザイナー]** を選択します。

    ![HTTP 要求/応答を選択する](./media/devtest-lab-auto-shutdown/select-http-request-response-option.png)
5. **[HTTP 要求と応答]** ページで、 **[このテンプレートを使用]** を選択します。 

    ![[このテンプレートを使用] オプションを選択する](./media/devtest-lab-auto-shutdown/select-use-this-template.png)
6. 次の JSON を **[要求本文の JSON スキーマ]** セクションにコピーします。 

    ```json
    {
        "$schema": "http://json-schema.org/draft-04/schema#",
        "properties": {
            "delayUrl120": {
                "type": "string"
            },
            "delayUrl60": {
                "type": "string"
            },
            "eventType": {
                "type": "string"
            },
            "guid": {
                "type": "string"
            },
            "labName": {
                "type": "string"
            },
            "owner": {
                "type": "string"
            },
            "resourceGroupName": {
                "type": "string"
            },
            "skipUrl": {
                "type": "string"
            },
            "subscriptionId": {
                "type": "string"
            },
            "text": {
                "type": "string"
            },
            "vmName": {
                "type": "string"
            }
        },
        "required": [
            "skipUrl",
            "delayUrl60",
            "delayUrl120",
            "vmName",
            "guid",
            "owner",
            "eventType",
            "text",
            "subscriptionId",
            "resourceGroupName",
            "labName"
        ],
        "type": "object"
    }
    ```
    
    ![要求本文の JSON スキーマ](./media/devtest-lab-auto-shutdown/request-json.png)
7. デザイナーで **[+ 新しいステップ]** を選択し、次の手順のようにします。
    1. **[Office 365 Outlook - メールの送信]** を探します。 
    2. **[アクション]** から **[メールの送信]** を選択します。 
    
        ![メールの送信オプション](./media/devtest-lab-auto-shutdown/select-send-email.png)
    3. **[サインイン]** を選択して、メール アカウントにサインインします。 
    4. **[宛先]** フィールドを選択して、所有者を選択します。
    5. **[件名]** を選択して、メール通知の件名を入力します。 例: "ラボ labName のマシン vmName のシャットダウン"
    6. **[本文]** を選択し、メール通知の本文の内容を定義します。 例: "vmName は 15 分後にシャットダウンする予定です。 このシャットダウンをスキップするにはクリックしてください: URL。 シャットダウンを 1 時間遅延: delayUrl60。 シャットダウンを 2 時間遅延: delayUrl120。"

        ![要求本文の JSON スキーマ](./media/devtest-lab-auto-shutdown/email-options.png)
1. ツールバーの **[保存]** を選択します。 ここで、 **[HTTP POST の URL]** をコピーできます。 コピー ボタンを選択して、URL をクリップボードにコピーします。 

    ![WebHook URL](./media/devtest-lab-auto-shutdown/webhook-url.png)

## <a name="next-steps"></a>次の手順
すべてのポリシーの設定方法については、[Azure DevTest Labs でのラボ ポリシーの定義](devtest-lab-set-lab-policy.md)に関する記事をご覧ください。
