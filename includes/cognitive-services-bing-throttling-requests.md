---
author: nitinme
ms.service: cognitive-services
ms.topic: include
ms.date: 11/09/2018
ms.author: nitinme
ms.openlocfilehash: 1d8340054ace25a0cdc36eef9c3d5b4238a6f99b
ms.sourcegitcommit: 509e1583c3a3dde34c8090d2149d255cb92fe991
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2019
ms.locfileid: "66124672"
---
サービスとサブスクリプションの種類によって、1 秒あたりのクエリ数 (QPS) が決まります。 アプリケーションに、クォータ内に収めるロジックを含めるようにしてください。 QPS の上限に達するか超えた場合、要求は失敗し、HTTP 429 状態コードが返されます。 応答には、`Retry-After` ヘッダーが含まれています。これは、別の要求を送信できるようになるまでに待機する必要がある時間を示します。

## <a name="denial-of-service-versus-throttling"></a>サービス拒否とスロットリング

このサービスは、サービス拒否 (DoS) 攻撃と QPS 違反を区別しています。 サービスが DoS 攻撃を疑っている場合、要求は成功します (HTTP 状態コードは 200 OK)。 しかし、応答の本文は空になります。