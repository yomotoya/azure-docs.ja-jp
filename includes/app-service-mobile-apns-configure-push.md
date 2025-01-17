---
author: conceptdev
ms.author: crdun
ms.service: app-service-mobile
ms.topic: include
ms.date: 08/23/2018
ms.openlocfilehash: 852a3b00e8513f9ce68c5aae54c974505d0c9af6
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66140154"
---
1. お使いの Mac で、 **Keychain Access**を起動します。 左側のナビゲーション バーで、**[分類]** の **[自分の証明書]** を開きます。 前のセクションでダウンロードした SSL 証明書を見つけ、その内容を開示します。 (秘密キーを選択せずに) 証明書のみを選択します。 次に、[それをエクスポート](https://support.apple.com/kb/PH20122?locale=en_US)します。
2. [Azure Portal](https://portal.azure.com/) で **[すべて参照]** > **[App Services]** の順に選択します。 次に、Mobile Apps バックエンドを選択します。 
3. **[設定]** で **[App Service Push]\(App Service プッシュ\)** を選択します。 次に、通知ハブの名前を選択します。 
4. **[Apple Push Notification Service]** > **[証明書のアップロード]** の順に選択します。 (前の手順のクライアント SSL 証明書が実稼働環境用かサンドボックス用かに応じて) 適切な**モード**を選択して、.p12 ファイルをアップロードします。 すべての変更を保存します。

これで、iOS のプッシュ通知と連携するようにサービスが構成されました。

[1]: ./media/app-service-mobile-apns-configure-push/mobile-push-notification-hub.png
