---
author: alkohli
ms.service: storsimple
ms.topic: include
ms.date: 10/26/2018
ms.author: alkohli
ms.openlocfilehash: 2d0fd904dd704c704662192e1e92fe403f0971c5
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66171856"
---
#### <a name="to-install-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a>StorSimple 用 Windows PowerShell を使用してメンテナンス モードの修正プログラムをインストールするには
> [!IMPORTANT]
> メンテナンス モードでは、1 つのコントローラーに最初に修正プログラムを適用してから、その他のコントローラーに適用する必要があります。
> 
> 

1. デバイスをメンテナンス モードにします。 「[手順 2: メンテナンス モードを開始する](../articles/storsimple/storsimple-update-device.md#step2)」で、メンテナンス モードを開始する方法について参照してください。
2. 修正プログラムを適用するには、次のように入力します。
   
     `Start-HcsHotfix` 
3. メッセージが表示されたら、修正プログラムのファイルが含まれているネットワーク共有フォルダーへのパスを入力します。
4. 確認を求められます。 「 **Y** 」と入力して修正プログラムのインストールを続行します。
5. 1 つのコントローラーで修正プログラムを適用した後、別のコントローラーにサインインします。 前のコントローラーと同様に修正プログラムを適用します。
6. 修正プログラムが適用されたら、メンテナンス モードを終了します。 手順については、「[手順 4: メンテナンス モードを終了する](../articles/storsimple/storsimple-update-device.md#step4)」を参照してください。

