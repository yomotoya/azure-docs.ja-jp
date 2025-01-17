---
title: インクルード ファイル
description: インクルード ファイル
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 12/11/2018
ms.author: cherylmc
ms.openlocfilehash: 31ccf14c82f6248c74d6af932fe9e338d26d2747
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66157234"
---
お客様がポイント対サイト接続を使用して VNet に接続する各クライアント コンピューターには、クライアント証明書がインストールされていなければなりません。 ルート証明書からそれを生成し、各クライアント コンピューターにインストールします。 有効なクライアント証明書をインストールしないと、クライアントが VNet への接続を試行したときに認証が失敗します。

クライアントごとに一意の証明書を生成することも、複数のクライアントに同じ証明書を使用することもできます。 一意のクライアント証明書を生成する利点は、1 つの証明書を失効させることができる点です。 そうでなければ、複数のクライアントで同じクライアント証明書が認証に使用されていて、お客様がそれを失効させる場合に、その証明書が使用されているすべてのクライアントに対して新しい証明書を生成してインストールする必要があります。

クライアント証明書は、次の方法を使用して生成できます。

- **エンタープライズ証明書:**

  - エンタープライズ証明書ソリューションを使用している場合は、共通名の値の形式 *name\@yourdomain.com* を使用してクライアント証明書を生成します。 *domain name\username* 形式の代わりに、この形式を使用します。
  - クライアント証明書が、ユーザー一覧の最初の項目が "*クライアント認証*" であるユーザー証明書テンプレートに基づいていることを確認します。 証明書を確認するには、それをダブルクリックし、**[詳細]** タブの **[拡張キー使用法]** を表示します。

- **自己署名ルート証明書:** お客様が作成するクライアント証明書が P2S 接続との互換性を備えるよう、P2S 証明書に関する以下のいずれかの記事の手順に従ってください。 これらの記事の手順では、互換性のあるクライアント証明書が生成されます。 

  * [Windows 10 PowerShell の手順](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientcert): これらの手順で証明書を生成するには、Windows 10 および PowerShell が必要です。 生成される証明書は、サポートされている任意の P2S クライアントにインストールできます。
  * [MakeCert の手順](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md): 証明書を生成する Windows 10 コンピューターにアクセスできない場合は、MakeCert を使用します。 MakeCert は非推奨になりましたが、まだ証明書の生成に使用することができます。 生成される証明書は、サポートされている任意の P2S クライアントにインストールできます。
  * [Linux の手順](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-linux.md)

  自己署名ルート証明書からクライアント証明書を生成した場合、お客様が生成に使用したコンピューターにそれが自動的にインストールされます。 クライアント証明書を別のクライアント コンピューターにインストールしたい場合は、それを .pfx ファイルとして、証明書チェーン全体と共にエクスポートします。 そうすることで、クライアントの認証に必要なルート証明書情報が含まれている .pfx ファイルが作成されます。 

**証明書をエクスポートするには**

証明書をエクスポートする手順については、「[PowerShell を使用したポイント対サイトの証明書の生成とエクスポート](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientexport)」を参照してください。
