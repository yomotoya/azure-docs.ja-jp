---
title: Azure Security Center での Endpoint Protection ソリューションの検出と正常性評価 | Microsoft Docs
description: Endpoint Protection ソリューションを検出し、正常と識別する方法。
services: security-center
documentationcenter: na
author: monhaber
manager: barbkess
ms.assetid: 2730a2f5-20bc-4027-a1c2-db9ed0539532
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2019
ms.author: v-mohabe
ms.openlocfilehash: b17e5f16b988bfa562b00bc6f5b9dfd34be4ca43
ms.sourcegitcommit: 509e1583c3a3dde34c8090d2149d255cb92fe991
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2019
ms.locfileid: "66245574"
---
# <a name="endpoint-protection-assessment-and-recommendations-in-azure-security-center"></a>Azure Security Center での Endpoint Protection の評価と推奨事項

Azure Security Center の Endpoint Protection の評価と推奨事項では、Endpoint Protection ソリューションの[サポートされている](https://docs.microsoft.com/azure/security-center/security-center-os-coverage#supported-platforms-for-windows-computers-and-vms)バージョンが検出され、正常性評価が行われます。 このトピックでは、Azure Security Center による Endpoint Protection ソリューションに対する次の 2 つの推奨事項が生成されるシナリオについて説明します。

* **仮想マシンに Endpoint Protection ソリューションをインストールする**
* **マシンの Endpoint Protection の正常性の問題を解決する**

## <a name="windows-defender"></a>Windows Defender

* "**仮想マシンに Endpoint Protection ソリューションをインストールする**" の推奨事項は、[Get-MpComputerStatus](https://docs.microsoft.com/powershell/module/defender/get-mpcomputerstatus?view=win10-ps) が実行され、結果が **AMServiceEnabled:False** の場合に生成されます

* "**マシンの Endpoint Protection の正常性の問題を解決する**" の推奨事項は、[Get-MpComputerStatus](https://docs.microsoft.com/powershell/module/defender/get-mpcomputerstatus?view=win10-ps) が実行され、次のいずれかまたは両方が発生した場合に生成されます。

  * 次のプロパティの少なくとも 1 つが false である。

     **AMServiceEnabled**

     **AntispywareEnabled**

     **RealTimeProtectionEnabled**

     **BehaviorMonitorEnabled**

     **IoavProtectionEnabled**

     **OnAccessProtectionEnabled**

  * 次のプロパティのいずれかまたは両方が 7 以上である場合。

     **AntispywareSignatureAge**

     **AntivirusSignatureAge**

## <a name="microsoft-system-center-endpoint-protection"></a>Microsoft System Center Endpoint Protection

* "**仮想マシンに Endpoint Protection ソリューションをインストールする**" の推奨事項は、**SCEPMpModule ("$env:ProgramFiles\Microsoft Security Client\MpProvider\MpProvider.psd1")** をインポートし、**AMServiceEnabled = false** で **Get-MProtComputerStatus** 結果を実行している場合に生成されます

* "**マシンの Endpoint Protection の正常性の問題を解決する**" の推奨事項は、**Get-MprotComputerStatus** が実行され、次のいずれかまたは両方が発生した場合に生成されます。

    * 次のプロパティの少なくとも 1 つが false である。

       **AMServiceEnabled**
    
       **AntispywareEnabled**
    
       **RealTimeProtectionEnabled**
    
       **BehaviorMonitorEnabled**
    
       **IoavProtectionEnabled**
    
       **OnAccessProtectionEnabled**
          
    * 次のシグネチャの更新のいずれかまたは両方が 7 以上である場合。 

       **AntispywareSignatureAge**
    
       **AntivirusSignatureAge**

## <a name="trend-micro"></a>Trend Micro

* "**仮想マシンに Endpoint Protection ソリューションをインストールする**" の推奨事項は、次の 1 つまたは複数のチェックが満たされていない場合に生成されます。
    * **HKLM:\SOFTWARE\TrendMicro\Deep Security Agent** が存在する
    * **HKLM:\SOFTWARE\TrendMicro\Deep Security Agent\InstallationFolder** が存在する
    * インストール フォルダーに **dsq_query.cmd** ファイルがある
    * **Component.AM.mode: on - Trend Micro Deep Security Agent detected** で **dsa_query.cmd** 結果が実行されている

## <a name="symantec-endpoint-protection"></a>Symantec Endpoint Protection
"**仮想マシンに Endpoint Protection ソリューションをインストールする**" の推奨事項は、次のいずれかのチェックが満たされていない場合に生成されます。

* **HKLM:\Software\Symantec\Symantec Endpoint Protection\CurrentVersion\PRODUCTNAME = "Symantec Endpoint Protection"**

* **HKLM:\Software\Symantec\Symantec Endpoint Protection\CurrentVersion\public-opstate\ASRunningStatus = 1**

または

* **HKLM:\Software\Wow6432Node\Symantec\Symantec Endpoint Protection\CurrentVersion\PRODUCTNAME = "Symantec Endpoint Protection"**

* **HKLM:\Software\Wow6432Node\Symantec\Symantec Endpoint Protection\CurrentVersion\public-opstate\ASRunningStatus = 1**

"**マシンの Endpoint Protection の正常性の問題を解決する**" の推奨事項は、次のいずれかのチェックが満たされていない場合に生成されます。  

* Symantec バージョン 12 以上のチェック:レジストリの場所:**HKLM:\Software\Symantec\Symantec Endpoint Protection\CurrentVersion" - 値 "PRODUCTVERSION"**

* リアルタイム保護の状態のチェック:**HKLM:\Software\Wow6432Node\Symantec\Symantec Endpoint Protection\AV\Storages\Filesystem\RealTimeScan\OnOff == 1**

* シグネチャの更新の状態のチェック:**HKLM\Software\Symantec\Symantec Endpoint Protection\CurrentVersion\public-opstate\LatestVirusDefsDate <= 7 日**

* フル スキャンの状態のチェック:**HKLM:\Software\Symantec\Symantec Endpoint Protection\CurrentVersion\public-opstate\LastSuccessfulScanDateTime <= 7 日**

* Symantec 12 のシグネチャのバージョンへのシグネチャ バージョン番号パスの検索:**レジストリ パス + "CurrentVersion\SharedDefs" - 値 "SRTSP"** 

* Symantec 14 のシグネチャのバージョンへのパス:**レジストリ パス + "CurrentVersion\SharedDefs\SDSDefs" - 値 "SRTSP"**

レジストリ パス:

**"HKLM:\Software\Symantec\Symantec Endpoint Protection" + $Path**
 **"HKLM:\Software\Wow6432Node\Symantec\Symantec Endpoint Protection" + $Path**

## <a name="mcafee-endpoint-protection-for-windows"></a>McAfee Endpoint Protection for Windows

"**仮想マシンに Endpoint Protection ソリューションをインストールする**" の推奨事項は、次のチェックが満たされていない場合に生成されます。

* **HKLM:\SOFTWARE\McAfee\Endpoint\AV\ProductVersion** が存在する

* **HKLM:\SOFTWARE\McAfee\AVSolution\MCSHIELDGLOBAL\GLOBAL\enableoas = 1**

"**マシンの Endpoint Protection の正常性の問題を解決する**" の推奨事項は、次のチェックが満たされていない場合に生成されます。

* McAfee バージョン:**HKLM:\SOFTWARE\McAfee\Endpoint\AV\ProductVersion >= 10**

* シグネチャのバージョンの検索:**HKLM:\Software\McAfee\AVSolution\DS\DS - 値 "dwContentMajorVersion"**

* シグネチャの日付の検索:**HKLM:\Software\McAfee\AVSolution\DS\DS - 値 "szContentCreationDate" >= 7 日**

* スキャン日の検索:**HKLM:\Software\McAfee\Endpoint\AV\ODS - 値 "LastFullScanOdsRunTime" >= 7 日**

## <a name="troubleshoot-and-support"></a>トラブルシューティングとサポート

### <a name="troubleshoot"></a>トラブルシューティング

Microsoft マルウェア対策拡張機能ログは次から入手できます。  
**%Systemdrive%\WindowsAzure\Logs\Plugins\Microsoft.Azure.Security.IaaSAntimalware(Or PaaSAntimalware)\1.5.5.x(version#)\CommandExecution.log**

### <a name="support"></a>サポート

この記事についてさらにヘルプが必要な場合は、いつでも [MSDN の Azure フォーラムと Stack Overflow フォーラム](https://azure.microsoft.com/support/forums/)で Azure エキスパートに問い合わせることができます。 または、Azure サポート インシデントを送信できます。 その場合は、[Azure サポートのサイト](https://azure.microsoft.com/support/options/)に移動して、[サポートの要求] をクリックします。 Azure サポートの使用方法の詳細については、「 [Microsoft Azure サポートに関する FAQ](https://azure.microsoft.com/support/faq/)」を参照してください。
