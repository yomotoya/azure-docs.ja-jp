---
title: Azure Marketplace 向けのユーザー VM イメージを作成する
description: ユーザー VM イメージを作成するために必要な手順と参照情報の一覧を示します。
services: Azure, Marketplace, Cloud Partner Portal,
author: v-miclar
ms.service: marketplace
ms.topic: article
ms.date: 11/29/2018
ms.author: pabutler
ms.openlocfilehash: 0005ab517d38903b87889b67449569495e396265
ms.sourcegitcommit: c53a800d6c2e5baad800c1247dce94bdbf2ad324
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2019
ms.locfileid: "64938327"
---
# <a name="create-a-user-vm-image"></a>ユーザー VM イメージの作成

この記事では、汎用化された VHD からアンマネージド イメージを作成するために必要な 2 つの一般的なステップについて説明します。  各ステップ (イメージのキャプチャ、イメージの汎用化) について説明されている参照情報を提供します。


## <a name="capture-the-vm-image"></a>VM イメージのキャプチャ

VM のキャプチャに関する次の記事から、アクセス方法に対応する手順を使用してください。

-  PowerShell:[Azure VM から非管理対象 VM イメージを作成する方法](../../../virtual-machines/windows/capture-image-resource.md)
-  Azure CLI:[仮想マシンまたは VHD のイメージを作成する方法](../../../virtual-machines/linux/capture-image.md)
-  API:[Virtual Machines - キャプチャ](https://docs.microsoft.com/rest/api/compute/virtualmachines/capture)


## <a name="generalize-the-vm-image"></a>VM イメージの汎用化

以前に汎用化した VHD からユーザー イメージを生成しているため、これも汎用化する必要があります。  ここでも、アクセス メカニズムに対応する記事を次から選択します。  (ディスクをキャプチャしたときに、既に汎用化している可能性があります。)

-  PowerShell:[VM の汎用化](https://docs.microsoft.com/azure/virtual-machines/windows/sa-copy-generalized#generalize-the-vm)
-  Azure CLI:[手順 2:VM イメージを作成する](https://docs.microsoft.com/azure/virtual-machines/linux/capture-image#step-2-create-vm-image)
-  API:[Virtual Machines - 汎用化](https://docs.microsoft.com/rest/api/compute/virtualmachines/generalize)


## <a name="next-steps"></a>次の手順

次に、[証明書を作成](cpp-create-key-vault-cert.md)し、新しい Azure キー コンテナーに格納します。  この証明書は、VM 上でセキュリティ保護された WinRM 接続を確立するために必要です。
