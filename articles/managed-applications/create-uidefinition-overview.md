---
title: Azure マネージド アプリケーション用の UI 定義の作成を理解する | Microsoft Docs
description: Azure マネージド アプリケーションに使う UI 定義の作成方法について説明します。
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: managed-applications
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/26/2019
ms.author: tomfitz
ms.openlocfilehash: 3d0a6d97440404904c041369a4631fdd3fb618b4
ms.sourcegitcommit: 25a60179840b30706429c397991157f27de9e886
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66257560"
---
# <a name="create-azure-portal-user-interface-for-your-managed-application"></a>マネージド アプリケーション用の Azure ポータルのユーザー インターフェイスを作成する
このドキュメントでは、createUiDefinition.json ファイルの主要な概念について説明します。 Azure ポータルは、このファイルを使用して、マネージド アプリケーションを作成するためのユーザー インターフェイスを生成します。

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json#",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

CreateUiDefinition には必ず、次の 3 つのプロパティが存在します。 

* handler
* version
* parameters

マネージド アプリケーションでは、handler は常に `Microsoft.Compute.MultiVm` とする必要があります。また、サポートされている最新のバージョンは `0.1.2-preview` です。

parameters プロパティのスキーマは、指定した handler と version の組み合わせによって異なります。 マネージド アプリケーションでサポートされているプロパティは `basics`、`steps`、`outputs` です。 basics プロパティと steps プロパティには、Azure Portal に表示される "_要素_" (テキスト ボックス、ドロップダウンなど) が指定されます。 outputs プロパティは、指定された要素の出力値を Azure Resource Manager デプロイ テンプレートのパラメーターに対してマッピングする目的で使われます。

`$schema` は、指定することが推奨されますが、必須ではありません。 指定する場合は、`$schema` の URI 内のバージョンと `version` の値とを一致させる必要があります。

JSON エディターを使用して UI 定義を作成するか、または UI 定義サンドボックスを使用して UI 定義を作成およびプレビューすることができます。 このサンドボックスの詳細については、[Azure Managed Applications のポータル インターフェイスのテスト](test-createuidefinition.md)に関するページを参照してください。

## <a name="basics"></a>基本
Azure ポータルによってファイルが解析されたときに生成されるウィザードの最初のステップは必ず Basics ステップになります。 Azure Portal は、`basics` に指定された要素を表示することに加え、デプロイに使用するサブスクリプション、リソース グループ、場所をユーザーが選択するための要素を挿入します。 一般に、デプロイ全体にかかわるパラメーター (クラスターの名前、管理者の資格情報など) の入力をユーザーに求めるための要素は、このステップに追加する必要があります。

ユーザーのサブスクリプション、リソース グループ、または場所によって動作が異なるような要素は、basics では使用できません。 たとえば **Microsoft.Compute.SizeSelector** で利用可能な一連のサイズは、ユーザーのサブスクリプションや場所に応じて決まります。 そのため、**Microsoft.Compute.SizeSelector** は steps の中でしか使うことができません。 一般に、basics で使うことができるのは、**Microsoft.Common** 名前空間の要素だけです。 ただしそれ以外の名前空間 (**Microsoft.Compute.Credentials** など) であっても、ユーザーのコンテキストに依存しない一部の要素については使うことができます。

## <a name="steps"></a>手順
basics の後に表示するステップ (0 個以上) は steps プロパティに追加することができ、各ステップに少なくとも 1 つの要素を記述します。 デプロイするアプリケーションのロールまたはレベルごとにステップを追加することを検討してください。 たとえば、クラスターのマスター ノードとワーカー ノードとで分けて入力ステップを追加します。

## <a name="outputs"></a>出力
`outputs` プロパティは、Azure Portal が `basics` と `steps` の要素を Azure Resource Manager デプロイ テンプレートのパラメーターにマッピングする際に使われます。 このディクショナリのキーはテンプレート パラメーターの名前で、ディクショナリの値は、参照された要素の出力オブジェクトのプロパティです。

マネージド アプリケーションのリソース名を設定するには、`applicationResourceName` という名前の値を outputs プロパティに含める必要があります。 この値を設定しない場合は、アプリケーションによって名前に GUID が割り当てられます。 ユーザーに名前を要求するテキスト ボックスをユーザー インターフェイスに追加できます。

```json
"outputs": {
    "vmName": "[steps('appSettings').vmName]",
    "trialOrProduction": "[steps('appSettings').trialOrProd]",
    "userName": "[steps('vmCredentials').adminUsername]",
    "pwd": "[steps('vmCredentials').vmPwd.password]",
    "applicationResourceName": "[steps('appSettings').vmName]"
}
```

## <a name="functions"></a>Functions
Azure Resource Manager のテンプレート関数と同様に (構文と機能の両方)、CreateUiDefinition には、要素の入力と出力を操作するための関数および条件文などの機能が用意されています。

## <a name="next-steps"></a>次の手順
createUiDefinition.json ファイルには、それ自体に単純なスキーマが存在します。 その実際の深さは、すべてのサポートされている要素と関数に由来します。 これらの項目については、次の記事で詳しく説明します。

- [要素](create-uidefinition-elements.md)
- [関数](create-uidefinition-functions.md)

CreateUiDefinition の現在の JSON スキーマは、 https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json から入手できます。

ユーザー インターフェイス ファイルの例については、[createUiDefinition.json](https://github.com/Azure/azure-managedapp-samples/blob/master/samples/201-managed-app-using-existing-vnet/createUiDefinition.json) を参照してください。
