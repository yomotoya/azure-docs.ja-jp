---
author: ecfan
ms.service: logic-apps
ms.topic: include
ms.date: 11/03/2016
ms.author: estfan
ms.openlocfilehash: 7cfce34cb2d6002dba5ec570bf859ec47e894c65
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66149751"
---
#### <a name="prerequisites"></a>前提条件
* Azure アカウント。[無料アカウント](https://azure.microsoft.com/free)を作成できます。
* [OneDrive](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3) アカウント 

ロジック アプリで OneDrive アカウントを使用するには、OneDrive アカウントに接続するロジック アプリを承認してください。  これは、Azure ポータルのロジック アプリ内で簡単に実行できます。 

次の手順に従って、OneDrive アカウントに接続するロジック アプリを承認します。

1. ロジック アプリを作成します。 Logic Apps デザイナーで、ドロップダウン リストから **[Microsoft が管理している API を表示]** を選択し、検索ボックスに「onedrive」と入力します。 トリガーまたはアクションの 1 つを選択します。  
   ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. これまでに OneDrive への接続を作成したことがない場合は、OneDrive の資格情報を使用してサインインするよう求められます。  
   ![](./media/connectors-create-api-onedrive/onedrive-2.png)
3. **[サインイン]** を選択し、ユーザー名とパスワードを入力します。 **[サインイン]** をクリックします。  
   ![](./media/connectors-create-api-onedrive/onedrive-3.png)   
   
    この資格情報は、接続するロジック アプリの承認と、OneDrive アカウントのデータへのアクセスに使用されます。 
4. **[はい]** を選択して、OneDrive アカウントの使用をロジック アプリに承認します。  
   ![](./media/connectors-create-api-onedrive/onedrive-4.png)   
5. 接続が作成されたことを確認します。 これで、ロジック アプリで他の手順に進むことができます。  
   ![](./media/connectors-create-api-onedrive/onedrive-5.png)

