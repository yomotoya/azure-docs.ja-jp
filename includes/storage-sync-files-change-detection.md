---
author: tamram
ms.service: storage
ms.topic: include
ms.date: 10/26/2018
ms.author: tamram
ms.openlocfilehash: beb08c29587e4ce522131142fd61925b5af45fa9
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66114561"
---
Azure Portal または SMB を使用して Azure ファイル共有に加えられた変更は、サーバー エンドポイントに対する変更とは異なり、検出とレプリケーションが即座に行われることはありません。 Azure Files にはまだ変更通知/ジャーナルがないため、ファイルが変更されたときに自動的に同期セッションを開始する方法はありません。 Windows Server では、Azure File Sync は [Windows USN ジャーナル](https://msdn.microsoft.com/library/windows/desktop/aa363798.aspx)を使用して、ファイルが変更されたときに同期セッションを自動的に開始します。<br /><br /> Azure ファイル共有に対する変更を検出するために、Azure File Sync には、*変更検出ジョブ*と呼ばれるスケジュールされたジョブがあります。 変更検出ジョブは、ファイル共有内のすべてのファイルを列挙した後、ファイルの同期バージョンと比較します。 変更検出ジョブによってファイルが変更されていると判断された場合に、Azure File Sync は同期セッションを開始します。 変更検出ジョブは 24 時間ごとに実行されます。 変更検出ジョブは Azure ファイル共有内のすべてのファイルを列挙することで機能するため、変更の検出は、大きな名前空間のほうが小さな名前空間よりも時間がかかります。 大規模な名前空間の場合、変更されたファイルを判断するのに 24 時間ごとに 1 回より長くなる場合があります。<br /><br />
なお、REST を使用して Azure ファイル共有に加えられた変更は、SMB の最終更新時刻を更新するものではなく、同期による変更とは見なされません。 <br /><br />
Windows Server 上のボリュームに対する USN のような変更検出を Azure ファイル共有に追加するための調査を行っています。 今後この機能の開発を優先的に進めるために、[Azure Files UserVoice](https://feedback.azure.com/forums/217298-storage/category/180670-files) で投票をお願いします。
