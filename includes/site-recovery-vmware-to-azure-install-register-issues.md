---
author: rayne-wiselman
ms.service: site-recovery
ms.topic: include
ms.date: 10/26/2018
ms.author: raynew
ms.openlocfilehash: 9919521c8cb77f23f50a8097c4e630b4467dc725
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66127738"
---
### <a name="installation-failures"></a>インストール エラー
| **サンプルのエラー メッセージ** | **推奨される操作** |
|--------------------------|------------------------|
|エラー   アカウントを読み込めませんでした。 エラー:System.IO.IOException:Unable to read data from the transport connection when installing and registering the CS server (CS サーバーをインストールおよび登録するときに転送接続からデータを読み取れません)| コンピューターで TLS 1.0 が有効になっていることを確認します。 |

### <a name="registration-failures"></a>登録エラー
登録エラーは **%ProgramData%\ASRLogs** フォルダーのログを確認してデバッグできます。

| **サンプルのエラー メッセージ** | **推奨される操作** |
|--------------------------|------------------------|
|**09:20:06**:InnerException.Type:SrsRestApiClientLib.AcsException,InnerException.<br>メッセージ:ACS50008:SAML token is invalid. (SAML トークンが無効です。)<br>トレース ID:1921ea5b-4723-4be7-8087-a75d3f9e1072<br>関連付け ID:62fea7e6-2197-4be4-a2c0-71ceb7aa2d97><br>タイムスタンプ:**2016-12-12 14:50:08Z<br>** | システム クロックの時刻と現地時刻に 15 分以上の差がないことを確認します。 インストーラーを再実行して登録を完了します。|
|**09:35:27** :DRRegistrationException while trying to get all disaster recovery vault for the selected certificate: : (選択された証明書のすべてのディザスター リカバリー コンテナーを所得使用として DRRegistrationException が発生しました)Threw Exception.Type:Microsoft.DisasterRecovery.Registration.DRRegistrationException, Exception.Message:ACS50008:SAML token is invalid. (SAML トークンが無効です。)<br>Trace ID: e5ad1af1-2d39-4970-8eef-096e325c9950<br>Correlation ID: abe9deb8-3e64-464d-8375-36db9816427a<br>タイムスタンプ:**2016-05-19 01:35:39Z**<br> | システム クロックの時刻と現地時刻に 15 分以上の差がないことを確認します。 インストーラーを再実行して登録を完了します。|
|06:28:45:Failed to create certificate<br>06:28:45:Setup cannot proceed. A certificate required to authenticate to Site Recovery cannot be created. Rerun Setup | ローカル管理者としてセットアップを実行していることを確認します。 |
