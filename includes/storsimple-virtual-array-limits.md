---
author: alkohli
ms.service: storsimple
ms.topic: include
ms.date: 10/26/2018
ms.author: alkohli
ms.openlocfilehash: 658fd9178495f14274c85eab2129c9dcd3be7693
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66143288"
---
| **制限の種類** | **制限** | **説明** |
| --- | --- | --- |
| 総容量 (クラウドを含む) |仮想デバイスあたり最大 64 TB |StorSimple Virtual Array 全体を別の空のアレイにフェールオーバーできます。 同じデバイスに復元する場合は、デバイスにこの操作を実行できるだけの十分な領域があることを確認してください。 32 TB を超えると、同じデバイスには復元できません。 |
| デバイスあたりのストレージ アカウントの資格情報の最大数 |1 | |
| ボリューム/共有の最大数 |16 | |
| 階層化共有の最小サイズ |500 GB | |
| 階層化ボリュームの最小サイズ |500 GB | |
| 階層化共有の最大サイズ |20 TB | |
| 階層化ボリュームの最大サイズ |5 TB | |
| ローカル固定共有の最小サイズ |50 GB | |
| ローカル固定ボリュームの最小サイズ |50 GB | |
| ローカル固定共有の最大サイズ |2 TB | |
| ローカル固定ボリュームの最大サイズ |200 GB | |
| イニシエーターからの iSCSI 接続の最大数 |512 | |
| デバイスごとのアクセス制御レコードの最大数 |64 | |
| 仮想デバイスによってファイル サーバー用の *.backups* フォルダーに保持されるバックアップの最大数 |5 |これには、最近スケジュールされたバックアップ (既定のバックアップ ポリシーによって生成) と手動バックアップが含まれます。 |
| デバイスによって保持される、スケジュールされたバックアップの最大数 |55 |30 日分のバックアップ<br>12 か月分のバックアップ<br>13 年分のバックアップ |
| デバイスによって保持される、手動バックアップの最大数 |45 | |
| ファイル サーバーの共有ごとのファイルの最大数 |100 万 |デバイスの復元を実行する際は、デバイス上のすべての共有に存在するファイルの数に応じて、復元にかかる時間が変わります。 |
| iSCSI サーバーのボリュームごとのファイルの最大数 |100 万 | |
| 仮想配列ごとのファイルの最大数 |400 万 | |
| 復元による復旧時間 |すばやい復元 |復元はヒート マップに基づいており、ボリューム サイズに左右されます。<br>復元操作の実行中にも、バックアップ操作を実行できます。 |

