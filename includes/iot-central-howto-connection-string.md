---
title: インクルード ファイル
description: インクルード ファイル
services: iot-central
author: dominicbetts
ms.service: iot-central
ms.topic: include
ms.date: 04/09/2019
ms.author: dobett
ms.custom: include file
ms.openlocfilehash: eae4b1e919270413d4ca6627964fad9c7f5bd9bf
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66151980"
---
1. `dps-keygen` コマンドライン ユーティリティを使用して接続文字列を生成します。

    [キー ジェネレーター ユーティリティ](https://github.com/Azure/dps-keygen)をインストールするには、次のコマンドを実行します。

    ```cmd/sh
    npm i -g dps-keygen
    ```

1. 接続文字列を生成するには、先ほど書き留めておいた接続の詳細を使用して、次のコマンドを実行します。

    ```cmd/sh
    dps-keygen -di:<Device ID> -dk:<Primary or Secondary Key> -si:<Scope ID>
    ```

1. `dps-keygen` 出力からの接続文字列をデバイス コードで使用するためにコピーします。