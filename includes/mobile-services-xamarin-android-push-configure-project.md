---
author: conceptdev
ms.author: crdun
ms.service: app-service-mobile
ms.topic: include
ms.date: 08/23/2018
ms.openlocfilehash: 69dc0e1c14bc88cdbf0aa48700f95058ba759cc0
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66140233"
---
1. ソリューション ビュー (または Visual Studio の**ソリューション エクスプローラー**) で、**[Components]** フォルダーを右クリックして **[コンポーネントをさらに取得する...]** をクリックし、**[Google Cloud Messaging Client]** コンポーネントを検索して、それをプロジェクトに追加します。
2. ToDoActivity.cs プロジェクト ファイルを開き、次の using ステートメントをクラスに追加します。

    ```csharp
    using Gcm.Client;
    ```

3. **ToDoActivity** クラスに、次の新しいメソッドを追加します。 

    ```csharp
    // Create a new instance field for this activity.
    static ToDoActivity instance = new ToDoActivity();

    // Return the current activity instance.
    public static ToDoActivity CurrentActivity
    {
        get
        {
            return instance;
        }
    }
    // Return the Mobile Services client.
    public MobileServiceClient CurrentClient
    {
        get
        {
            return client;
        }
    }
    ```

    これにより、プッシュ ハンドラー サービス プロセスからモバイル クライアント インスタンスにアクセスできるようになります。
4. **MobileServiceClient** が作成された後で、次のコードを **OnCreate** メソッドに追加します。

    ```csharp
    // Set the current instance of TodoActivity.
    instance = this;

    // Make sure the GCM client is set up correctly.
    GcmClient.CheckDevice(this);
    GcmClient.CheckManifest(this);

    // Register the app for push notifications.
    GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);
    ```

これで、 **ToDoActivity** は、プッシュ通知を追加するための準備が整いました。
