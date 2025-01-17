---
author: alkohli
ms.service: storsimple
ms.topic: include
ms.date: 10/26/2018
ms.author: alkohli
ms.openlocfilehash: 560c9c177bfa693580979101e5b9343fcff7fe40
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66171188"
---
### <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>StorSimple 用 Windows PowerShell を使用したメンテナンス モードの更新プログラムのインストール

StorSimple デバイスにメンテナンス モードの更新プログラムを適用すると、すべての I/O 要求が一時停止します。 非揮発性ランダム アクセス メモリ (NVRAM) などのサービスやクラスター化サービスが停止されます。 このモードを開始または終了するときに、両方のコントローラーが再起動します。 このモードを終了すると、すべてのサービスが再開され、正常な状態になります  (これには数分かかることがあります)。

> [!IMPORTANT]
> * メンテナンス モードを開始する前に、Azure Portal で両方のデバイス コントローラーが正常であることを確認してください。 コントローラーが正常な状態でない場合は次の手順を [Microsoft サポートにお問い合わせください](../articles/storsimple/storsimple-8000-contact-microsoft-support.md)。
> * メンテナンス モードになっているときは、1 つのコントローラーを最初に更新してから、他のコントローラーを更新する必要があります。

1. PuTTY を使ってシリアル コンソールに接続します。 詳細については、[PuTTy を使用してシリアル コンソールに接続する方法](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)に関するセクションを参照してください。 コマンド プロンプトで **Enter**キーを押します。 オプション 1 の **[Log in with full access]\(フル アクセスによるログイン\)** を選択します。

2. コントローラーをメンテナンス モードにするには、次のように入力します。
    
    `Enter-HcsMaintenanceMode`

    両方のコントローラーがメンテナンス モードで再起動します。

3. メンテナンス モードの更新プログラムをインストールします。 型: 

    `Start-HcsUpdate`

    確認を求められます。 更新プログラムを確認すると、現在アクセスしているコントローラーにインストールされます。 更新プログラムがインストールされると、コントローラーが再起動されます。

4. 更新プログラムの状態を監視します。 現在のコントローラーは更新中で他のコマンドを処理できないので、ピア コントローラーにサインインします。 型: 

    `Get-HcsUpdateStatus`

    `RunInProgress` が `True` の場合は、更新が実行中です。 `RunInProgress` が `False` の場合は、更新が完了したことを示します。

5. ディスク ファームウェアの更新プログラムが正常に適用されて、更新されたコントローラーが再起動した後、ディスク ファームウェアのバージョンを確認します。 更新されたコントローラーで、次のように入力します。

    `Get-HcsFirmwareVersion`
   
    予想されるディスク ファームウェアのバージョンは次のとおりです。`XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`

6. メンテナンス モードを終了します。 各デバイス コントローラーに対して次のコマンドを入力します。

    `Exit-HcsMaintenanceMode`

    メンテナンス モードを終了すると、コントローラーが再起動します。

7. Azure Portal に戻ります。 メンテナンス モードの更新プログラムがインストールされたことがポータルに表示されるまでに、24 時間かかる可能性があります。