---
title: インクルード ファイル
description: インクルード ファイル
services: site-recovery
author: rayne-wiselman
manager: carmonm
ms.service: site-recovery
ms.topic: include
ms.date: 09/12/2018
ms.author: raynew
ms.openlocfilehash: f4cd9cad3813378fcdc3f06e8ab1c28eced4f93c
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66116023"
---
Name | 商用の URL | 政府機関の URL | 説明
--- | --- | --- | ---
Azure Active Directory | ``login.microsoftonline.com`` | ``login.microsoftonline.us`` | Azure Active Directory を使用したアクセス制御と ID 管理に使用されます。 
バックアップ | ``*.backup.windowsazure.com`` | ``*.backup.windowsazure.us`` | レプリケーション データの転送と調整に使用。
レプリケーション | ``*.hypervrecoverymanager.windowsazure.com`` | ``*.hypervrecoverymanager.windowsazure.us``  | レプリケーション管理操作と調整に使用。
Storage | ``*.blob.core.windows.net`` | ``*.blob.core.usgovcloudapi.net``  | レプリケートされたデータを格納するストレージ アカウントへのアクセスに使用。
テレメトリ (オプション) | ``dc.services.visualstudio.com`` | ``dc.services.visualstudio.com`` | テレメトリに使用されます。
時刻同期 | ``time.windows.com`` | ``time.nist.gov`` | すべてのデプロイでシステム時刻とグローバル時刻の間の時刻同期を確認するために使用されます。


