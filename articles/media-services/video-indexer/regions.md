---
title: Video Indexer を利用できるリージョン - Azure
titlesuffix: Azure Media Services
description: この記事では、Video Indexer を利用できる Azure リージョンについて説明します。
services: media-services
author: anikaz
manager: johndeu
ms.service: media-services
ms.subservice: video-indexer
ms.topic: article
ms.date: 05/15/2019
ms.author: anzaman
ms.openlocfilehash: 404aaf91c0cb30df0a83353ef7397987ec3f8e80
ms.sourcegitcommit: 36c50860e75d86f0d0e2be9e3213ffa9a06f4150
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2019
ms.locfileid: "65799427"
---
# <a name="azure-regions-in-which-video-indexer-exists"></a>Video Indexer が存在する Azure リージョン

Video Indexer API には、呼び出しがルーティングされる Azure リージョンを設定する必要がある **location** パラメーターがあります。 これは、[Video Indexer が利用できる Azure リージョン](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all)にする必要があります。

## <a name="locations"></a>Locations

**Azure** パラメーターには、その値として Azure リージョンのコード名を指定する必要があります。 Video Indexer をプレビュー モードで使用する場合は、値として *"trial"* を指定する必要があります。 それ以外の場合は、お使いのアカウントが存在し、呼び出しがルーティングされる Azure リージョンのコード名を取得するために、次の行を [Azure CLI](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest) で実行できます。

```bash
az account list-locations
```

上記の行を実行すると、すべての Azure リージョンの一覧が取得されます。 探している *displayName* がある Azure リージョンに移動し、その *name* 値を **location** パラメーターで使用します。

たとえば、Azure リージョンの米国西部 2 の場合 (下に示されています)、"westus2" を **location** パラメーターで使用します。

```json
   {
      "displayName": "West US 2",
      "id": "/subscriptions/35c2594a-23da-4fce-b59c-f6fb9513eeeb/locations/westus2",
      "latitude": "47.233",
      "longitude": "-119.852",
      "name": "westus2",
      "subscriptionId": null
    }
```

## <a name="next-steps"></a>次の手順

- [API を使用して言語モデルをカスタマイズする](customize-language-model-with-api.md)
- [API を使用してブランド モデルをカスタマイズする](customize-brands-model-with-api.md)
- [API を使用して人物モデルをカスタマイズする](customize-person-model-with-api.md)
