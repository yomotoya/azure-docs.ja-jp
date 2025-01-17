---
author: ecfan
ms.service: logic-apps
ms.topic: include
ms.date: 11/03/2016
ms.author: estfan
ms.openlocfilehash: 752c43604349a2361a8f5b26cd6d0bce7b516bc0
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66149766"
---
### <a name="prerequisites"></a>前提条件
* [MailChimp](https://www.MailChimp.com/) アカウント 

ロジック アプリで MailChimp アカウントを使用するには、MailChimp アカウントに接続するロジック アプリを承認する必要があります。 幸い、Azure Portal のロジック アプリ内から簡単に実行できます。 

次に、MailChimp アカウントに接続するロジック アプリを承認する手順を示します。

1. MailChimp への接続を作成するには、ロジック アプリ デザイナーのドロップダウン リストから **[Microsoft が管理している API を表示]** を選択し、検索ボックスに「*MailChimp*」と入力します。 使用するトリガーまたはアクションを選択します。  
   ![MailChimp 手順 1](./media/connectors-create-api-mailchimp/mailchimp-1.png)
2. これまでに MailChimp への接続を作成していない場合は、MailChimp の資格情報を指定するよう求められます。 この資格情報を使用して、接続するロジック アプリの承認と、MailChimp アカウントのデータへのアクセスが行われます。  
   ![MailChimp 手順 2](./media/connectors-create-api-mailchimp/mailchimp-2.png)
3. MailChimp のユーザー名とパスワードを入力して、ロジック アプリを承認します。  
   ![MailChimp 手順 3](./media/connectors-create-api-mailchimp/mailchimp-3.png)   
4. 接続が作成されたら、ロジック アプリで他の手順を自由に実行できるようになります。  
   ![MailChimp 手順 4](./media/connectors-create-api-mailchimp/mailchimp-4.png)

