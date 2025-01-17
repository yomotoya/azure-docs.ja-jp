---
title: Azure Data Factory の Mapping Data Flow のフィルター変換
description: Azure Data Factory の Mapping Data Flow のフィルター変換
author: kromerm
ms.author: makromer
ms.reviewer: douglasl
ms.service: data-factory
ms.topic: conceptual
ms.date: 02/03/2019
ms.openlocfilehash: e0b41850c149ff7095333cf77b780dec1f03b882
ms.sourcegitcommit: 509e1583c3a3dde34c8090d2149d255cb92fe991
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2019
ms.locfileid: "66234408"
---
# <a name="azure-data-factory-filter-transformation"></a>Azure Data Factory のフィルター変換

[!INCLUDE [notes](../../includes/data-factory-data-flow-preview.md)]

フィルター変換では、行のフィルター処理が実行されます。 フィルター条件を定義する式を作成します。 テキスト ボックスをクリックして、式ビルダーを起動します。 式ビルダーの中で、現在のデータ ストリームから次の変換に渡すことを許可する行を制御する (フィルター処理する) フィルター式を作成します。 フィルター変換は SQL ステートメントの WHERE 句と考えてください。

## <a name="filter-on-loanstatus-column"></a>loan_status 列をフィルター処理:

```
in([‘Default’, ‘Charged Off’, ‘Fully Paid’], loan_status).
```

Movies デモの year 列をフィルター処理:

```
year > 1980
```

## <a name="next-steps"></a>次の手順

列フィルター変換である[選択変換](data-flow-select.md)を試す
