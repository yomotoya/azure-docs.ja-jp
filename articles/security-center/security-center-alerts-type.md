---
title: Azure Security Center における各種のセキュリティ アラート | Microsoft Docs
description: この記事では、Azure Security Center で利用できるさまざまなセキュリティ アラートについて説明します。
services: security-center
documentationcenter: na
author: monhaber
manager: barbkess
editor: ''
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/20/2018
ms.author: v-mohabe
ms.openlocfilehash: 4592caacf7f73e4bce9f974fb3bb2ab3ed1a89ff
ms.sourcegitcommit: e9a46b4d22113655181a3e219d16397367e8492d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65968364"
---
# <a name="understanding-security-alerts-in-azure-security-center"></a>Azure Security Center のセキュリティ アラートの概要
この記事では、Azure Security Center で利用できるさまざまなセキュリティ アラートと関連する分析情報についてわかりやすく説明します。 アラートとインシデントを管理する方法の詳細については、「[Azure Security Center でのセキュリティの警告の管理と対応](security-center-managing-and-responding-alerts.md)」を参照してください。

高度な検出をセットアップする場合には、Azure Security Center Standard にアップグレードする必要があります。 無料試用版が提供されています。 アップグレードするには、[[セキュリティ ポリシー]](tutorial-security-policy.md) で **[価格レベル]** を選択します。 詳細については、[価格のページ](https://azure.microsoft.com/pricing/details/security-center/)を参照してください。

## <a name="what-type-of-alerts-are-available"></a>使用できる警告の種類
Azure Security Center では、さまざまな[検出機能](security-center-detection-capabilities.md)を使用して、お客様の環境を対象とする攻撃の可能性を通知します。 これらのアラートには、アラートをトリガーした要因、対象となったリソース、攻撃元に関する重要な情報が含まれています。 こうした情報は、脅威を検出するために使用された分析の種類によって異なります。 インシデントには、脅威を調査する際に活用できる追加のコンテキスト情報も含まれる可能性があります。  この記事では、次の警告の種類について説明します。

* 仮想マシンの動作分析 (VMBA)
* ネットワーク分析
* SQL Database と SQL Data Warehouse の分析
* コンテキスト情報

## <a name="virtual-machine-behavioral-analysis"></a>仮想マシンの動作分析
Azure Security Center は動作分析を使用し、仮想マシンのイベント ログの分析に基づいて、侵害の発生したリソースを特定します。 分析対象となるイベントには、プロセス作成イベント、ログイン イベントなどがあります。 また、他のシグナルとの間には、蔓延している攻撃の裏付けとなる兆候を確認できる相関関係が存在します。

> [!NOTE]
> Security Center の検出機能に関する詳細については、「[Azure Security Center の検出機能](security-center-detection-capabilities.md)」を参照してください。


### <a name="event-analysis"></a>イベントの分析
Security Center は高度な分析を使用し、仮想マシンのイベント ログの分析に基づいて、侵害の発生したリソースを特定します。 分析対象となるイベントには、プロセス作成イベント、ログイン イベントなどがあります。 また、他のシグナルとの間には、蔓延している攻撃の裏付けとなる兆候を確認できる相関関係が存在します。

* **Suspicious process execution detected (疑わしいプロセスの実行が検出されました)**: 多くの場合、攻撃者は、無害なプロセスを偽装して、検出されずに悪意のあるコードを実行しようとします。 これらのアラートは、プロセスの実行が次のパターンのいずれかと一致したことを示します。
    * 悪意のある目的に使用されることがわかっているプロセスが実行されました。 個々のコマンドは害がないように見える可能性がありますが、それらのコマンドの集合に基づいてアラートが評価されます。
    * 一般的ではない場所からプロセスが実行されました。
    * 既知の疑わしいファイルと共通する場所からプロセスが実行されました。
    * 疑わしいパスからプロセスが実行されました。
    * 異常なコンテキストでプロセスが実行されました。
    * 通常とは異なるアカウントによってプロセスが実行されました
    * 疑わしい拡張子のプロセスが実行されました。
    * 疑わしい二重の拡張子があるプロセスが実行されました。
    * ファイル名に疑わしい右から左 (RLO) の文字を含むプロセスが実行されました。
    * 名前は似ているものの一般的に実行されるプロセスとは異なるプロセスが実行されました
    * 既知の攻撃ツールに対応する名前のプロセスが実行されました。
    * ランダムな名前のプロセスが実行されました。
    * 疑わしい拡張子のプロセスが実行されました。
    * 隠しファイルが実行されました。
    * プロセスが、別の無関係なプロセスの子として実行されました。
    * システム プロセスによって通常とは異なるプロセスが作成されました。
    * 異常なプロセスが Windows 更新プログラム サービスによって開始されました。
    * 通常とは異なるコマンド ラインでプロセスが実行されました。 これは、悪意のあるコンテンツの実行のために正当なプロセスが乗っ取られていることと関連しています。
    * コマンド ラインから、ディレクトリ内のすべての実行可能ファイル (*.exe) の実行が試行されました。
    * プロセスが PsExec ユーティリティによって実行されました。このユーティリティは、プロセスのリモート実行に使用される可能性があります。
    * 疑わしい子プロセスの起動に Apache Tomcat® Parent 実行可能ファイル (Tomcat#.exe) が使用されました。この子プロセスは、悪意のあるコマンドをホストまたは起動する可能性があります。
    * 悪意のある可能性がある実行可能コードの起動に Microsoft Windows の "プログラム互換性アシスタント" (pcalua.exe) が使用されました。
    * 疑わしいプロセス終了バーストが検出されました。
    * システム プロセス SVCHOST が異常なコンテキストで実行されました。
    * システム プロセス SVCHOST がほとんど使用されないサービス グル​​ープで実行されました。
    * 疑わしいコマンド ラインが実行されました。
    * PowerShell スクリプトには、既知の疑わしいスクリプトと共通の特徴があります。
    * 既知の悪意のある PowerShell Powersploit コマンドレットが実行されました。
    * 組み込みの SQL ユーザーが通常は実行しないプロセスを実行しました
    * Base-64 でエンコードされた実行可能ファイルが検出されました。これは、攻撃者が一連のコマンドを使用して、その場で実行可能ファイルを構築することで、検出を無効にしようとしている可能性があります。

* **Suspicious RDP resource activity (疑わしい RDP リソース アクティビティ)**: 攻撃者は、RDP などのオープンな管理ポートをブルート フォース攻撃のターゲットにすることがよくあります。 これらのアラートは、次のような疑わしいリモート デスクトップ ログイン アクティビティを示します。
    * リモート デスクトップ ログインが複数回試行されました。
    * 無効なアカウントを使用してリモート デスクトップ ログインが複数回試行されました。
    * リモート デスクトップ ログインが複数回試行され、その一部がマシンに正常にログインできました。
* **Suspicious SSH resource activity (疑わしい SSH リソース アクティビティ)**: 攻撃者は、SSH などのオープンな管理ポートをブルート フォース攻撃のターゲットにすることがよくあります。 これらのアラートは、次のような疑わしい SSH ログイン アクティビティを示します。
    * SSH ログインが複数回失敗しました。
    * SSH ログインが複数回試行され、その一部が成功しました。
* **Suspicious WindowPosition registry value (疑わしい WindowPosition レジストリ値)**: このアラートは、WindowPosition レジストリ構成の変更が試行されたことを示します。これは、デスクトップの非表示セクションにアプリケーション ウィンドウを隠していることを示す可能性があります。
* **Potential attempt to bypass AppLocker (AppLocker をバイパスする潜在的試行)**: AppLocker は、Windows 上で実行できるプロセスを制限し、マルウェアに対する露出を制限するために使用できます。 このアラートは、信頼できないコードを実行するために、(AppLocker ポリシーによって許可された) 信頼できる実行可能ファイルを使用して AppLocker の制限のバイパスが試行された可能性があることを示します。
* **Suspicious named pipe communications (疑わしい名前付きパイプ通信)**: このアラートは、Windows コンソール コマンドからローカルの名前付きパイプにデータが書き込まれたことを示します。 名前付きパイプは、攻撃者が悪意のあるインプラントを使用し、通信するために使用されることがわかっています。
* **Decoding of an executable using built-in certutil.exe tool (組み込みの certutil.exe ツールを使用した実行可能ファイルのデコード)**: このアラートは、組み込みの管理者ユーティリティ certutil.exe が実行可能ファイルのデコードに使用されたことを示します。 攻撃者は、正規の管理者ツールの機能を悪用して悪意のある操作を実行することがわかっています。たとえば、悪意のある実行ファイルのデコードに certutil.exe などのツールが使用され、デコード後のファイルが実行されることがあります。
* **An event log was cleared (イベント ログがクリアされました)**: このアラートは、疑わしいイベント ログのクリア操作を示します。これは、痕跡を隠そうとする攻撃者によってよく使用されます。
* **Disabling and deleting IIS log files (IIS ログ ファイルの無効化と削除)**: このアラートは、IIS ログファイルが無効になったか、削除されたことを示します。これは、痕跡を隠そうとする攻撃者によってよく使用されます。
* **Suspicious file deletion (疑わしいファイルの削除)**: このアラートは、ファイルの疑わしい削除を示します。攻撃者が悪意のあるバイナリの証拠を削除するために使用した可能性があります。
* **All file shadow copies have been deleted (すべてのファイル シャドウ コピーが削除されました)**: このアラートは、シャドウ コピーが削除されたことを示します。
* **Suspicious file cleanup commands (疑わしいファイルのクリーンアップ コマンド)**: このアラートは、侵害後に自己クリーンアップ アクティビティを実行するために systeminfo コマンドの組み合わせが使用されたことを示します。  *systeminfo.exe* は正規の Windows ツールですが、2 回連続して実行され、その後に削除コマンドが実行される方法はまれです。
* **Suspicious account creation (疑わしいアカウント作成)**: このアラートは、既存の組み込みの管理特権アカウントによく似たアカウントが作成されたことを示します。 この手法は、攻撃者が検出されずに不正なアカウントを作成するために使用されることがあります。
* **Suspicious volume shadow copy activity (疑わしいボリューム シャドウ コピー アクティビティ)**: このアラートは、リソースに対するシャドウ コピーの削除アクティビティを示します。 ボリューム シャドウ コピー (VSC) は、データ スナップショットを保存する重要なアーティファクトです。 このアクティビティはランサムウェアに関連していますが、正当なアクティビティの可能性もあります。
* **Windows registry persistence method (Windows レジストリ永続性メソッド)**: このアラートは、Windows レジストリにおける実行可能ファイルの永続化の試行を示します。 マルウェアは、起動時に存続するように、このような手法を使用することがよくあります。
* **Suspicious new firewall rule (疑わしい新しいファイアウォール ルール)**: このアラートは、*netsh.exe* を介して、疑わしい場所の実行可能ファイルからのトラフィックを許可する新しいファイアウォール ルールが追加されたことを示します。
* **Suspicious XCOPY executions (疑わしい XCOPY の実行)**: このアラートは、一連の XCOPY が実行されたを示します。これは、お客様のいずれかのマシンが侵害され、マルウェアを伝播するために使用されたことを示す可能性があります。
* **Suppression of legal notice displayed to users at logon (ログオン時にユーザーに表示される法的通知の抑制)**: このアラートは、サインイン時に法的通知をユーザーに表示するかどうかを制御するレジストリ キーの変更を示します。 これは、攻撃者がホストを侵害した後に行われる一般的なアクティビティです。
* **Detected anomalous mix of upper and lower case characters in command line (コマンド ラインで通常とは異なる大文字と小文字の混在が検出されました)**: このアラートは、コマンド ラインで大文字と小文字が混在していることを示します。これは、大文字と小文字を区別する、またはハッシュベースのマシン ルールから隠ぺいするために攻撃者が使用する手法です。
* **Obfuscated command line (難読化されたコマンド ライン)**: このアラートは、疑わしい難読化の兆候がコマンド ラインで検出されたことを示します。
* **Multiple domain accounts queried (複数のドメイン アカウントが照会されました)**: 攻撃者は、ユーザー、ドメイン管理者アカウント、ドメイン コントローラー、およびドメイン間の信頼関係に関する偵察を実行するときに、AD ドメイン アカウントを照会することがよくあります。 このアラートは、短期間に通常とは異なる数のドメイン アカウントが照会されたことを示します。
* **Possible local reconnaissance activity (ローカル偵察アクティビティの可能性)**: このアラートは、偵察アクティビティに関連する systeminfo コマンドの組み合わせが実行されたことを示します。  *systeminfo.exe* は正当な Windows ツールですが、2 回連続して実行されることはまれです。
* **Possible execution of keygen executable (keygen 実行可能ファイルが実行された可能性があります)**: このアラートは、keygen ツールを示す名前のプロセスが実行されたことを示します。 このようなツールは、通常、ソフトウェア ライセンス メカニズムを無効にするために使用されますが、他の悪意のあるソフトウェアがバンドルされてダウンロードされることがよくあります。
* **Suspicious execution via rundll32.exe (rundll32.exe による疑わしい実行)**: このアラートは、通常とは異なる名前のプロセスを実行するために rundll32.exe が使用されたことを示します。これは、攻撃者が侵害したホストに第 1 段階のインプラントをインストールするために使用されるプロセスの命名スキームと一致します。
* **Suspicious combination of HTA and PowerShell (HTA と PowerShell の疑わしい組み合わせ)**: このアラートは、Microsoft HTML アプリケーション ホスト (HTA) が PowerShell コマンドを起動していることを示します。 これは攻撃者が悪質な PowerShell スクリプトを起動するときに使う手法です。
* **Change to a registry key that can be abused to bypass UAC (UAC のバイパスに悪用される可能性があるレジストリ キーの変更)**: このアラートは、UAC (ユーザー アカウント制御) のバイパスに悪用される可能性があるレジストリ キーが変更されたことを示します。これは、侵害されたホスト上で特権を持たない (標準ユーザー) アクセス権から特権のある (たとえば管理者) アクセス権に移行するために攻撃者によってよく使用されます。
* **Use of suspicious domain name within command line (コマンド ラインでの疑わしいドメイン名の使用)**: このアラートは、疑わしいドメイン名が使用されたことを示します。これは、攻撃者が、指揮管理とデータの取り出しのエンドポイントとして悪意のあるツールをホストしている証拠である可能性があります。
* **An account was created on multiple hosts within a 24-hour time period (24 時間以内に複数のホストにアカウントが作成されました)**: このアラートは、複数のホストに同じユーザー アカウントの作成が試みられたことを示します。これは、攻撃者が、1 つ以上のネットワーク エンティティを侵害した後に、ネットワーク全体を横断している証拠である可能性があります。
* **Suspicious use of CACLS to lower the security state of the system (システムのセキュリティ状態を低下させる CACLS の疑わしい使用)**: このアラートは、Change Access Control List (CACLS) が変更されたことを示します。 この手法は、攻撃者が ftp.exe、net.exe、wscript.exe などのシステム バイナリに完全アクセス権を付与するためによく使われます。
* **Suspected Kerberos Golden Ticket attack parameters (疑わしい Kerberos ゴールデン チケット攻撃パラメーター)**: このアラートは、Kerberos ゴールデン チケット攻撃と一致するコマンド ライン パラメーターが実行されたことを示します。 攻撃者は侵害した krbtgt キーを使用して、目的の任意のユーザーになりすますことができます。
* **Enabling of the WDigest UseLogonCredential registry key (WDigest UseLogonCredential レジストリ キーの有効化)**: このアラートは、サインイン資格情報がクリア テキストで LSA メモリに格納されるようにレジストリ キーが変更され、その結果、資格情報をメモリから取得できるようになったことを示します。
* **Potentially suspicious use of Telegram tool (Telegram ツールの疑わしい可能性がある使用方法)**: このアラートは、Telegram がインストールされたことを示します。これは、悪意のあるバイナリを他のコンピューター、電話、またはタブレットに転送するために攻撃者が使用する無料のクラウドベースのインスタント メッセージング サービスです。
* **New ASEP creation (新しい ASEP の作成)**: このアラートは、新しい ASEP (Auto Start Extensibility Point) が作成されたことを示します。これによって、コマンド ラインで指定された名前のプロセスが自動的に開始され、攻撃者が永続化を達成するために使用する可能性があります。
* **Suspicious Set-ExecutionPolicy and WinRM changes (疑わしい Set-ExecutionPolicy と WinRM の変更)**: このアラートは、悪意のある ChinaChopper webshell の使用に関連する構成の変更を示します。
* **Disabling of critical services (重要なサービスの無効化)**: このアラートは、"net.exe stop" コマンドが SharedAccess や Windows Security Center などの重要なサービスを停止するために使用されたことを示します。
* **Suspicious use of FTP -s switch (FTP -s スイッチの疑わしい使用)**: このアラートは、FTP の "-s" スイッチが使用されたことを示します。これは、マルウェアがリモート FTP サーバーに接続し、悪意のあるバイナリをさらにダウンロードするために使用されることがあります。
* **Suspicious execution of VBScript.Encode command (VBScript.Encode コマンドの疑わしい実行)**: このアラートは、*VBScript.Encode* コマンドが実行されたことを示します。これで、スクリプトは読み取り不可能なテキストにエンコードされ、ユーザーがコードを確認しづらくなります。
* **VBScript HTTP object allocation (VBScript HTTP オブジェクトの割り当て)**: このアラートは、コマンド プロンプトを使用して VB スクリプト ファイルが作成されたことを示します。これは、悪意のあるファイルをダウンロードするために使用される可能性があります。
* **Sticky keys attack (固定キー攻撃)**: このアラートは、攻撃者がバックドア アクセスを提供するために、アクセシビリティ バイナリ (固定キー、スクリーン キーボード、ナレーターなど) を侵害している可能性があることを示します。
* **Petya ransomware indicators (Petya ランサムウェア インジケーター)**: このアラートは、Petya ランサムウェアに関連する手法が観察されたことを示します。
* **Attempt to disable AMSI (AMSI の無効化が試行されました)**: このアラートは、マルウェア対策スキャン インターフェイス (AMSI) を無効にする試行を示しています。AMSI が無効になると、マルウェア対策の検出も無効になります。
* **Ransomware indicators (ランサムウェア インジケーター)**: このアラートは、過去にロック画面と暗号化のランサムウェアに関連付けられたことがある疑わしいアクティビティを示します。
* **Suspicious trace collection output file (疑わしいトレース収集出力ファイル)**: このアラートは、トレース (ネットワーク アクティビティなど) が収集され、通常とは異なるファイルの種類に出力されたことを示します。
* **High risk software (危険度の高いソフトウェア)**: このアラートは、マルウェアのインストールに関連付けられているソフトウェアの使用を示します。 攻撃者は、このアラートに記載されているような無害のツールでマルウェアをパッケージ化し、バックグラウンドでマルウェアを自動インストールします。
* **Suspicious file creation (疑わしいファイルの作成)**: このアラートは、フィッシング ドキュメントの添付ファイルが開かれた後に、侵害されたホストにさらにマルウェアをダウンロードするために攻撃者が使用するプロセスの作成または実行を示します。
* **Suspicious credentials in command line (コマンド ラインの疑わしい資格情報)**: このアラートは、ファイルの実行に使用されたパスワードが疑わしいことを示します。 この手法は、攻撃者が Pirpi マルウェアを実行するために使用されています。
* **Possible execution of malware dropper (マルウェア ドロッパーが実行された可能性)**: このアラートは、攻撃者がマルウェアをインストールするために使用したファイル名を示します。
* **Suspicious execution via rundll32.exe (rundll32.exe による疑わしい実行)**: このアラートは、notepad.exe または reg.exe の実行に rundll32.exe が使用されていることを示します。これは、攻撃者が使用するプロセス インジェクション手法と一致しています。
* **Suspicious command line arguments (疑わしいコマンド ライン引数)**: このアラートは、アクティビティ グループ HYDROGEN によって使用されるリバース シェルと共に、疑わしいコマンド ライン引数が使用されたことを示します。
* **Suspicious document credentials (疑わしいドキュメントの資格情報)**: このアラートは、ファイルを実行するためにマルウェアによって使用されている、疑わしい共通の事前計算されたパスワード ハッシュを示します。
* **Dynamic PS script construction (動的 PS スクリプトの構築)**: このアラートは、PowerShell スクリプトが動的に構築されていることを示します。 攻撃者は、この手法を使用して、IDS システムを回避するためにスクリプトを段階的に構築します。
* **Metasploit indicators (Metasploit インジケーター)**: このアラートは、さまざまな攻撃者の機能とツールを提供する Metasploit フレームワークに関連付けられたアクティビティを示します。
* **Suspicious account activity (疑わしいアカウントアクティビティ)**: このアラートは、最近侵害されたアカウントを使用してマシンに接続しようとしたことを示します。
* **Account creation (アカウント作成)**: このアラートは、マシンに新しいアカウントが作成されたことを示します。


### <a name="crash-analysis"></a>クラッシュ分析


クラッシュ ダンプ メモリ分析は、従来のセキュリティ ソリューションを回避することができる高度なマルウェアの検出に使用される方法です。 さまざまな形式のマルウェアは、ディスクへの書き込みを行わないことや、ディスクに書き込まれたソフトウェア コンポーネントを暗号化することで、ウイルス対策製品によって検出される可能性を減らすよう試みます。 この手法が、従来のマルウェア対策手法を使ったマルウェア検出を困難にしています。 しかし、マルウェアが機能するためにはメモリに痕跡を残す必要があるので、メモリ分析を使用すればそのようなマルウェアを検出することができます。

ソフトウェアがクラッシュすると、クラッシュ時のメモリが部分的にクラッシュ ダンプにキャプチャされます。 クラッシュは、マルウェア、一般的なアプリケーション、またはシステムの問題によって引き起こされる可能性があります。 Security Center では、クラッシュ ダンプでメモリを分析することによって、ソフトウェアの脆弱性の悪用や機密データへのアクセスに使用された手法を検出できます。また、侵入したコンピューターに密かに常駐するタイプの手法であっても検出が可能です。 Security Center バックエンドによって分析が実行されるため、この方法ではホストのパフォーマンスに対する影響が最小限に抑えられます。

* **Code injection discovered (コード インジェクションが検出されました)**: コード インジェクションとは、実行中のプロセスやスレッドに実行可能なモジュールを挿入することです。 この手法は、マルウェアがデータにアクセスし、その削除を隠したり防いだりするために使用されます (たとえば永続化)。 このアラートは、挿入されたモジュールがクラッシュ ダンプに存在することを示します。 正当なソフトウェア開発者は、悪意からではなく、既存のアプリケーションやオペレーティング システム コンポーネントの変更や拡張などの目的で、コード インジェクションを実行することもあります。 悪意のある挿入モジュールと悪意のない挿入モジュールを区別できるように、Security Center は、挿入されたモジュールが疑わしい動作のプロファイルに準拠しているかどうかをチェックします。 このチェックの結果は、警告の "SIGNATURE (シグネチャ)" フィールドに表示され、警告の重大度、説明、修正手順に反映されます。
* **Suspicious code segment (疑わしいコード セグメント)**: 疑わしいコード セグメントのアラートは、反射型インジェクションやプロセス ハロウイングなど、標準以外の方法を使用してコード セグメントが割り当てられたことを示します。 さらに、コード セグメントの他の特性を処理して、報告されるコード セグメントの能力および動作に関するコンテキストを提供します。
* **Shellcode discovered (シェルコードが検出されました)**: シェルコードは、マルウェアがソフトウェアの脆弱性を突破した後に実行されるペイロードです。 このアラートは、悪意のあるペイロードに共通した振る舞いをする実行可能コードがクラッシュ ダンプ分析によって検出されたことを意味します。 悪意のないソフトウェアによる振る舞いである可能性もありますが、ソフトウェア開発の標準的な慣例からは逸脱しています。
* **Module hijacking discovered (モジュールのハイジャックが検出されました)**: Windows では、システムに共通の機能をソフトウェアから利用できるようにするために、ダイナミック リンク ライブラリ (DLL) を使用しています。 DLL ハイジャックは、マルウェアが DLL の読み込み順序を改変することによって行われます。このときメモリに悪質なペイロードが読み込まれ、任意のコードを実行できる状態となります。 このアラートは、クラッシュ ダンプ分析により、よく似た名前のモジュールが 2 つの異なるパスから読み込まれている状態が検出されたことを示しています。 パスの 1 つは、一般的な Windows システム バイナリが置かれた場所です。 悪意からではなく、インストルメント化や Windows OS の拡張、Windows アプリケーションの拡張といった目的で、通常のソフトウェア開発者が DLL の読み込み順序を変更することも皆無ではありません。 DLL の読み込み順序に対する悪意のある変更と、無害である可能性の高い変更とを判別しやすいように、Security Center では、読み込まれているモジュールに疑わしい特徴が見られるかどうかをチェックします。
* **Masquerading Windows module detected (Windows モジュールの偽装が検出されました)**: マルウェアには、Windows システムに共通するバイナリ名 (SVCHOST.EXE など) やモジュール名 (NTDLL.DLL など) が使用されている場合があります。悪質なソフトウェアを "紛れ込ませる" ことで、その正体をシステム管理者に見破られないようにするためです。 このアラートは、Windows システムのモジュール名と同じ名前のモジュールがクラッシュ ダンプ ファイルに含まれているものの、それ以外の点は一般的な Windows モジュールの基準をそのモジュールは満たしていないことを示します。 そのモジュールが悪意のあるものかどうかについては、ディスク上のなりすましモジュールのコピーを分析することによって、さらに詳しい情報を得ることができます。
* **Modified system binary discovered (システム バイナリの変更が検出されました)**: マルウェアは、侵入したシステム上でこっそりデータにアクセスしたり人目に付かないよう常駐したりするために、主要なシステム バイナリを改変する場合があります。 このアラートは、Windows OS の主要なバイナリがメモリ内またはディスク上で改変されたことがクラッシュ ダンプ分析によって検出されたことを意味します。 悪意からではなく、迂回やアプリケーションの互換性といった目的で、通常のソフトウェア開発者がメモリ内のシステム モジュールに変更を加えることも皆無ではありません。 悪意のあるモジュールとそうでないモジュールを判別しやすいよう、Security Center は、改変されたモジュールに疑わしい特徴が見られるかどうかをチェックします。

## <a name="network-analysis"></a>ネットワーク分析
Security Center のネットワーク脅威検出は、Azure IPFIX (Internet Protocol Flow Information Export) トラフィックからセキュリティ情報を自動的に収集することによって機能します。 この情報を分析し、ときには複数の情報源から得た情報との関連性を探りながら、脅威を特定します。

* **Possible incoming SQL brute force attempts (SQL ブルート フォース攻撃を受けている可能性)**: ネットワーク トラフィック分析で、疑わしい着信 SQL 通信が検出されました。 このアクティビティは、SQL サーバーに対するブルート フォース攻撃の試行と一致しています。
* **Suspicious incoming RDP network activity from multiple sources (複数の送信元からの疑わしい着信 RDP ネットワーク アクティビティ)**: ネットワーク トラフィック分析で、複数の送信元からの異常な着信 Remote Desktop Protocol (RDP) 通信が検出されました。 具体的には、サンプリングされたネットワーク データでは、固有の IP がコンピューターに接続していますが、この環境では異常と考えられます。 このアクティビティは、複数のホスト (ボットネット) から RDP エンド ポイントに対するブルート フォース攻撃の試行を示す可能性があります。
* **Suspicious incoming RDP network activity (疑わしい着信 RDP ネットワーク アクティビティ)**: ネットワーク トラフィック分析で、異常な着信 Remote Desktop Protocol (RDP) 通信が検出されました。 具体的には、サンプリングされたネットワーク データでは、コンピューターに多数の着信接続がありますが、この環境では異常と考えられます。 このアクティビティは、RDP エンド ポイントに対するブルート フォース攻撃の試行を示す可能性があります。
* **Suspicious outgoing RDP network activity to multiple destinations (複数の送信元からの疑わしい発信 RDP ネットワーク アクティビティ)**: ネットワーク トラフィック分析で、複数の宛先への異常な発信 Remote Desktop Protocol (RDP) 通信が検出されました。 このアクティビティは、コンピューターが侵害され、現在、外部の RDP エンド ポイントのブルート フォース攻撃に使用されていることを示す可能性があります。 この種の活動によって、自分の IP が外部のエンティティによって悪意のある IP とフラグが付けられる可能性があることに注意してください。
* **Suspicious outgoing RDP network activity (疑わしい発信 RDP ネットワーク アクティビティ)**: ネットワーク トラフィック分析で、異常な発信 Remote Desktop Protocol (RDP) 通信が検出されました。 具体的には、サンプリングされたネットワーク データでは、コンピューターからの多数の発信接続がありますが、この環境では異常と考えられます。 このアクティビティは、コンピューターが侵害され、現在、外部の RDP エンド ポイントのブルート フォース攻撃に使用されていることを示す可能性があります。 この種の活動によって、自分の IP が外部のエンティティによって悪意のある IP とフラグが付けられる可能性があることに注意してください。
* **Suspicious incoming SSH network activity (疑わしい着信 SSH ネットワーク アクティビティ)**: ネットワーク トラフィック分析で、異常な着信 SSH 通信が検出されました。 具体的には、サンプリングされたネットワーク データでは、コンピューターに多数の着信接続がありますが、この環境では異常と考えられます。 このアクティビティは、SSH エンド ポイントに対するブルート フォース攻撃の試行を示す可能性があります。
* **Suspicious incoming SSH network activity from multiple sources (複数のソースからの疑わしい着信 SSH ネットワーク アクティビティ)**: ネットワーク トラフィック分析で、異常な着信 SSH 通信が検出されました。 具体的には、サンプリングされたネットワーク データでは、固有の IP がコンピューターに接続していますが、この環境では異常と考えられます。 このアクティビティは、複数のホスト (ボットネット) から SSH エンド ポイントに対するブルート フォース攻撃の試行を示す可能性があります。
* **Suspicious outgoing SSH network activity (疑わしい発信 SSH ネットワーク アクティビティ)**: ネットワーク トラフィック分析で、異常な発信 SSH 通信が検出されました。 具体的には、サンプリングされたネットワーク データでは、コンピューターからの多数の発信接続がありますが、この環境では異常と考えられます。 このアクティビティは、コンピューターが侵害され、現在、外部の SSH エンド ポイントのブルート フォース攻撃に使用されていることを示す可能性があります。 この種の活動によって、自分の IP が外部のエンティティによって悪意のある IP とフラグが付けられる可能性があることに注意してください。
* **Suspicious outgoing SSH network activity to multiple destinations (複数の送信元からの疑わしい発信 SSH ネットワーク アクティビティ)**: ネットワーク トラフィック分析で、複数の宛先への異常な発信 SSH 通信が検出されました。 具体的には、サンプリングされたネットワーク データでは、コンピューターが固有の IP に接続していますが、この環境では異常と考えられます。 このアクティビティは、コンピューターが侵害され、現在、外部の SSH エンド ポイントのブルート フォース攻撃に使用されていることを示す可能性があります。 この種の活動によって、自分の IP が外部のエンティティによって悪意のある IP とフラグが付けられる可能性があることに注意してください。
* **Network communication with a malicious machine detected (悪意のあるマシンとのネットワーク通信が検出されました)**: ネットワーク トラフィック分析で、お客様のマシンがコマンドおよびコントロール センターの可能性がある対象と通信していることが検出されました。
* **Possible compromised machine detected (侵害された可能性のあるマシンが検出されました)**: ネットワーク トラフィック分析で、ボットネットの一部として動作していることを示す可能性がある発信アクティビティが検出されました。 この分析は、リソースからアクセスされている IP と、パブリック DNS レコードに基づいて行われています。


## <a name="sql-database-and-sql-data-warehouse-analysis"></a>SQL Database と SQL Data Warehouse の分析

Security Center のリソース分析は、[Azure SQL Database の脅威の検出](../sql-database/sql-database-threat-detection.md)機能や Azure SQL Data Warehouse との統合など、サービスとしてのプラットフォーム (PaaS) サービスに重点を置いています。 SQL の脅威の検出は、データベースにアクセスしたりデータベースを悪用したりしようとする、異常で有害な可能性がある不自然な動作を検出し、次のアラートをトリガーします。

* **Vulnerability to SQL Injection (SQL インジェクションの脆弱性)**: このアラートは、アプリケーションがデータベースにエラーのある SQL ステートメントを生成したときにトリガーされます。 これは、SQL インジェクション攻撃に対する脆弱性が存在する可能性を示すものです。 エラーのあるステートメントが生成される理由として、次の 2 つが考えられます。
    * アプリケーション コードの欠陥により、エラーのある SQL 文が作成される
    * アプリケーション コードまたはストアド プロシージャが、SQL インジェクションに悪用される可能性があるエラーのある SQL ステートメントを作成するときにユーザー入力をサニタイズしない
* **Potential SQL injection (SQL インジェクションの可能性)**:このアラートは、SQL インジェクションに対する特定されたアプリケーションの脆弱性に対してアクティブな悪用が発生したときにトリガーされます。 これは、攻撃者が脆弱なアプリケーション コードまたはストアド プロシージャを使用して悪意のある SQL 文を挿入しようとしていることを意味します。
* **Access from unusual location (通常とは異なる場所からのアクセス)**:このアラートは、だれかが通常とは異なる地理的な場所から SQL サーバーにログオンしたことで SQL Server へのアクセス パターンに変化が生じたときにトリガーされます。 このアラートで正当なアクション (新しいアプリケーションや開発者メンテナンス) が検出されることがあります。 別のケースでは、このアラートによって悪意のあるアクション (元従業員、外部の攻撃者) が検出されます。
* **Access from unusual Azure data center (通常とは異なる Azure データ センターからのアクセス)**:このアラートは、SQL Server へのアクセス パターンに変化が生じたときにトリガーされます。たとえば、だれかが通常とは異なる Azure データ センターから SQL Server にログオンしたことが、サーバーで最近確認された場合です。 このアラートで正当なアクション (Azure、Power BI、Azure SQL クエリ エディターの新しいアプリケーション) が検出されることがあります。 別のケースでは、このアラートによって Azure リソース/サービス (元従業員、外部の攻撃者) からの悪意のあるアクションが検出されます。
* **Access from unfamiliar principal (通常とは異なるプリンシパルからのアクセス)**:このアラートは、だれかが通常とは異なるプリンシパル (SQL ユーザー) を使用して SQL サーバーにログオンしたことで SQL サーバーへのアクセス パターンに変化が生じたときにトリガーされます。 このアラートで正当なアクション (新しいアプリケーションや開発者メンテナンス) が検出されることがあります。 別のケースでは、このアラートによって悪意のあるアクション (元従業員、外部の攻撃者) が検出されます。
* **Access from a potentially harmful application (潜在的に有害なアプリケーションからのアクセス)**:このアラートは、データベースにアクセスするために潜在的に有害なアプリケーションが使用されたときにトリガーされます。 このアラートで実行中の侵入テストが検出されることがあります。 別のケースでは、このアラートで一般的な攻撃ツールを使用した攻撃が検出されます。
* **Brute force SQL credentials (SQL 資格情報に対するブルート フォース攻撃)**:このアラートは、異なる資格情報でログインに失敗した回数が異常に多いときにトリガーされます。 このアラートで実行中の侵入テストが検出されることがあります。 別のケースでは、このアラートでブルート フォース攻撃が検出されます。

## <a name="contextual-information"></a>コンテキスト情報
アナリストが調査を行い、脅威の性質とそれを軽減する方法を判断するためには、追加のコンテキストが必要になります。  たとえば、ネットワーク異常が検出された際に、ネットワーク上で発生していたその他のイベントや対象となっているリソースを把握できなければ、対処法を決めることは困難です。 この判断を助けるため、セキュリティ インシデントにはアーティファクトや関連イベントのほか、調査に役立つ情報が含まれています。 利用できる追加情報は、検出された脅威の種類や環境内の構成によって異なります。また、すべてのセキュリティ インシデントで追加情報が利用できるとは限りません。

追加情報が利用可能な場合は、セキュリティ インシデントの警告の一覧の下に表示されます。 次のような情報が含まれます。

- ログの消去イベント
- 不明なデバイスからの PNP デバイスの接続
- 対応できないアラート
- 新しいアカウントの作成
- certutil ツールを使用してデコードされたファイル

![Unusual access alert](./media/security-center-alerts-type/security-center-alerts-type-fig20.png)


## <a name="next-steps"></a>次の手順
この記事では、Security Center のさまざまな種類のセキュリティ アラートについて説明しました。 セキュリティ センターの詳細については、次を参照してください。

* [Azure Security Center でのセキュリティ インシデントの処理](security-center-incident.md)
* [Azure Security Center の検出機能](security-center-detection-capabilities.md)
* [Azure Security Center 計画および運用ガイド](security-center-planning-and-operations-guide.md)
* [Azure Security Center に関する FAQ](security-center-faq.md): このサービスの使用に関してよく寄せられる質問が記載されています。
* [Azure セキュリティ ブログ](https://blogs.msdn.com/b/azuresecurity/): Azure のセキュリティとコンプライアンスについてのブログ記事を確認できます。
