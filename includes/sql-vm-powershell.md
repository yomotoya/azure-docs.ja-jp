---
author: MikeRayMSFT
ms.service: virtual-machines-sql
ms.topic: include
ms.date: 11/25/2018
ms.author: mikeray
ms.openlocfilehash: c6666f4417cde9e0f77cc965ded1d6bdb5dced34
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66165819"
---
## <a name="start-your-powershell-session"></a>PowerShell セッションの開始
 

[**Connect-Az Account**](https://docs.microsoft.com/powershell/module/Az.Accounts/Connect-AzAccount) コマンドレットを実行すると、資格情報を入力するサインイン画面が表示されます。 Azure ポータルにサインインするときと同じ資格情報を使用してください。

```powershell
Connect-AzAccount
```

複数のサブスクリプションがある場合は、[**Set-AzContext**](https://docs.microsoft.com/powershell/module/az.accounts/set-azcontext) コマンドレットを使用して、PowerShell セッションで使用するサブスクリプションを選択します。 PowerShell セッションが現在使用しているサブスクリプションを確認するには、[**Get-AzContext**](https://docs.microsoft.com/powershell/module/az.accounts/get-azcontext) を実行します。 すべてのサブスクリプションを表示するには、[**Get-AzSubscription**](https://docs.microsoft.com/powershell/module/az.accounts/get-azsubscription) を実行します。

```powershell
Set-AzContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```

