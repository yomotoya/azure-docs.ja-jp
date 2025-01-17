---
author: alkohli
ms.service: storsimple
ms.topic: include
ms.date: 10/26/2018
ms.author: alkohli
ms.openlocfilehash: c10482029e6cfce7063d205161fed54030919c48
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66159688"
---
#### <a name="to-stop-and-start-a-cloud-appliance"></a>クラウド アプライアンスを停止および開始するには

1. クラウド アプライアンスを停止するには、クラウド アプライアンスの VM に移動します。
    ![StorSimple Cloud Appliance 仮想マシン](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)

2. コマンド バーで **[停止]** をクリックします。

    ![StorSimple Cloud Appliance 仮想マシン](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. 確認を求められたら、 **[はい]** をクリックします。

    ![StorSimple Cloud Appliance 仮想マシン](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. 仮想マシンを停止すると、割り当てが解除されます。 クラウド アプライアンスが停止している間、状態は **[割り当て解除中]** になります。 クラウド アプライアンスが停止されると、状態は **[停止済み (割り当て解除)]** になります。

    ![StorSimple Cloud Appliance 仮想マシン](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. VM が停止したら、**[開始]**(ボタンが使用可能になっている) をクリックして VM を起動します。 クラウド アプライアンスが開始されると、状態は **[開始済み]** になります。

    ![StorSimple Cloud Appliance 仮想マシン](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

以下は、クラウド アプライアンスを停止および開始するためのコマンドレットです。

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-cloud-appliance"></a>クラウド アプライアンスを再起動するには

クラウド アプライアンスを再起動するには、クラウド アプライアンスの VM に移動します。 コマンド バーで **[再起動]** をクリックします。 メッセージが表示されたら、再起動を確定します。 クラウド アプライアンスを使用する準備ができると、状態が **[実行中]** になります。

![StorSimple Cloud Appliance 仮想マシン](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

以下は、クラウド アプライアンスを再起動するためのコマンドレットです。

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

