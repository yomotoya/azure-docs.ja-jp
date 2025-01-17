---
title: インクルード ファイル
description: インクルード ファイル
services: notification-hubs
author: spelluru
ms.service: notification-hubs
ms.topic: include
ms.date: 03/30/2018
ms.author: spelluru
ms.custom: include file
ms.openlocfilehash: f0ff729084d194ff2e05e89eadc45782f775b1c5
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66156744"
---
このセクションでは、.NET コンソール アプリから、タグ付けされたテンプレート通知としてニュース速報を送信します。 

1. Visual Studio で、Visual C# の新しいコンソール アプリケーションを作成します。a. メニューで、**[ファイル]** > **[新規作成]** > **[プロジェクト]** を選択します。
    b. **[Visual C#]** を展開し、**[Windows デスクトップ]** を選択します。 
    c. テンプレートの一覧から **[コンソール アプリ (.NET Framework)]** を選択します。 
    d. アプリの**名前**を入力します。 
    e. アプリの**フォルダー**を選択します。
    f. **[OK]** を選択してプロジェクトを作成します。 
2. Visual Studio のメイン メニューで、**[ツール]** > **[NuGet Package Manager]** > **[パッケージ マネージャー コンソール]** の順に選択してから、コンソール ウィンドウで次の文字列を入力します。
   
    ```
    Install-Package Microsoft.Azure.NotificationHubs
    ```
   
3. **[Enter]** を選択します。  
    この操作によって、[Microsoft.Azure.Notification Hubs NuGet パッケージ]を使用して Azure Notification Hubs SDK に参照が追加されます。

4. Program.cs ファイルを開き、次の `using` ステートメントを追加します。
   
    ```csharp
    using Microsoft.Azure.NotificationHubs;
    ```

5. `Program` クラス内で、次のメソッドを追加するか、既にメソッドが指定されている場合は置き換えます。
   
    ```csharp
    private static async void SendTemplateNotificationAsync()
    {
        // Define the notification hub.
        NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");

        // Create an array of breaking news categories.
        var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};

        // Send the notification as a template notification. All template registrations that contain
        // "messageParam" and the proper tags will receive the notifications.
        // This includes APNS, GCM, WNS, and MPNS template registrations.

        Dictionary<string, string> templateParams = new Dictionary<string, string>();

        foreach (var category in categories)
        {
            templateParams["messageParam"] = "Breaking " + category + " News!";
            await hub.SendTemplateNotificationAsync(templateParams, category);
        }
    }
    ```   
   
    このコードでは、文字列の配列の 6 つのタグのそれぞれに対するテンプレート通知が送信されます。 タグを使用することで、デバイスは登録されているカテゴリに関する通知のみを確実に受信できます。

5. 上記のコードでは、プレースホルダー `<hub name>` と `<connection string with full access>` を、通知ハブの名前と通知ハブのダッシュボードから得た *DefaultFullSharedAccessSignature* の接続文字列に置き換えます。

6. **Main** メソッド内に、次の行を追加します。
   
    ```csharp
    SendTemplateNotificationAsync();
    Console.ReadLine();
    ```

7. コンソール アプリケーションをビルドします。

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[Get started with Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Notification Hubs REST interface]: https://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[Add push notifications for Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[How to use Notification Hubs from Java or PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[Microsoft.Azure.Notification Hubs NuGet パッケージ]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
